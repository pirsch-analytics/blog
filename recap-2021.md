slug = "recap-2021"
title = "Recap 2021"
date = 2021-12-21
summary = "A recap of the past year, what we did, and what we have planned for 2022."
image = "recap2021.png"

[author]
name = "Marvin Blum"
image = "mb.png"
github = "Kugelschieber"
twitter = "m5blum"
---

2021 is almost over, so it's time for a quick recap of how Pirsch developed and what we are planning for the next year.

## How Did We Do?

Pirsch generated a gross volume of 2028€ from 48 customers. December was our best month so far, with a gross volume of 651€. We additionally generated revenue of about 4800€ implementing features for a larger client that we mostly had on our roadmap already (so they basically got sponsored).

Our server costs increased from about [45€/month](https://pirsch.io/blog/techstack/) to 290€/month, mostly due to our *much* larger database server. We still host everything on Hetzner in Germany and will continue doing so.

Traffic vise, you can always check our [public dashboard](https://pirsch.pirsch.io/). Roughly, we had ~29k visitors, 55k page views, and a conversion rate of about 1.2% to 1.4%. We didn't measure the conversion rate from the beginning, so this number is not quite accurate.

## Development and Two Rewrites

A lot has changed since we moved out of beta in March, after 2 1/2 months working on Pirsch and [33 updates](https://docs.pirsch.io/changelog/#100). Our initial idea was to aggregate statistics for each day and store only the aggregated data, but it turned out that we couldn't implement more advanced features this way. This was the first time we rewrote most of our [open-source core library](https://github.com/pirsch-analytics/pirsch) and released it as version 2.0. The main change was the switch from Postgres to ClickHouse. Data is no longer aggregated, but processed in real-time, reducing complexity and allowing us to filter on any field.

The third rewrite was necessary when we got contacted by a large client (150 million page views/month) and our queries didn't perform well. This was quite a stressful moment, as we temporarily broke most of Pirsch's functionality in an attempt to improve performance. We were able to get everything fixed within a week (12-14 hour workdays, yay) without anyone (?) noticing. We were not able to acquire the customer due to some compliance issues after the initial testing phase, but we learned a lot from this and improved Pirsch significantly.

Alongside these major rewrites, we also added a *ton* of new features and improvements. Here are some highlights:

* new and improved charts for vital statistics
* combinable and invertible filters for all statistics
* more statistics, like the visitor city, entry and exit pages, UTM parameters, ...
* a powerful API

We also teamed up with [Dailytics](https://dailytics.com/) to bring you advanced and more in-depth email reports.

## Our Plan for 2022

Our main goal for 2022 is to grow Pirsch to make a living off of it. This will allow us to fully focus on making the best privacy-friendly analytics tool possible. Marketing is our greatest weakness, and we need to work on that, but we're sure we can get there.

We also have two major features on our roadmap. A white-label solution for agencies to resell our services and funnels.

The white-label solution idea exists since we started developing Pirsch and we still think it would be great for agencies to easily use Pirsch for their customers. A customizable dashboard on a custom domain and an additional access management level are the main factors to make it happen.

Funnels also have been on our list for a long time. We were unsure how to implement them, but we now at least have an idea of what they could look like, so that's something you can expect to come in 2022.

### Changes to Our Pricing

Pirsch evolved quickly in the past year. We initially set a lower price tag because we felt our feature set was too small to justify higher pricing. This has now changed and we will make some adjustments to reflect the progress. Here are the changes for our three most used plans (a full list will be made available on our [pricing page](https://pirsch.io/pricing) in January):

* 10k page views: $48 -> $60 annually
* 100k page views: $96 -> $120 annually
* 200k page views: $144 -> $180 annually

The monthly pricing for these plans will stay the same.

## Conclusion

We would like to thank everyone who supported us in the past year. You helped us to get Pirsch off the ground, by becoming customers, sending us feedback, bug reports, and spreading the word. We hope that you will have a nice and calm end of the year and stay with us in the next one.

Sincerely,
Your Pirsch Team
