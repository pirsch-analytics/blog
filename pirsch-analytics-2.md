slug = "introducing-pirsch-analytics-2.0"
title = "Introducing Pirsch Analytics 2.0: Custom Domains, Themes, Organizations and More"
date = 2023-07-08
summary = "Today we are releasing Pirsch Analytics 2.0 including custom domains, themes, organizations and more."
image = "pirschanalytics2.png"

[author]
name = "Daniel Schramm"
image = "ds.png"
github = "Motorschpocht"
---

# Looking Into the Past

Funnily enough, today is exactly 1111 days (or just over three years) since Marvin published an article on his personal website titled "[Server-Side Tracking Without Cookies In Go](https://marvinblum.de/blog/server-side-tracking-without-cookies-in-go-OxdzmGZ1Bl)". The reason was simple: less is more. He wanted his new website to be very minimal, but he still wanted to know how many people visited it on a daily, weekly, or monthly basis. But then, as now, Google Analytics was anything but simple and, above all, unethical.

Being a big advocate of open source software, he went ahead and built his [own little library called Pirsch](https://github.com/pirsch-analytics/pirsch) in Go. In his blog post he describes exactly what he was thinking and how Pirsch worked in the beginning.

We had been working on a knowledge management tool for a long time. You can imagine it a bit like Notion. Unfortunately, the success we had hoped for did not materialize, so we decided to try something new: After seeing how well Pirsch worked as a small library, we wanted to turn it into our own product — without really checking the market beforehand. As usual for indie hackers, we wanted to do everything better this time. Spoiler alert: we have not.

# Humble Beginnings

The [first version](https://twitter.com/PirschAnalytics/status/1325446163894579201) was rough. As any good founder will tell you, "don't release software without dark mode," [so we didn't](https://twitter.com/PirschAnalytics/status/1334135233218826242). Pirsch slowly came to life on December 5, 2020 and 11 days later we started the [first launch on ProductHunt](https://www.producthunt.com/products/pirsch-analytics#pirsch-analytics-beta).

Even though the launch didn't go through the roof, the feedback was quite positive. Pirsch reached 1.0 on March 16, 2021, at which time we measured 260,000 unique visitors to 118 web pages.

What followed was two years of steady growth. Nothing TechCrunch would write about, but enough to keep us motivated and make Pirsch a little better every week. Today we have over 350 paying customers, around 15,000 websites and more than 1.15 billion page views collected. Not bad at all, if you ask me.

# Pirsch Analytics 2.0

Today we are releasing Pirsch Analytics 2.0. Many of you will notice at first glance that not much has changed visually since version 1.17.41. This is due to the fact that a lot of changes have been made behind the scenes. Technical improvements that make the backend more reliable, the data more accurate and the dashboard faster.

Perhaps more obvious is the slightly different header structure. The name of the site has moved to the top, and we've introduced tabs that, among other things, lead to the new overview. Also, this move is in preparation for big features coming later this year (looking at you, funnels).

We are especially proud of the new whitelabeling features. Appealing design has always been important to us, and with the new options, everyone can design their dashboard the way they want. We think it's the best theming available in analytics right now.

Of course, this includes a custom logo, and as an added bonus, the dashboard can have its own domain. So now you can have analytics.your-company.com or analytics.your-client.com for a truly seamless experience.

![Pirsch Analytics - Dashboard White Labeling](/blog/static/pirschanalytics2/dashboards.gif)

To make it even easier to work in a team, we introduce organizations in addition to the normal invitation of users to websites. This makes it easy to manage a large team and clients with just a few clicks.

# A Few Words About Pricing

When we started working on Pirsch, it was clear that it couldn't be free if it was going to be sustainable. However, we wanted to make the transition from Google Analytics as cheap as possible, and to this day we are one of the cheapest providers.

In order to continue this, we have decided to introduce a second pricing tier called Pirsch Plus, which will include more specific features in the future that go beyond simply measuring visitor flows.

The good news is that if you are already a customer, nothing will change for you. For new customers, we have introduced a limit of 50 websites in the smaller Standard tier. Most customers don't even come close to this limit. For more information, please visit our new [Pricing Page](https://pirsch.io/pricing).

# Thank you!

This release contains over 250 commits and over 50,000 lines of code. We hope you like it and look forward to your feedback. We continue to have a lot of fun working on Pirsch and hope to do so for many years to come. This is made possible by you, so a big thank you for your support!
