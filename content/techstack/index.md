---
title: "How We Build and Operate Pirsch"
date: 2021-07-03
summary: "Learn how we operate Pirsch on Hetzner cloud using HashiCorp Nomad, Traefik, Letsencrypt and more."
image: "techstack/images/pcb.jpg"
authors: ["Marvin Blum"]
draft: false
---

*This article is intended for readers with a technical background. Basic knowledge of IT and server administration (Linux) is required.*

> TL;DR
>
> This is our tech-stack:
> * hosting: Hetzner Cloud
> * services: AWS S3 and SES, Hetzner VPN, load balancing, block storage, and managed SSL certificates, Stripe for payments
> * programming languages: Go (golang), TypeScript
> * software: Docker, HashiStack (Consul + Nomad + Vault) for container orchestration, GoLand and Visual Studio Code for development

When it comes to building and hosting a SaaS, you will basically read about two approaches. The first one is to use the services of some (large) cloud provider, like AWS, Azure, or Google Cloud. This approach is usually taken by startups with funding, or prior experience using the services. The second one is to host it yourself, usually on dedicated servers or virtual machines. This lean approach is good if you want to keep it simple and get started quickly at low cost.

I think we fall in between these two approaches, neither spending too much on cloud services/servers or getting locked in, nor do we have a simple setup. That's why I think it's worth writing about how we operate Pirsch. In this article, you will learn how we develop Pirsch, what hardware and software we use, and why we made the technology choices we did.

## Hosting

Starting with hosting, we use virtual machines on Hetzner Cloud based in Falkenstein, Germany running Ubuntu Linux. The main reason we chose Hetzner is cost. A single core VM on Google Cloud for example starts at about $15/month, while a single core Hetzner VM costs about 2,50€/month. Pirsch runs on a three node cluster, plus an additional VM for the database, all of them configured with two cores and 4 GB of RAM (more on that later). We had a similar setup for Emvi on Google Cloud before, which cost about 250€/month, while we are now paying about 45€/month for everything, including cloud services.

Why not use dedicated servers you might ask. While it does make sense from a performance to cost perspective, dedicated servers are less flexible. Renting a dedicated server is more of a commitment then spinning up a VM you can stop or rescale at any time. Should the need arise, we can scale the VMs vertically or add dedicated servers later on. Flexibility is one of the main reasons why cloud services became so popular, but it comes at a cost. Hetzner strikes a good balance between flexibility and costs.

## Services

We use a bunch of (cloud) services.

### Storage

We use two types of storage right now. The first one is block storage (aka "volumes") on Hetzner for the Postgres database. The ClickHouse instance uses the hard disk of the VM. Both of them are replicated automatically, so you don't need to worry about data loss. The second one is AWS S3 for user pictures and email reports. We use an external object storage so that we can serve images from any cluster node and don't get locked in. The S3 API is basically an industry standard by now. So, should the need arise, we can also switch to a self-hosted alternative.

### Email

AWS SES (Simple Email Service) is our email service of choice. The main reason here is that hosting a mail server is a nightmare and a waste of time. We used SendGrid before, but it costs $15/month for 40,000 emails, while SES only costs 10 cents for 1,000 emails (so $4 for the same amount as SendGrid) and we don't need any of the other SendGrid features. We usually send less than a 1,000 emails a months and we haven't payed anything for SES yet (I think it's free up to a certain amount of emails or they just don't issue bills for a few cents). Emails are always rendered on our backend using Go templates. The newsletter is send manually.

### SSL Certificates and Networking

SSL is something I struggled a lot with. While Letsencrypt is an amazing service I really appreciate, there are a million ways to issue certificates and place them on your servers. I was never quite sure which one I should use. We run our own [acme-dns](https://github.com/joohoi/acme-dns) server, which seemed to work but then interfered with some DNS service running on port 53. We used Traefik's build-in system to issue certificates, build our own service to update the load balancer certificate on Hetzner, and so on. In the end, Hetzner released an update so that the load balancer can use a fully managed (wildcard) certificate. You just have to use Hetzner's DNS servers and it will be updated automatically.

![Certificate](posts/techstack/certificate.png)

Appart from the load balancer, we also use a firewall, only allowing ports that must be open, and a private network for the cluster and database servers. Everything build right into the Hetzner cloud.

### Subscriptions and Payments

Subscriptions and payments are managed and processed by [Stripe](https://stripe.com/). We have used Stripe before and kept using it for Pirsch. The API and dashboard are fantastic and they have a great [Go SDK](https://github.com/stripe/stripe-go).

## Programming Languages

If you follow our development on [GitHub](https://github.com/pirsch-analytics) or [Twitter](https://twitter.com/PirschAnalytics), you probably know already that we're using Go (golang) for backend and TypeScript for frontend development. I don't want to go into to much detail here, as there are other articles explaining the advantages and disadvantages of these languages better.

![Programming Languages](posts/techstack/programming-languages.png)

Go is a fantastic language with good performance characteristics, as it is statically typed and compiled to machine code. The simplicity helps to keep Pirsch maintainable and extendable, and we like that it is made for the web. Our website for example is rendered using Go templates.

TypeScript is something we just recently switched to, coming from vanilla JavaScript (ES6). It's a good fit for Vue 3 applications, which we use to build our dashboard. I was sceptical about TypeScript, because I didn't really see the need for types in a scripting language. But as complexity growth, it really helps to maintain the app. You can read more about this [on my personal blog](https://marvinblum.de/blog/my-experience-with-vue-3-and-typescript-so-far-bZ1DQzJdjK).

## Development

Something we highly value is that we can build, test, and run Pirsch locally. For this reason, all parts of the application (backend, website, dashboard, batches, and databases) can be started without having to build the Docker images first or changing the YAML configuration. Only the databases (Postgres and ClickHouse) are run through Docker on our machines. This allows us to quickly iterate, test new features, and experiment. Additionally, we generate a test data set on startup, so that we have something to look at when we open the dashboard.

All parts of the application can be started with a simple `go run main.go` or `npm run watch` (for the dashboard) command inside their respective directory. This is what the project directory structure looks like.

![Project structure](posts/techstack/structure.png)

If you look carefully, you'll notice that we have a `run_tests.sh` script. This is used to locally run all Go and TypeScript tests. As we are a two-person company, we didn't bother setting up CI (yet). Before each commit or release we run the script to ensure that are tests are passing. This is probably not how you should do it (you might forget to run it) and clearly a lazy solution, but the tests only take a couple of minutes to complete and are usually cached, so only a few seconds in reality.

Before doing a release, we build the Docker images locally and push them to the GitHub container registry (all code is managed on GitHub).

## The HashiStack, Databases, and Deployment

This section is the most requested by our users and followers. I won't explain every detail of our setup, but I do want to highlight why you should consider it in favor of other container orchestrators like Kubernetes.

### Consul, Vault, and Nomad

When people talk about the HashiStack, they mean the combination of [Consul](https://www.consul.io/docs/intro), [Vault](https://www.hashicorp.com/products/vault), and [Nomad](https://www.nomadproject.io/) developed by HashiCorp. These three pieces of software combined make up the server cluster for Pirsch. There is a free open-source version for each of them and an enterprise tier for larger organizations and multi-cloud clusters. HashiCorp also offers managed solutions, in case you don't want to maintain it yourself.

Consul is used for server meshing and service discovery. It provides a DNS service to resolve hostnames (like my.service.consul) to IP addresses. Vault stores secrets securely and provides access to them from Nomad. It's a very powerful tool that offers a lot more than that, but we only use to manage secrets and passwords right now. Nomad is a container orchestrator. We use it to schedule our containers and batch workloads (more on that below the deployment section).

Combined, Consul, Vault, and Nomad can be considered a lightweight alternative to Kubernetes. Lightweight because they are easy to set up and maintain, making them a good fit for small businesses that want to maintain their own cluster. The HashiCorp configuration language (HCL) is a great improvement over Kubernetes YAML files and there are far less concepts to learn. Each part of the stack has its own focus and can be installed independently from the other systems, but they integrate very well. Nomad for example will automatically discover other nodes using Consul when installed.

Another reason to chose the HashiStack over its alternatives is documentation. HashiCorp's documentation pages are very well written, beautiful, and most importantly, complete. You can set up the stack following the instructions without missing anything important. Something I really dislike about documentation is when it skip steps because they are "too complicated" at that point. HashiCorp doesn't make these tradeoffs and explains everything required to set up a production ready cluster. You don't have to spent countless hours figuring out how to make it secure or fix something missing in the documentation.

Last but not least, all HashiStack tools have beatiful web UIs, making it really easy to deploy your software, discover issues, view log files, and more.

> The only thing that lead to some confusion while setting up the stack was that Consul's service discovery didn't work on our Ubuntu servers first. The issue was that the DNS service collided with systemd-resolved on port 53. The solution was to make systemd-resolved listen to the Consul DNS service. This can be configured by editing the `/etc/systemd/resolved.conf` and changing the following lines.
>
> ```
> DNS=127.0.0.1
> Domains=~consul
> ```
>
> We also had to add these two iptable rules.
>
> ```
> iptables -t nat -A OUTPUT -d localhost -p udp -m udp --dport 53 -j REDIRECT --to-ports 8600
> iptables -t nat -A OUTPUT -d localhost -p tcp -m tcp --dport 53 -j REDIRECT --to-ports 8600
> ```

### Databases

Pirsch makes use of two databases, Postgres and [ClickHouse](https://clickhouse.tech/). You probably have heared of Postgres before. We use it to store user account data and configuration. It's part of the server cluster as it isn't under heavy load and therefor doesn't require its own server.

You might not have heared of ClickHouse though. It's an analytical OLAP database developed by Yandax. The main difference to generalized databases like Postgres is, that it stores the data in a time series on disk. This allows it to quickly search through and aggregate data based on time ranges. We chose it because it perfectly fits our requirements and is very well supported on GitHub. It's installed on its own server, as it can become very performance hungry and we want to keep response times low. Right now it only uses a small two core 4 GB RAM virtual machine, but we can upscale it at any time.

### Deployment

TODO

## Conclusion

TODO

*Image by [Adi Goldstein](https://unsplash.com/photos/EUsVwEOsblE)*
