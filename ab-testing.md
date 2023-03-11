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

*WIP*

## Tech-Stack

*WIP*

## Implementation

*WIP*

## Conclusion

*WIP*
