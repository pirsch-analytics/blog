slug = "flexible-ab-testing-on-deno-using-the-fresh-framework-and-pirsch-analytics"
title = "Flexible A/B Testing on Deno Using the Fresh Framework and Pirsch Analytics"
date = 2023-03-11
summary = "Learn how you can implement A/B testing on Deno + Fresh using Pirsch."
image = ""

[author]
name = "Marvin Blum"
image = "mb.png"
github = "Kugelschieber"
twitter = "m5blum"
---

Before we get started, I'd like to point out that we will most likely implement a more sophisticated A/B testing feature in the future. But you can do proper A/B testing today using events. In this demo, we're doing everything on the server-side, but you can do everything shown here in the browser using our JavaScript snippets.

The source code for this demo is available on [GitHub](https://github.com/pirsch-analytics/demo/tree/master/deno).

## Ordino - Your Dinosaur Shop!

We make every child's dream come true. A dinosaur shop! Not really a shop because you can't pay, but you know what I mean. Ordino is Italian and means 'I order', which I think is quite appropriate for a shop.

This is the home page.

![Home Page](/blog/static/abtesting/home.png)

As you can see, there are two dinosaurs to choose from and a form to order one or the other. If you click on one of them, you'll get a description and a larger picture. The form will pre-select the dinosaur you see on the details page.

![Details Page](/blog/static/abtesting/details.png)

Once you've chosen and ordered your dinosaur, you'll receive a confirmation.

![Form Submission](/blog/static/abtesting/form-submission.png)

So what do we care about here? Where is the A/B testing?

Well, because we do everything on the server, you can't really see it on the website. On the first visit, we define which variants the visitor will see and keep showing them in the same way. There are no in-between changes during a session.

We have four variations. The images on the home page can be swapped (A and B) and we have two titles for the order form (C and D).

![Variant A and B](/blog/static/abtesting/variant-ab.png)

![Variant C and D](/blog/static/abtesting/variant-cd.png)

Now, of course, we want to know which variations work best.

## Analyzing the Results on the Dashboard

Let's take a quick look at the dashboard.

![Dashboard Overview](/blog/static/abtesting/dashboard-overview.png)

We had three visitors today. One of them placed an order and the other two just browsed the website. Each of them created a single *A/B-Testing* event. The order was also tracked as an event.

Looking at the event metadata, we can see that we always displayed variant B for the dinosaur selection and variant C and D for the form headline.

![Selection Metadata](/blog/static/abtesting/metadata-selection.png)

![Form Metadata](/blog/static/abtesting/metadata-form.png)

Which variant is displayed is selected randomly. In this case comparing variant A and B (order of the detail page links) isn't really useful, so we'll see what we can do with the form headline (variant C and D). Of course, you need a bigger sample to make any decisions in the real world.

As we set the *A/B-Testing* event only once on the first page view, we can now click the variant we would like to filter the sessions upon. It's important to note that we now only see results were the event with that particular metadata (!) was created during the session.

![Metadata Filter](/blog/static/abtesting/filter-variant-c.png)

This returns all page views created during the session. In this case headline C didn't lead to an order. The visitors just browsed the details pages and left.

If we now add the *New Order* event to the filter (from the lense selection) and switch to variant D, we can see that we received an order.

![Order Filter](/blog/static/abtesting/filter-variant-d.png)

Two key takeaways from this are:

* Headline D (*Get your Dinosaur!*) is more effective at converting visitors to customers
* The form works better on the details page (you can tell from the exit or event page panels)

There is more we could look into. For example where the visitor came from, which browser or device was used, ... but this should be enough to give you a rough idea of how you could use this.

A simpler way to analyze the results is by viewing the metadata for the order event, as we only create that when an order is placed.

![Order Event](/blog/static/abtesting/order-event.png)

This will immediatly tell you which headline was displayed when an order is placed. If we would have more data, we could compare them site by site. Imagine having 10,000 visitors a day and 3,000 of them placed an order when variant D was displayed, while only 500 placed an order with variant C.

The *A/B-Testing* event is more useful if you would like to compare non-interactive elements on your page, like the order of the links, or a different theme color.

## Tech-Stack

*WIP*

## Implementation

*WIP*

## Conclusion

*WIP*
