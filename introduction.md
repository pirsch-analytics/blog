slug = "introduction"
title = "Introduction"
date = 2021-06-04
summary = "Lets talk about us, why we started Pirsch and its future."
image = "introduction.png"

[author]
name = "Marvin Blum"
image = "mb.png"
github = "Kugelschieber"
twitter = "m5blum"
---

I think it's time to introduce ourselves and explain why we are building Pirsch. While we are always open if you talk to us directly, I feel like we are somewhat anonymous. Let's change that!

## Who We Are

We are an independent two-person startup from Germany. The Emvi Software GmbH (GmbH is the german version of a limited) was initially founded in 2019 for our first product [Emvi](https://emvi.com/) by Daniel Schramm and me.

Daniel has a background in product design and mechanical engineering and is responsible for UI and UX. Most of what you see on the dashboard has been designed and implemented by him.

I have a degree in computer science and have been programming since I was a child. I'm working on most of the technical parts, like the backend, server infrastructure, documentation, and so on. But it's hard to draw a clear line between the work we both do.

![Team](/blog/posts/introduction/team.png)

*Daniel on the left, Marvin on the right.*

## How It Started

About a year ago, while we were working on the full release of Emvi, I started rebuilding my website with the intention to write technical blog posts. We used Google Analytics for Emvi at that time and I was interested in how well the few blog posts I had (and still have) perform. In Europe, it became standard to add GA and a cookie banner, but my website was supposed to be easy to maintain and have a small footprint. And cookie banners are an ugly UX nightmare. So I rejected the idea and looked into a technique I heard about and was interested in: fingerprinting.

Just to give you some idea what fingerprinting means, here is an excerpt from our [documentation](https://docs.pirsch.io/):

> Pirsch makes use of the HTTP protocol to recognize visitors using a technique called fingerprinting. It generates a hash for each page visit calculated from the visitor's IP address, the User-Agent header, the current date, and a salt.

The main advantage of this is, that it doesn't require cookies and can't be traced back to the visitor. The [original article](https://marvinblum.de/blog/server-side-tracking-without-cookies-in-go-OxdzmGZ1Bl) on my blog goes into more detail about how that works.

I started implementing a [library](https://github.com/pirsch-analytics/pirsch) that could be integrated into Go ([golang](https://golang.org/)) applications, as that is my programming language of choice for anything server related. The reason why I wanted to analyze traffic from the backend is that we saw a lot of people using adblockers from the Emvi blog, which block tracking scripts. I don't have hard numbers, but especially people in IT will use script blockers and if you write technical blog posts, you will probably lose a lot of data.

After adding it to my website, I created a page with some charts showing how well my posts performed. Except for some bot traffic initially, I was quite pleased with the result. The page now redirects to Pirsch, but it looked like this:

![marvinblum.de Dashboard](/blog/posts/introduction/charts.png)

There were more charts, like visitors by page and time of day.

I kept adding more features and improved the library, and as Emvi didn't meet our expectations (mostly to very strong competition, like Notion and Roam Research), we decided to switch focus and make a product out of it in October last year.

Pirsch has come a long way since then. We initially took some inspiration from GoatCounter for the technical bits, but we built it mostly without minding competition, something that actually made Emvi worse. Pirsch has changed so much since then, that it now is a unique product with its own clear focus.

## How We Are Doing

So far, Pirsch has been doing quite well in our opinion. We have 10 paying customers generating about $76 MRR. All of them give valuable feedback and enjoy using it. Considering that we had no product in October and just started doing content marketing (no paid ads), we are doing fine. Let's hope we can increase growth and gain more traction.

## Plans for the Future

Pirsch lacks some important features to generate value if you're selling online or running paid marketing campaigns. That's something we already improved and we will keep working on within the next few months. Our next goal is to implement event tracking and better API support (mostly documentation and SDKs).

Apart from this short-term goal, we would like to provide a white-label version of Pirsch for agencies and freelancers, to enable them to resell our services. We will share more details about this in the future.

## Conclusion

I hope you enjoyed our first blog post. We will write more about how we operate Pirsch and give some tips on how to use it with greater effect in the future. In case you have questions or would like to get in touch, you can find us on Twitter [@PirschAnalytics](https://twitter.com/PirschAnalytics) or sent us an [email](mailto:contact@pirsch.io).
