slug = "our-recap-of-2021"
title = "Our Recap of 2021"
date = 2021-12-21
summary = "A summary of the past year, what we did, and what we have planned for 2022."
image = "recap2021.png"

[author]
name = "Marvin Blum"
image = "mb.png"
github = "Kugelschieber"
twitter = "m5blum"
---

2021 is almost over, so it's time to look back on how Pirsch developed and what we planned for the next year.

## How Did We Do?

Pirsch generated a gross volume of 2028€ from 48 customers. December was our best month so far, with a gross volume of 651€. We additionally generated revenue of about 4800€ implementing features for a larger client that we mostly had on our roadmap already (so they basically got sponsored).

Our server costs increased from about [45€/month](https://pirsch.io/blog/techstack/) to 290€/month, especially due to our *much* larger database server. We still host everything on Hetzner in Germany and will continue doing so.

As for traffic, you can always check out our [public dashboard](https://pirsch.pirsch.io/). Roughly, we had ~29k visitors, 55k page views, and a conversion rate of about 1.2% to 1.4%. We didn't measure the conversion rate from the beginning, so this number is not entirely accurate but the trend is upward.

## Development and Two Rewrites

A lot has changed since we moved out of Beta in March and have worked on Pirsch for about six months and released [33 updates](https://docs.pirsch.io/changelog/#100).

Our initial idea was to aggregate statistics for each day and store the aggregated data only. It turned out that we couldn't implement more advanced features doing so - this was the first time we rewrote most of our [open-source core library](https://github.com/pirsch-analytics/pirsch) and released it as version 2.0. The main change was the switch from Postgres to ClickHouse. Data is no longer aggregated but processed in real-time, reducing complexity and allowing us to filter on any field.

The second rewrite was necessary when we got contacted by a large client (150 million page views/month) and our queries didn't perform well. This was quite a stressful moment, as we temporarily broke most of Pirsch's functionality in an attempt to improve performance. We managed to get everything fixed within a week (12-14 hour workdays, yay) without anyone (?) noticing. We were unable to acquire the customer though, due to some compliance issues after the initial testing phase. In the end, we learned a lot from this and could make significant improvements to Pirsch, so it wasn't all wasted.

Alongside the major rewrites, we also added a *ton* of new features and improvements. Here are some highlights:

* new and improved charts for vital statistics
* more statistics, like the visitor city, entry and exit pages, UTM parameters, ...
* combinable and invertible filters
* a powerful API

Additionally, we teamed up with [Dailytics](https://dailytics.com/), bringing you more advanced and in-depth email reports.

## Our Plan for 2022

Our main goal for 2022 is to grow Pirsch to make a living off of it. This will allow us to fully focus on building the best privacy-friendly analytics tool possible. Marketing is our greatest weakness - we need to work on that but we're sure we can get there.

There are also two major features on our roadmap. A white-label solution for agencies to resell our services, and funnels.

The white-label solution idea exists since we started developing Pirsch and we still think it would be great for agencies to easily use Pirsch for their customers. A customizable (brandable) dashboard on a custom domain and an additional access management level are the main factors to make it happen.

Funnels also have been on our list for a long time. We were unsure how to implement them, but now have an idea of what they could look like - so that's a feature you can expect in 2022.

### Changes to Our Pricing

Pirsch evolved quickly in the past year. We initially set a lower price tag because we felt our feature set was too small to justify a higher price. This has now changed and we will make some adjustments to reflect the progress. Here are the changes for our three most used plans (a full list will be made available on our [pricing page](https://pirsch.io/pricing) in January):

* 10k page views: $48 -> $60 annually
* 100k page views: $96 -> $120 annually
* 200k page views: $144 -> $180 annually

The monthly pricing for these plans will stay the same.

## Conclusion

Thank you to everyone who supported us in the past year. You helped us to get Pirsch off the ground, by becoming a customer, sending us feedback and bug reports, and spreading the word. Also a special thank you to Dezeiraud, Rishi, Ferdinand, Gustavo, Nathan, Berry, William, and Zep for your helpful feedback and contributions (I hope I didn't miss someone).

We hope that you will have a nice and calm end of the year and stay with us in the next one.

Sincerely,
Your Pirsch Team
