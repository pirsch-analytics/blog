slug = "how-to-create-white-labeled-web-analytics-dashboard"
title = "How to Create a White-Labeled Web Analytics Dashboard for Your Clients"
date = 2023-08-30
summary = "Learn how to create a white-labeled web analytics dashboard for your clients using Pirsch Analytics. A beginner-friendly guide to setting up a privacy-friendly Google Analytics alternative that's on brand!"
image = "pirschanalytics2.png"

[author]
name = "Daniel Schramm"
image = "ds.png"
github = "Motorschpocht"
---

## A Beginner's Guide to Wowing Your Clients with Personalized, Privacy-friendly Web Analytics

If you're a digital agency, freelancer, or anyone who manages multiple websites, you know how important it is to provide your clients with actionable, easy-to-understand analytics. But let's face it, most people find Google Analytics unintuitive and complicated.

That's why we created Pirsch Analytics—a powerful web analytics platform designed to deliver simple, privacy-aware metrics in a format you can call your own. Today, we're thrilled to show you how to set up a white-labeled web analytics dashboard using our platform.

## Why Choose Pirsch Analytics?

Before we get started, let's quickly cover why Pirsch is the way to go for your white label analytics needs. Unlike many other platforms, we offer a straightforward dashboard, easy setup, and most importantly, the freedom to make it your own. Being an developer-first web analytics solution, Pirsch is highly customizable and respects user privacy. Consider it your perfect Google Analytics alternative!

## Getting Started with Pirsch Analytics

### Step 1: Setting Up Your Dashboard

To get started, [sign up](https://pirsch.io/signup) for an account. We offer a free 30-day trial so you can try before you buy with no credit card required. After logging in for the first time, you can create a dashboard for your client's website. Enter the hostname of your website and the desired subdomain. Don't worry, we'll set up your own or your client's domain for the dashboard in a later step. In addition to the default timezone, you can also associate the domain with an organization. This is especially useful if you work in a larger team, as each member automatically gets access to new dashboards and can manage them if they have the appropriate role.

For this example, we will pretend that our company Emvi is the client and we will use our own website [emvi.com](https://emvi.com).

### Step 2: Adding Pirsch to the Website

Now that you have created your dashboard, we need to install Pirsch. You can choose between several options, but the easiest way is to copy one of the provided snippets and paste it into the head section of your website. If you use WordPress, [we have a plugin](https://wordpress.org/plugins/pirsch-analytics/) that you can install and use without any code. To avoid the risk of Pirsch being blocked by browser plugins and missing out on visitors, you can also implement it on the [server side](https://docs.pirsch.io/get-started/backend-integration), or [use a proxy](https://docs.pirsch.io/advanced/proxy) in between. Feel free to check our documentation, which explains the different options step by step. If you miss a guide for your CMS, website builder or frontend framework, please let us know!

Be sure to test the installation before proceeding. It may take a moment to see your first page views on your dashboard. If something doesn't seem to be working, we have a troubleshooting page that may help you.

For those of you who have already been using Google Analytics on your website, you can [import your data](https://docs.pirsch.io/get-started/ga-import) in just a few clicks.

### Step 3: White-Labeling the Experience

Now comes the fun part—tailoring it to match your client's brand! First off, we'll create a reusable theme. You have the flexibility to do this either for your personal account or, as we're doing here, for your entire organization.

To make the dashboard look like a seamless extension of the website, we start by matching the colors for light and dark modes. Next, we replace the default Pirsch icon with the client's logo. For an optimal look, we suggest using an SVG format and keeping the logo roughly square in shape. We'll also include the website's favicon to give everything a consistent look.

The theme code at the bottom of the page is super handy for sharing or saving your settings externally. Copy the code and paste it wherever you want. In this case, the theme code is as follows:

Ready to see your new theme in action? Simply head over to the Theme tab within the Website Dashboard Settings and select it.

To put the finishing touches on your dashboard, we recommend giving it its own domain. You can use any domain that's under your control. Typically, a subdomain like dashboard.your-client.com or analytics.your-client.com will do the trick. If you don't have direct access to your client's domain, you can use one of your own, such as your-client.your-agency.com. This adds an extra layer of professionalism and keeps everything organized. We will use analytics.emvi.com for now.

Once you've specified the domain in the settings, you'll see the essential DNS records that need to be set up. Just go to your domain host and create these records, but give it some time to take effect.

### Step 4: Sharing Their Custom Dashboard With Clients

You have plenty of options when it comes to granting your clients access to their web analytics. If your client is comfortable with it, you can easily make the dashboard public right from the settings. Alternatively, you can provide an access link. With this link, anyone can view the dashboard without needing an account or password.

Furthermore, you have the flexibility to invite people via email through the website settings. To keep things on-brand, the email will feature your current theme's logo and colors—just like the login page. Since Pirsch billing is based on the number of page views, you have the freedom to create as many websites and invite as many users as you'd like.

## And That’s It!

Here is [the end result](https://analytics.emvi.com). You're now equipped to offer a personalized, white-labeled web analytics dashboard. We're really excited to see the creative themes you come up with! Feel free to share them with us on [Twitter](https://twitter.com/PirschAnalytics) or [Discord](https://discord.gg/fAYm4Cz). Got any questions? Don't hesitate to reach out to us at [support@pirsch.io](mailto:support@pirsch.io). We're always here to help!
