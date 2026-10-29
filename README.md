# Awesome-Customer-Event-Tracking

## Top Customer Event Tracking Ecosystem



**Curated List of SaaS Products & Open-Source GitHub Projects**  

*Focused on Event Pipelines, Tag Management & Self-Hosted Customer Data Platforms*  

**Last updated: October 2026**



This repository tracks notable **SaaS platforms** and **open-source projects** for **Customer Event Tracking**. These tools enable organizations to capture user interactions—page views, clicks, add-to-carts, purchases—and route that data to analytics, advertising, and warehouse destinations, forming the foundation for attribution, personalization, and product analytics.



**Examples** include Shopify Pixels, Google Tag Manager, Meta Pixel, Segment, Tealium, Elevar, Littledata, RudderStack, Amplitude Analytics, and Mixpanel Events (the category leaders).



**Open-source emphasis**: Customer Event Tracking is a domain where open-source tooling is **mature at the pipeline layer but requires assembly for commerce-specific workflows**. **Jitsu** (MIT, self-hostable) is the strongest open-source Segment alternative, collecting events from web, mobile, and server and delivering them to warehouses and SaaS tools with per-minute batching and no usage billing when self-hosted . **RudderStack Open Source** provides a production-grade CDP with a self-hosted data plane, though advanced features (SSO, multi-node scaling, audit logs) require the commercial plan . **Snowplow** offers an enterprise-grade behavioral data engine for rich event collection, and **Matomo** provides self-hosted analytics with ecommerce tracking via its HTTP API . The critical gap: **Shopify's ecosystem has no open-source equivalent to the Web Pixels API or commercial tracking apps**—Shopify replaced its GTM-style data layer with a sandboxed Web Pixels API that delivers typed events directly to registered pixels, and custom pixels are isolated from the DOM, making GTM a "not supported" implementation .



Contributions welcome! Open a PR to add/update entries. Keep descriptions factual and link to official sites.



## Table of Contents

- [SaaS/Hosted Platforms](#saas-products)

- [Open-Source GitHub Projects](#open-source-github-projects)

- [How to Contribute](#how-to-contribute)

- [Disclaimer](#disclaimer)



## SaaS/Hosted Platforms



- **[Shopify Pixels (Web Pixels API)](https://shopify.dev/docs/api/web-pixels-api)**  

  Shopify's native event tracking architecture; delivers typed ecommerce events (`product_viewed`, `checkout_started`, `checkout_completed`) directly to registered pixels without a tag-manager layer . Pixels run in an isolated sandbox with no DOM access, and customer PII is nulled for apps without approved protected-data scopes . **The mandatory path for Shopify tracking in 2026**—`checkout.liquid` and additional scripts were sunset for Plus stores in August 2025, with remaining stores auto-upgraded by August 2026 .



- **[Google Tag Manager](https://tagmanager.google.com/)**  

  Tag management system for deploying tracking tags without code changes; widely used for GA4, Meta Pixel, and other marketing tags. **On Shopify, GTM requires a custom pixel bridge** and is explicitly "not a supported implementation"—no Preview Mode, no click/scroll triggers, and no DOM access . For non-Shopify sites, GTM remains the standard tag deployment layer.



- **[Meta Pixel](https://www.facebook.com/business/tools/meta-pixel)**  

  Meta's tracking pixel for Facebook and Instagram ad optimization; captures standard events (Purchase, Lead, ViewContent, AddToCart, InitiateCheckout) and custom conversions for retargeting and audience building . Supports Conversions API for server-side event delivery when paired with the pixel.



- **[Segment](https://segment.com/)**  

  Leading customer data platform (CDP) for collecting events from web, mobile, and server and routing them to hundreds of destinations; the benchmark against which open-source alternatives (Jitsu, RudderStack) position themselves .



- **[Tealium](https://tealium.com/)**  

  Enterprise CDP with **Events, Functions, and Attributes** architecture: Events capture consented user interactions via a no-code interface, Functions provide serverless JavaScript transformation and enrichment, and Attributes maintain dynamic customer profiles updated in under 200ms . Claims 850+ enterprise customers and 1,300+ integrations .



- **[Elevar](https://www.getelevar.com/)**  

  Shopify tracking and GTM container management service; implements server-side tracking and Enhanced Ecommerce. **Caution**: when used alongside Littledata, manual audits are required to avoid double-counting events that Littledata sends server-side .



- **[Littledata](https://www.littledata.io/)**  

  Shopify tracking app focused on accurate analytics and server-side tracking; works with Google Analytics and Segment as destinations . Sends `add_to_cart` and post-checkout events server-side, bypassing browser restrictions and improving conversion data accuracy for Google Ads . **Not a general CDP**—focused on Shopify-to-GA/Segment pipelines.



- **[RudderStack](https://www.rudderstack.com/)**  

  Customer data platform with open-source and hosted options; see open-source section for self-hosted capabilities .



- **[Amplitude Analytics](https://amplitude.com/)**  

  Product analytics platform with event tracking, funnels, retention, and behavioral cohorts; requires custom instrumentation or CDP integration for event collection.



- **[Mixpanel Events](https://mixpanel.com/)**  

  Product analytics platform with event tracking, funnels, and cohort analysis; requires SDK or API instrumentation to capture events.



## Open-Source GitHub Projects



### Customer Data Platforms (Segment Alternatives)



- **[Jitsu](https://github.com/jitsucom/jitsu)**  

  The strongest open-source **Segment alternative** available (MIT, self-hostable) . Collects events from browser, mobile, and server via SDKs, HTTP API, or a **drop-in Segment proxy** for migration without touching client code. Delivers to ClickHouse, BigQuery, Snowflake, Redshift, Postgres, S3, GCS, and dozens of SaaS tools with **per-minute batching** (vs. Segment's daily/hourly warehouse loads). Features JavaScript **Functions** for per-event transformation, connector syncs (Airbyte-compatible), user identity graph, **Live Events** for real-time debugging, and an **MCP server** for AI agent configuration. Acquired by Helium Ventures (October 2026) with continued MIT licensing and no usage limits when self-hosted . **The best starting point for organizations wanting a self-hosted event pipeline with Segment-like capabilities.**



- **[RudderStack Open Source](https://github.com/rudderlabs/rudder-server)**  

  Production-grade open-source CDP with a self-hosted data plane and RudderStack-hosted control plane (recommended) . Handles event collection, transformation (up to 5 transformations in OSS), and routing to destinations. **Limitations in OSS**: no SSO, no multi-node scaling, no audit logs, no Reverse ETL (or limited), and Live Events/Event Metrics only available via the hosted control plane . **Best for teams already in the RudderStack ecosystem** or willing to use the hosted control plane.



### Behavioral Data Engines



- **[Snowplow](https://github.com/snowplow/snowplow)**  

  Enterprise-grade behavioral data engine (Scala, 6,735+ GitHub stars) for web, mobile, server-side, and webhooks; runs cloud-natively on AWS, GCP, and Azure . Provides rich event collection with structured schemas, validation, and loading to warehouses (Snowflake, Databricks, Redshift). **Heavier infrastructure** than Jitsu—requires assembling a pipeline (collector, enricher, loader) but offers the most rigorous data quality controls. Open-source Azure support via Terraform modules .



### Self-Hosted Analytics with Event Tracking



- **[Matomo](https://github.com/matomo-org/matomo)**  

  Open-source web analytics platform with full data ownership; supports server-side event tracking via its **Tracking HTTP API** with bulk POST batches up to 500 events . Ecommerce tracking requires enabling the Ecommerce feature in site settings; orders are de-duplicated by `ec_id`, and each product requires an SKU or product_id . **Best for organizations wanting self-hosted analytics with event tracking** rather than a full CDP pipeline.



### Additional Strong Open-Source Options



- **No open-source Shopify tracking app exists** — Shopify's Web Pixels API is the mandatory tracking path on Shopify , and no open-source project provides a production-ready pixel that replicates commercial apps like Elevar or Littledata. Merchants must build custom pixels or use commercial solutions.

- **Meta Pixel for WordPress (Official)** — Meta's official open-source WordPress plugin for pixel installation and Conversions API support . **WordPress-specific**—not applicable to Shopify or headless architectures.



**Frameworks for building custom systems**: For a **self-hosted Segment replacement**, Jitsu is the most complete option with per-minute batching, Segment proxy migration, and MCP support . For **enterprise-grade behavioral data with strict schemas**, Snowplow provides the most rigorous pipeline . For **self-hosted analytics with ecommerce events**, Matomo offers a simpler path . For **Shopify specifically**, no open-source tracking app exists—the Web Pixels API is the platform's supported path, and commercial apps or custom pixel development are required .



## How to Contribute



1. Fork the repo.

2. Add/edit entries in `README.md` (follow existing format).

3. Include: name, link, 1–2 sentence description, and whether it's SaaS or open-source.

4. Submit PR with a short explanation.



Star the repo if you find it useful!



## Disclaimer



- This is a **community-curated** list — not exhaustive and not an endorsement.

- Customer event tracking platforms handling user behavior and personal data must comply with applicable privacy regulations (GDPR, CCPA) and consent frameworks; Shopify's Web Pixels API nulls PII for apps without approved protected-data scopes .

- **Open-source customer event tracking is mature at the pipeline layer**—Jitsu, RudderStack OSS, and Snowplow provide production-grade event collection and routing . However, **Shopify's ecosystem has no open-source tracking equivalent**—the Web Pixels API is the mandatory path, and GTM on Shopify is "not a supported implementation" . Merchants requiring Shopify tracking should use the native Web Pixels API, commercial apps, or build custom pixels.

- Verify license terms for commercial use; Jitsu uses MIT , RudderStack OSS has open-source licensing with commercial feature gates , Snowplow uses Apache 2.0, and Matomo uses GPL.



---



**Made for analytics engineers, marketing technologists, and developers building event pipelines.**  

Let's make customer event tracking more open, but with clear eyes about the platform-specific constraints that define what's actually possible.
