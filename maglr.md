slug = "maglr-pirsch-integration"
title = "Use Case: Integrating Pirsch Into Maglr"
date = 2022-12-09
summary = "We interviewed Berry van Elk about his Pirsch integration into Maglr."
image = "maglr.png"

[author]
name = "Marvin Blum"
image = "mb.png"
github = "Kugelschieber"
twitter = "m5blum"
---

## Can you give us a short introduction of yourself and to Maglr?

My name is Berry van Elk, CEO of Maglr.com. We are a Dutch Saas platform that helps organizations worldwide to share online stories with a better reading experience. Anyone without technical knowhow is able to design and publish interactive stories via our design platform. Think of magazines, reports, presentations, infographics or product brochures.

Today, a lot of corporate content is still shared in (older) static formats, while the way we read information has completely changed. Ever tried to read a multi-page PDF on mobile?

With Maglr, organizations share stories in a modern format. Easy to read on mobile, visually formatted for the web, organized in short, bite-sized articles with room for interactive additions. Updates can be made immediately, but the most important; you can see who reads the story.

## What issues did you face before switching to Pirsch?

As soon as a published project is shared, it is important for the customer to gain insight into the reading behaviour. Maglr is used for a better content experience, but in the end it’s about the numbers. Did the design, the navigation, the way how, for example, an 'annual report' was shared, ultimately ensured that the story was well read?

With these figures we want to be able to go deeper into the content. Not only the global visitor numbers are important, a customer must be able to go a step deeper and really measure whether the design choices that have been made have contributed.

When developing the platform, we started with Google Analytics. We collected statistics from customers who agreed to this via a central tracker. Via the Google API we were able to show basic statistics of a publication with selections. This worked for a number of years until there was more resistance towards Google, the loading of results took longer and longer and the results were no longer accurate.

We wanted to be able to measure in more detail where a customer should have the opportunity to make selections themselves.

## How did you learn about Pirsch and why did you choose it?

We started looking for an alternative. We wanted to be able to create a dashboard ourselves and merge the measured data with our own data. We wanted to be able to run trackers to measure the stats on our own domain. Important for addblockers but also organizations that don’t want third party plugins into their publications.

In the search we came across numerous solutions. Complex, where you are responsible for collecting + calculating the data. Or very simple, where you may be able to embed a dashboard, but have no option to merge your own data.

We ended up with Pirsch, which quickly showed some advantages for us:

* It’s without cookies, a growing concern by more and more customers who are using Google Analytics
* Partly open source, will we ever get to a point where we want to host it ourselves (back-end) it is possible
* A tracker where we can send events with our own meta data
* A simple API where everything is calculated in advance with enough room for custom filters

After creating a simple test, we made the next step.

## How did the implementation go?

Because we use Pirsch in combination with a multi-tenant environment, it took a while to figure out how we could best organize this. This in combination with the collection of specific data and the selections we wanted to make. Once the scheme was clear, integration was easy. From experiences with other platforms, calculating the data is the most difficult, this was already fully provided in Pirsch.

Via the API we create a separate 'website' for each customer in Pirsch with its own API keys. Every project of that specific customer is measured on the same 'website' in Pirsch. Instead of the standard page URL, we send a series of parameters that we can filter on from our platform. So instead of the path “/name-publication/page.html” we send “/client_ID/project_type/project_ID/page_ID”. With this any selection is possible. We supplement the metadata, such as the actual URL or page name, from our own data.

To push these 'pageviews' and 'events' in a modified way, we use the Pirsch back-end API. From JS we first forward the custom events to an AWS Lambda function (stats.maglr.com). From this point the information is forwarded to Pirsch.

From the dashboard, each 'client' connects to the Pirsch API itself. We then merge this data with the different dashboard views (VueJS). Many ideas are borrowed from the Pirsch dashboard, which makes it extra easy in combination with the existing API calls. For the regular 'pageviews' and 'events' there are enough filter options available in the API to present the data in your own way.

## What do your customers think about the integration?

The nice thing is that the customers don’t know anything about the integration. We did tell them where the data is stored and that we are using Pirsch in combination with the new dashboard. But when opening the dashboard all statistics are completely embedded within the design. Within the publication pageviews and events are sent to stats.maglr.com, so it all fits seamlessly into Maglr itself.

The feedback itself is great. Before this update customers had to wait 30 seconds to collect data from the Google API. The data is now shown, real-time in seconds with the option to make instant selections.

Designers are now also able to see in detail how their UX design is being used, something that wasn’t possible before.
