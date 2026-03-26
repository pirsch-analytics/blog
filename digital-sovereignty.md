slug = "digital-sovereignty-in-europe-and-why-the-location-of-your-data-matters"
title = "Digital Sovereignty in Europe and Why the Location of Your Data Matters"
date = 2026-03-25
summary = ""
image = "digitalsovereignty.png"

[author]
name = "Marvin Blum"
image = "mb.png"
github = "Kugelschieber"
twitter = "m5blum"
---

AI isn't the only topic being discussed. I’m glad to see that digital sovereignty in Europe is now being discussed more, and that we're talking about how to reduce our dependence on US service providers.

Anyone running a website, managing a business or developing digital products cannot afford to ignore this issue. In this article, I'll explain why digital sovereignty is a critical issue for European businesses and website operators, and what the US CLOUD Act has to do with it. I'll also discuss why, in this context, choosing a European analytics tool like Pirsch Analytics is about far more than just technology.

A quick disclaimer: I'm not writing this article to criticise US companies. In fact, I would prefer it if there were clear regulations in place, so that we could work together more effectively. Around 30–40% of our customers are US-based, including enterprise customers that I highly value and enjoy working with.

## The US CLOUD Act

In 2018, the United States enacted the CLOUD Act (*Clarifying Lawful Overseas Use of Data Act*). It emerged in response to a legal dispute between Microsoft and the US government: Microsoft had refused to hand over customer data stored on Irish servers to US authorities. The law resolved the question clearly: in favour of US authorities.

What the CLOUD Act means in practice: **US authorities can compel American companies to disclose data, regardless of where in the world that data is stored.** Whether the servers are in Frankfurt, Dublin, or Paris makes no difference. What matters is the nationality of the provider.

This puts European companies in an awkward position. Article 48 of the EU GDPR explicitly requires that access to data by foreign authorities must go through legal assistance agreements (known as MLATs). A US service provider that complies with the CLOUD Act may be violating European data protection law, while providers complying with the GDPR might violate the CLOUD Act. It's impossible to comply with both laws as a US company, ruling them out as service providers for EU-based companies.

Also, there is no notification requirement. US authorities can access data without informing the affected individuals or European supervisory authorities.

## "European Data Centres" Don't Solve the Problem

Many US providers have responded to this by promising European customers that their data stays in Europe. AWS is building a "European Sovereign Cloud" in Brandenburg, Microsoft markets an "EU Data Boundary," Google talks about "Sovereign Controls." These offerings are well-intentioned, but they do not solve the fundamental problem.

A European data centre address does not change the legal jurisdiction. As long as the parent company is headquartered in the US and subject to US law, the CLOUD Act applies. AWS recently established a new parent company and several subsidiaries in Germany for its European Sovereign Cloud, intended to be run by EU citizens, but whether this fully neutralises the CLOUD Act remains legally unresolved.

## European Alternatives: OVH, Hetzner, and the Principle of Data Residency

Good European alternatives have been around for a while now. While we also use some US providers, such as Gmail, we have used European providers wherever possible since we launched Pirsch Analytics around five years ago. It's a shame that most companies and governments keep choosing US providers like Microsoft Windows or 365 out of convenience, or simply because they grew up with them.

Hetzner, based in Gunzenhausen, Germany, and OVH, based in France, are two of the best-known European cloud and hosting providers. Both companies operate data centres in Europe (Hetzner in Germany and Finland, and OVH primarily in France), are subject to European law and are not affected by the CLOUD Act. Many workloads do not require infrastructure spanning a hundred regions — a reliable, GDPR-compliant data centre in Germany or France is often sufficient.

We have been using Hetzner since launch. You might think it's incomplete because a specific AWS service you use is missing, but in my experience, a Docker image on a VM or a systemd service on bare metal is often sufficient. Many developers have lost the knowledge of how software can be run without vendor lock-in to specific services. It might be time to relearn these skills in order to reduce our dependence on Google Cloud, Azure or AWS. I'm not just talking about the CLOUD Act, but lean software development in general.

Not every application needs to be globally available or globally scalable. For most mid-sized businesses, agencies, freelancers, and startups in Europe, a solution that runs reliably and legally securely within Europe is far more valuable than a theoretically worldwide infrastructure with unresolved compliance questions and a blown up microservice architecture.

## European Software and Services

Beyond infrastructure, there are also high-quality European alternatives at the application level that can genuinely compete. Here are a few examples:

- **Email:** Mailbox.org, Proton Mail, Tuta as replacements for Gmail
- **Office & Collaboration:** Nextcloud, OnlyOffice, Cryptpad, instead of Microsoft 365 / Google Workspace
- **Video Conferencing:** Jitsi, BigBlueButton, instead of Zoom / Teams
- **Web Analytics:** Pirsch Analytics instead of Google Analytics (of course)

There are already plenty of success stories that hopefully inspire other users to switch too.

One recent example is the German state of Schleswig-Holstein, which planned to eliminate Microsoft entirely. Around 30,000 employees will be affected, including those working in the police force, the courts, and other institutions. They have already migrated their emails and calendars to Open-Xchange and Thunderbird, and have almost completed the migration to LibreOffice. The next step will be switching to Linux on KDE Plasma desktops, which I also use and find nice. This will save billions in licence fees.

Another notable example is the Italian Ministry of Defence. It migrated 150,000 computers to LibreOffice and selected OpenDocument Format (ODF) as its primary document format. Unlike docx, ODF is open-source, so it does not lock users into the Microsoft ecosystem. Italy has been enforcing the use of open-source software by governmental institutions since 2012.

There are more success stories. Most of these involve governments migrating to Office alternatives, but we are also seeing a shift in personal computing. This year alone, Linux reached a desktop market share of over 5% in the US for the first time — a historic high driven primarily by Microsoft's poor Windows implementation, UI/UX issues, and forced Copilot AI integration.

## What You Can Do to Become More Independent

Digital sovereignty doesn't happen overnight. But there are concrete steps that every business and website operator can take:

1. Identify critical workloads: Which data is particularly sensitive? Customer records, contracts, medical information, intellectual property? These areas should be the first to migrate to European solutions.
2. Look beyond the data centre: It is not enough to check where the servers are located. What matters is who owns the provider. A European subsidiary of a US corporation offers no genuine legal independence from the CLOUD Act.
3. Migrate step by step: Not everything at once. Web tracking is often a good starting point: replacing Google Analytics with a European tool like Pirsch Analytics is a concrete, visible step towards data sovereignty — and one less annoying cookie banner to deal with.
4. Actively support European providers: Every Euro that flows into European software companies strengthens the ecosystem. Digital sovereignty is also an economic and political choice.
5. See GDPR compliance as a competitive advantage, not a burden: Especially in B2B and regulated industries, data protection is a trust signal. Demonstrating that you handle data responsibly builds credibility with customers and partners alike.

## Our Commitment to Software Made in Europe

As mentioned in the introduction, we have been running Pirsch on German-owned servers since the beginning. We are strongly committed to European software and hope that others will follow suit, or that the regulations will become clearer or the CLOUD Act will be removed.

**Developed and hosted in Germany.** Pirsch runs on Hetzner servers in Germany. That means no US jurisdiction, no CLOUD Act exposure, no unexpected access by American authorities. Your visitors' data does not leave the EU.

**Fully GDPR-compliant.** Pirsch is compliant with GDPR, CCPA, PECR, and Schrems II. No personal data is stored, no cookies are set, and no cross-site tracking profiles are created.

**No cookie banner required.** Because Pirsch works without cookies, there is no need for the consent banner that many visitors find intrusive and that can significantly degrade the user experience on a website.

**Full transparency through open source.** The core of Pirsch is open source and publicly available on [GitHub](https://github.com/pirsch-analytics/pirsch) (now over 1,000 stars by the way, thank you!). You can verify how data is collected and processed. This is a fundamental difference from black-box solutions like Google Analytics, where what happens behind the scenes remains opaque.

## Conclusion

Europe's digital dependency on US platforms is a structural risk. It is not just a question of data protection, but of economic competitiveness, political resilience, and the trust of users.

The good news is that European alternatives exist, they are high-quality, and they are getting better all the time. Hetzner for hosting, Nextcloud for collaboration, Pirsch for web analytics...

The path to digital sovereignty starts with small steps. I hope you'll join us on it :)
