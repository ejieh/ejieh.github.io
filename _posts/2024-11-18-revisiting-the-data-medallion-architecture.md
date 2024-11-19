---
layout: post
tags: data-arhitecture
---

When interviewing senior data professionals, the topic of data architecture usually comes up. More often than not, they mention working with (or building) a Medallion Data Architecture, commonly structured around *Bronze*, *Silver*, and *Gold* layers, or some derivative of this model. There are many variations of these layers that I need a copy of the periodic table to decode them sometimes — platinum, titanium, plutonium layers seem to appear out of nowhere. Some others use naming conventions like *Tier 1, 2, 3* or use labels such as *Raw, Intermediate, and Mart*. Despite the different terminologies, these all follow a **multi-hop data architecture** pattern, where data is copied and progressively transformed across layers until it's ready for consumption. Among these, the Medallion Architecture is the most popular and widely referenced.

However, there’s something missing in these conversations: **substance**. Almost every time, the discussion revolves solely around the idea of data flow across the layers with progressive data cleaning or filtering done. The narrative usually sounds like this:

> "The Bronze layer (or Stage 1, or Raw layer) is where the raw source data resides; the Silver layer is where we store the transformed data; and the Gold layer holds the data that’s ready for business consumption."

Digging in for more details about design decisions in each layer such as data structure, logical modelling, quality controls, and governance policies, often leads to rehashing the same spiel, with slight variations and perhaps an example involving a generic customer table. 

After futile attempts trying to dig in for more design patterns, I leave the conversation more curious than when it started. I wonder what assumptions are being made about data in each layer, how data is structured across the layers and what informs those choices. Also, I wonder, if a new data use case emerges (say, a product data science team wants to pull from the Silver layer), does that effectively turn the Silver layer into a Gold layer? The response I usually get is something along the lines of, *"No, in that case, we’d just create a Copper or \[insert random element] layer to accommodate that use case."*

This lack of clarity and inability to articulate modelling patterns led me to revisit the original [Medallion Data Architecture](https://www.databricks.com/glossary/medallion-architecture) as introduced by Databricks. Surprisingly (or perhaps not), the initial concept **did** include recommendations for data modelling patterns within each layer. It's quite opinionated and not loose. According to Databricks, the Silver layer should ideally follow a more normalised (3rd Normal Form) data model, while the Gold layer should leverage a Kimball-style star schema or an Inmon-style data mart.

A quick aside: I’m not sure what the author of the Databricks article meant by “Inmon-style data marts,” because in Inmon's later writings, he actually advocated for using star schema within data marts. Moving on...

Furthermore, I believe discussions on data architecture should be opinionated and have considerations for data quality and governance controls at each layer as it applies to that particular business. While the Databricks article didn’t dive deep into these areas (likely because it was more marketing-oriented than a technical deep dive), it’s worth exploring (future blog post, I guess).

By thinking about the Medallion layers (or any multi-hop pattern) not just in terms of data flow but also from a modelling and governance standpoint, we can bring much-needed clarity into our data architecture. It also helps avoid the self-inflicted complexity that often plagues data projects.

In fact, I’d go so far as to say that many data migration or transformation projects could be avoided if teams designed each data layer through multiple lenses, rather than relying solely on a flow-based mindset. When we take the time to define our data models, enforce quality standards, and implement tailored governance controls at each layer, we end up with an architecture that’s easy to understand. We also build better, more resilient data platforms that hold true in the face of evolving business requirements.

