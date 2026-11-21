slug = "introducing-pirsch-analytics-3.0"
title = "Introducing Pirsch Analytics 3.0"
date = 2026-11-21
summary = "The next major version of Pirsch Analytics is now available, setting us up for the future."
image = "pirschanalytics3.png"

[author]
name = "Marvin Blum"
image = "mb.png"
github = "Kugelschieber"
twitter = "m5blum"
---

Today, we're happy to announce that the next major version of Pirsch, version 3, is new available! 🎉

Our last major update was in 2023. Since then, we have updated Pirsch hundreds of times and made improvements to it over the years. While it has been a fantastic journey and we have grown considerably, there have been limitations. Version 3 is the next stage in its evolution, featuring a complete rewrite of the core responsible for data ingestion and generating statistics.

You might not notice the changes on the surface, but they are significant, and we plan to release features that will have a more direct impact on how you work with Pirsch in the coming months. Version 3.0 is just the first step. The changes described below are not yet fully available. You can see this from the headlines.

## Why a New Major Version?

We have been making continuous improvements to v2 since its launch, but we have encountered limitations that cannot be resolved without starting again from scratch. Many of these limitations were reported by you, our customers.

* The API was more complicated and difficult to use then neccessary
* The permission model needed to be simpler and more granular
* It wasn't possible to generate specialised reports
* Data ingestion had room for improvement
* Events didn't support nested metadata

The new core will allow us to address these points and form the basis of our expansion strategy. For instance, we intend to provide AI support through the new API and a custom MCP server, enabling you to use Pirsch with any frontier model and, hopefully, with our own EU-based LLM hosted on Hetzner for compliance.

## Data Migration (v3)

v3 requires your existing data to be migrated. This process runs in the background and will not affect your day-to-day use of Pirsch. However, until the final step of the migration process has been completed, some of your historical data may not appear on your dashboard. There's no need to worry if a few numbers appear incomplete for a short time: everything will be there once the migration is finished.

In combination with the new reporting system, statistics will be generated faster and be more accurate. We have identified and resolved some inconsistencies in version 2 of Pirsch.

## JSON metadata for events (v3)

This is one of the changes we're most excited about! Until now, event metadata was limited to flat key-value pairs, with both keys and values having to be strings, for example "currency" and "USD". Numbers weren't possible.

In v3, however, you can store full JSON as event metadata, including objects, numbers, and arrays. This means that you can attach an entire shopping cart to a purchase event, for example. You can also filter nested data using a JSON path such as cart.items.0.price=99 to create reports tailored to your exact requirements.

This feature is available immediately. The existing JavaScript snippets and event API v1 endpoint now support JSON. Here is an example of a snippet for an event with JSON as metadata:

```js
pirsch("Purchase", {
    meta: {
        items: [
            {id: 923, title: "Product A", price: 23.99},
            {id: 66, title: "Product B", price: 66.55},
            {id: 1236, title: "Product C", price: 7.99}
        ],
        total: 98.53,
        currency: "USD"
    }
});
```

The `duration_seconds` field will be removed in a future update. It is still available for now, but will be moved to the event metadata fields in the background.

## A New Ingestion System and Better Bot Filtering (v3)

The ingestion system filters and stores the page views and events that you send through our JavaScript snippet and the API. In v3, it has been completely overhauled. The new code is much easier to read and understand, and comes with a number of new and improved bot filters, providing you with more accurate statistics. Batch inserts and request logging have also been improved.

In a future update, you may even be able to customise the ingestion pipeline so you can add your own filters and modify the data as it is processed for you.

## A Cleaner API (v3.1)

Since day one, our API has been one of Pirsch's defining features. We developed Pirsch as an 'analytics platform', enabling you to run it in the background for your own products and clients. This approach has served many of you well, but the statistics side of the API has grown considerably over the years. Therefore, we have decided to develop a new API (/api/v2) to address this issue. Don't worry, though, your existing integrations will continue to work: v1 isn't going anywhere and will remain available indefinitely.

There are specialised API endpoints for each statistic. The new core can generate reports based on dimensions and metrics on the fly, so this is going to change significantly. Here is an example of how you might generate a report in future:

```json
{
    "site_id": "o41Sfd9",
    "period": {
        "from": "2026-06-01",
        "to": "2026-06-30",
        "timezone": "UTC"
    },
    "dimensions": {
        "day": {}
    },
    "metrics": {
        "visitors": {},
        "page_views": {},
        "sessions": {}
    },
    "order_by": [
        {
            "metric": "visitors",
            "direction": "desc"
        }
    ]
}
```

As you can see, dimensions and metrics can now be mixed and matched. Rather than having a 'referrer' endpoint or something similar, you can now request a report based on your requirements from a single API endpoint. Filters are supported, of course, and now support logical operators such as AND, OR and NOT.

A different endpoint will be used for funnels, but that's it! From 40+ endpoints down to just two!

## A Simpler, More Granular Permission Model (v3.1)

Until now, regular users and API clients were handled differently, with several layers of permissions (such as owners, account-level clients and dashboard clients).

With the new API, however, you can define roles and decide exactly which permissions each one has. These roles can then be assigned to both team members and API clients, and used to generate simple bearer tokens for API access. The complicated OAuth flow of version 2 will no longer be necessary for the new API.

## Next Steps

The release of version 3.0 is just the first step in laying the foundation for future updates. Rather than releasing a single major update, we plan to make the new features available in smaller updates over the coming months.

The next update, version 3.1, will introduce our new permission model and the new data ingestion and statistics API endpoints (/api/v2). As these are the most important endpoints, we will ensure they are implemented first. The old API is already running on the new code, so we can be sure that it has been thoroughly tested.

Versions 3.2 and 3.3 will finalise the new API and changes to the dashboard, such as a new filter mechanism for event metadata, since these now support nested JSON data.

Afterwards, we will look into adding AI and other advanced features. Our SDKs and integrations will be updated along the way.

## Conclusion

v3 takes Pirsch to the next level, setting the stage for future updates. It is not possible to cover every detail here. If you have any questions or notice any bugs, please send us an email at [support@pirsch.io](mailto:support@pirsch.io) or visit our forums. Thank you for your feedback and patience over the past few years. We hope you enjoy Pirsch v3!
