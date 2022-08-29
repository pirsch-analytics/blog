slug = "how-to-switch-from-google-analytics"
title = "How to Switch From Google Analytics (and Keep Your Data)"
date = 2022-08-28
summary = "Google Analytics 3 is sunsetting in 2023. Learn how you can switch to a better alternative and take your data with you."
image = "ga-import.png"

[author]
name = "Daniel Schramm"
image = "ds.png"
github = "Motorschpocht"
twitter = "PirschAnalytics"
---

## Introduction

Google Analytics seems unavoidable as it currently [runs on 55.7% of all websites](https://w3techs.com/technologies/details/ta-googleanalytics), possibly also on yours. Google – the largest ad-tech company in the world – offers Google Analytics for free ([up to 10 million monthly page views](https://developers.google.com/analytics/devguides/collection/analyticsjs/limits-quotas)) because they utilize the data to target and personalize both content and ads. To achieve this, they collect a whole range of personal data, store cookies, and track users across multiple devices and websites. In return, website owners get deep insights into the behavior of their users (unless they have a script blocker installed).

As of June 2022 [France](https://www.cnil.fr/en/use-google-analytics-and-data-transfers-united-states-cnil-orders-website-manageroperator-comply), [Austria](https://gdprhub.eu/index.php?title=DSB_(Austria\)_-_2021-0.586.257_(D155.027\)), [Italy](https://www.gpdp.it/web/guest/home/docweb/-/docweb-display/docweb/9782874#english), and [the Netherlands](https://tweakers.net/nieuws/192020/autoriteit-persoonsgegevens-waarschuwt-voor-mogelijk-verbod-op-google-analytics.html) have ruled Google Analytics to be illegal as it transmits data of internet users to servers in the United States and therefore violates the GDPR. This results in liability for website owners, and it is likely that more European countries will follow.

## Google Analytics 3 is Sunsetting

In March 2022, Google announced Google Analytics 3 – also called Universal Analytics – [will stop service on July 1, 2023](https://support.google.com/analytics/answer/11583528?hl=en), and will be replaced with all-new Google Analytics 4. As the new version is not compatible with the outgoing one and there is no way of converting or importing existing data, it is recommended to export collected properties, as it will be lost from a date not specified at the time of writing.

## Switching to a Privacy-friendly Alternative

In recent years, the market for analytics solutions has been expanded by many alternatives. We started Pirsch Analytics out of our own need and designed it with simplicity and user privacy in mind. We don't collect any personal data, don't store cookies and the core is [open-source on GitHub](https://github.com/pirsch-analytics/pirsch) for everyone to see and build upon.

These days, we are collecting tens of millions of page views for our customers every month and are continuously improving and expanding our platform. All data is kept securely on our servers in Germany. Obviously, we never share anything third parties.

Our optional [backend integration](https://docs.pirsch.io/get-started/backend-integration/) allows for accurate results while not slowing down your page with scripts, and the [powerful API and numerous SDKs](https://docs.pirsch.io/api-sdks/) let you automate any tasks and even integrate Pirsch into your software.

## Google Universal Analytics Import

Version 1.16 of Pirsch introduced Google Universal Analytics import. By connecting your Google account on the settings page, you can import and convert your website properties up to the date and time Pirsch collected your first page view. Afterward, you can delete your Google Analytics account as it is no longer needed. Imported data will show up in your dashboard seamlessly.

## Conclusion

Removing Google Analytics from your website speeds up your page load, doesn't penalize your SEO ranking and you can finally get rid of that cookie banner. There's never been a better moment to re-evaluate your analytics solution.
