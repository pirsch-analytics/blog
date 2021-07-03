---
title: "How We Build and Operate Pirsch"
date: 2021-06-30
summary: "Learn how we operate Pirsch on Hetzner cloud using HashiCorp Nomad, Traefik, Letsencrypt and more."
image: "techstack/images/pcb.jpg"
authors: ["Marvin Blum"]
draft: false
---

> TL;DR
>
> This is our tech-stack:
> * hosting: Hetzner Cloud
> * cloud services: AWS S3 and SES, Hetzner VPN, load balancing, block storage, and managed SSL certificates
> * programming languages: Go (golang), TypeScript

When it comes to building and hosting a SaaS, you will basically read about two approaches. The first one is to use the services of some (large) cloud provider, like AWS, Azure, or Google Cloud. This approach is usually taken by startups with funding, or prior experience using the services. The second one is to host it yourself, usually on dedicated servers or virtual machines. This lean approach is good if you want to keep it simple and get started quickly at low cost.

I think we fall in between these two approaches, neither spending too much on cloud services/servers or getting locked in, nor do we have a simple setup. That's why I think it's worth writing about how we operate Pirsch. In this article, you will learn how we develop Pirsch, what hardware and software we use, and why we made the technology choices we did.

## Hosting

Starting with hosting, we use virtual machines on Hetzner Cloud based in Falkenstein, Germany. The main reason we chose Hetzner is cost. A single core VM on Google Cloud for example starts at about $15/month, while a single core Hetzner VM costs about 2,50€/month. Pirsch runs on a three node cluster, plus an additional VM for the database, all of them configured with two cores and 4 GB of RAM (more on that later). We had a similar setup for Emvi on Google Cloud before, which cost about 250€/month, while we are now paying about 45€/month for everything, including cloud services.

Why not use dedicated servers you might ask. While it does make sense from a performance to cost perspective, dedicated servers are less flexible. Renting a dedicated server is more of a commitment then spinning up a VM you can stop or rescale at any time. Should the need arise, we can scale the VMs vertically or add dedicated servers later on. Flexibility is one of the main reasons why cloud services became so popular, but it comes at a cost. Hetzner strikes a good balance between flexibility and costs.

## Cloud Services

We use a bunch of cloud services. Mostly because they are cheap or we didn't want to host them ourselves.

### Storage

We use two types of storage right now. The first one is block storage (aka "volumes") on Hetzner for the Postgres database. The ClickHouse instance uses the hard disk of the VM. Both of them are replicated automatically, so you don't need to worry about data loss. The second one is AWS S3 for user pictures and email reports. We use an external object storage so that we can serve images from any cluster node and don't get locked in. The S3 API is basically an industry standard by now. So, should the need arise, we can also switch to a self-hosted alternative.

### Email

AWS SES (Simple Email Service) is our email service of choice. The main reason here is that hosting a mail server is a nightmare and a waste of time. We used SendGrid before, but it costs $15/month for 40,000 emails, while SES only costs 10 cents for 1,000 emails (so $4 for the same amount as SendGrid) and we don't need any of the other SendGrid features. We usually send less than a 1,000 emails a months and we haven't payed anything for SES yet (I think it's free up to a certain amount of emails or they just don't issue bills for a few cents). Emails are always rendered on our backend using Go templates. The newsletter is send manually.

### SSL Certificates and Networking

SSL is something I struggled a lot with. While Letsencrypt is an amazing service I really appreciate, there are a million ways to issue certificates and place them on your servers. I was never quite sure which one I should use. We run our own [acme-dns](https://github.com/joohoi/acme-dns) server, which seemed to work but then interfered with some DNS service running on port 53. We used Traefik's build-in system to issue certificates, build our own service to update the load balancer certificate on Hetzner, and so on. In the end, Hetzner released an update so that the load balancer can use a fully managed (wildcard) certificate. You just have to use Hetzner's DNS servers and it will be updated automatically.

![Certificate](posts/techstack/certificate.png)

Appart from the load balancer, we also use a firewall, only allowing ports that must be open, and a private network for the cluster and database servers. Everything build right into the Hetzner cloud.

## Programming Languages

If you follow our development on [GitHub](https://github.com/pirsch-analytics) or [Twitter](https://twitter.com/PirschAnalytics), you probably know already that we're using Go (golang) for backend and TypeScript for frontend development. I don't want to go into to much detail here, as there are other articles explaining the advantages and disadvantages of these languages better.

![Programming Languages](posts/techstack/programming-languages.png)

Go is a fantastic language with good performance characteristics, as it is statically typed and compiled to machine code. The simplicity helps to keep Pirsch maintainable and extendable, and we like that it is made for the web. Our website for example is rendered using Go templates.

TypeScript is something we just recently switched to, coming from vanilla JavaScript (ES6). It's a good fit for Vue 3 applications, which we use to build our dashboard. I was sceptical about TypeScript, because I didn't really see the need for types in a scripting language. But as complexity growth, it really helps to maintain the app. You can read more about this [on my personal blog](https://marvinblum.de/blog/my-experience-with-vue-3-and-typescript-so-far-bZ1DQzJdjK).

## Development

## The HashiStack and Deployment

## Conclusion

*Image by [Adi Goldstein](https://unsplash.com/photos/EUsVwEOsblE)*
