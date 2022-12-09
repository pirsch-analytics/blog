slug = "maglr-pirsch-integration"
title = "Case Study: How Maglr.com Integrated Pirsch Analytics"
date = 2022-12-09
summary = "We interviewed Berry van Elk about his Pirsch integration into Maglr as a replacement for Google Analytics."
image = "maglr.png"

[author]
name = "Marvin Blum"
image = "mb.png"
github = "Kugelschieber"
twitter = "m5blum"
---

*This is the first in a series of articles on how our customers use Pirsch. We are looking for interesting use cases and integrations. If you have something for us and would like to become part of this, reach out to our [support](mailto:support@pirsch.io).*

For our first article, we talked to Berry about his Pirsch integration into [Maglr](https://www.maglr.com/en).

**Hi, Berry! Please introduce yourself and tell us about Maglr.**

> My name is Berry van Elk, CEO of Maglr.com. We are a Dutch Saas platform that helps organizations worldwide share online stories with a better reading experience. Anyone without technical know-how is able to design and publish interactive stories via our design platform. Think of magazines, reports, presentations, infographics, or product brochures.

![Maglr](/blog/static/maglr/editor-create-buttons-interactions-naming-layer.png)

> Today, a lot of corporate content is shared in static formats, while the way we read information has completely changed. Ever tried to read a multi-page PDF on mobile?

> With Maglr, organizations share stories in a modern format. Mobile-friendly, visually formatted for the web, and organized in short, bite-sized articles with space for interactive additions. Updates can be made immediately, but most importantly, you can see who reads the story.

**What issues did you face that made you switch to Pirsch?**

> As soon as a project is shared, it is important for the customer to gain insight into the reader's behavior. Maglr is used for a better content experience, but in the end, it’s about the numbers. Did the design, the navigation, and the way an "annual report" was shared help to ensure that the story was well received?

![Statistics side panel](/blog/static/maglr/overview-stats-sidepanel.png)

> With these figures, we want to be able to go deeper into the content. Not only the global visitor numbers are important; a customer must be able to go a step deeper and really measure whether the design choices that have been made have contributed.

![Filter on project level](/blog/static/maglr/stats-filter-on-project.jpg)

> When developing the platform, we started with Google Analytics. We collected statistics from customers who agreed to this via a central tracker. Via the Google API, we were able to show the basic statistics of a publication with selections. This worked for a number of years until there was more resistance towards Google, loading results took too long, and they were inaccurate.

> We wanted to be able to measure in more detail where a customer should have the opportunity to make selections themselves.

![Filter on page level](/blog/static/maglr/stats-filter-on-page-level.jpg)

**How did you learn about Pirsch, and what made you choose it?

> We started looking for an alternative. We wanted to be able to create a dashboard ourselves and merge the measured data with our own. We wanted to be able to run trackers to measure the stats on our own domain. Not only is this important for ad blockers, but also for organizations that do not want third-party plugins in their publications.

> While searching, we came across numerous solutions. Too complex, where you are responsible for collecting and calculating the data. Or too simple, where you would be able to embed a dashboard but have no option to merge your own data.

> We ended up with Pirsch, which quickly showed some advantages for us:

> * It works without cookies, a growing concern among more and more customers who are using Google Analytics
> * It is partially open source, so if we ever want to host it ourselves, it is possible
> * A tracker where we can send events with our own meta data
> * A simple API where everything is calculated in advance with enough room for custom filters

> After creating a simple test, we took the next step.

**Can you give us some details about how you've integrated Pirsch into Maglr?**

> Because we use Pirsch in a multi-tenant environment, it took us a while to figure out how we could best organize the integration. This is in combination with the collection of specific data and the selections we wanted to make. Once the scheme was clear, integration was easy. From our experience with other platforms, calculating the data is the most difficult part, but this is already fully provided in Pirsch.

> Using the API, we create a separate dashboard for each customer in Pirsch with its own API keys. Every project for that specific customer is measured on the same dashboard in Pirsch. Instead of the standard page URL, we send a series of parameters that we can filter on from our platform. So instead of the path "/name-publication/page.html" we send "/client_ID/project_type/project_ID/page_ID". Doing this, any selection is possible. We supplement the metadata, such as the actual URL or page name, with our own data.

![Global statistics for a project](/blog/static/maglr/global-stats-and-per-project.jpg)

> To push page views and events in a modified way, we use AWS Lambda and the Pirsch API. From JavaScript, we forward the custom events to a lambda function, which will then make modifications to the request and forward the result to Pirsch.

> From the Maglr dashboard, each project connects to the Pirsch API. We then merge the data within the different views (written in VueJS). Many ideas are borrowed from the Pirsch dashboard, which made it easier for us to implement. For regular page views and events, there are enough filter options available in the API to present the data in your own way.

**What do your customers think about the integration?**

> The nice thing is that the customers don’t know anything about the integration. We did tell them where the data is stored and that we are using Pirsch in combination with the new dashboard. But when looking at the dashboard, all statistics are completely embedded within the design. Within the publication, page views and events are sent to stats.maglr.com, so it all fits seamlessly into Maglr itself.

> The feedback itself is great. Before this update, customers had to wait 30 seconds to collect data from the Google API. The data is now displayed in real-time within seconds, with the option to make instant selections.

> Designers are now also able to see in detail how their UX design is being used, something that wasn’t possible before.

**Thank you for your time and detailed answers, Berry!**

## Demo Video

<video width="768" height="442" style="border-radius: 6px;">
    <source src="/blog/static/maglr/demo.mp4" type="video/mp4">
</video> 

## More Screenshots

![Project selection](/blog/static/maglr/project-selection.jpg)

![Publication type selection](/blog/static/maglr/publication-type-selection.jpg)

![Date Selection](/blog/static/maglr/date-selection.jpg)
