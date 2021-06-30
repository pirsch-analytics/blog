---
title: "How We Build and Operate Pirsch"
date: 2021-06-30
summary: "Learn how we operate Pirsch on Hetzner cloud using HashiCorp Nomad, Traefik, Letsencrypt and more."
image: "techstack/images/pcb.jpg"
authors: ["Marvin Blum"]
draft: false
---

When it comes to building and hosting a SaaS, you will basically read about two approaches. The first one is to use the services of some (large) cloud provider, like AWS, Azure, or Google Cloud. This approach is usually taken by startups with funding, or prior experience using the services. The second one is to host it yourself, usually on dedicated servers or virtual machines. This lean approach is good if you want to keep it simple and get you started quickly at low cost.

I think we fall in between these two approaches, neither spending too much on cloud services or getting locked in, nor do we have a simple setup. That's why I think it's worth writing about how we operate Pirsch. In this article, you will learn how we develop Pirsch, what hardware and software we use, and why we made the technology choices we did.

## Hosting

Starting with hosting, we use virtual machines on Hetzner Cloud based in Falkenstein, Germany. The main reason we chose Hetzner is cost. A single core VM on Google Cloud for example starts at about $15/month, while a single core Hetzner VM costs about 2,50€/month. Pirsch runs on a three node cluster, plus an additional VM for the database, all of them configured with two cores and 4 GB of RAM (more on that later). We had a similar setup for Emvi on Google Cloud before, which cost about 250€/month, while we are now paying about 45€/month for everything, including cloud services.

Why not use dedicated servers you might ask. While it does make sense from a performance to cost perspective, dedicated servers are less flexible. Renting a dedicated server is more of a commitment then spinning up a VM you can stop or rescale at any time. Should the need arise, we can scale the VMs vertically or add dedicated servers. Flexibility is one of the main reasons the cloud got so popular, but it comes at a cost. Hetzner strikes a good balance between flexibility and costs.

## Cloud Services

## Programming Languages

## Development

## Software Choices

## Deployment

## Conclusion

*Image by [Adi Goldstein](https://unsplash.com/photos/EUsVwEOsblE)*
