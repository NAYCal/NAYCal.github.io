---
layout: post
title: "Reflecting on 2.5 Years at Walmart Global Tech"
summary: "Three teams, multiple 0-to-1 launches, and 1,500+ commits later: what we built across Walmart's supply chain, and the lesson about systems at scale that stuck with me."
date: 2026-10-12
tags: [Career, Distributed Systems, Data Infrastructure, Supply Chain]
---

After 2.5 years, three teams, and multiple 0-to-1 product launches at Walmart Global Tech, I am preparing to move on to the startup space. My last day is October 13.

Over this time, I contributed 120,000+ lines of code, removed 60,000+ lines, and made 1,500+ commits across production systems, opened 335 PRs, and reviewed 240 PRs across 41 repositories. My work spanned purchase order processing, inventory forecasting, inventory placement, and engineering infrastructure.

Before starting this next chapter, I wanted to reflect on what we have built, the problems we have solved, and how much I have grown as an engineer. I am incredibly grateful for the leadership, mentorship, and collaboration I have experienced at Walmart. I have had the opportunity to take projects from initial design through production, tackle difficult distributed systems problems, and work alongside people who consistently pushed me to become a better engineer.

Across Order Management Systems, Inventory Forecasting, and Inventory Placement, I worked on three teams supporting different parts of Walmart's supply chain. Here are the projects and milestones I am most proud of.

## 1. Order Management Systems: Rebuilding Purchase Order Processing

One of my first major initiatives was a ground-up reengineering of an event-driven purchase order processing system responsible for automatically closing purchase orders when appropriate.

Working with senior engineering leadership, I helped translate business requirements and new data-source integrations into a new system design, then drove the implementation of core pipeline modules and processing logic. The project involved replacing legacy processing logic with a modular architecture built around new data sources and downstream processes.

**Highlights**

- Designed and implemented core components of the new pipeline architecture, replacing legacy processing logic.
- Reworked asynchronous data flows and resolved production bugs, including issues reproducible only in batches of 10,000+ records.
- Reduced memory usage for database fetch, update, and delete operations to constant space using cursor-based access patterns, a pattern subsequently reused elsewhere.
- Improved logging, monitoring, and self-service diagnostic tooling to make production issues easier to investigate.
- Collaborated across teams to debug service-level threading issues, identify cross-service bugs, support disaster-recovery automation, and contribute to database change-data-capture pipelines.

Major performance improvements:

| Operation | Before | After |
|---|---|---|
| PostgreSQL updates | 15+ minutes | ~100 ms |
| GraphQL queries | 3–5 seconds | 1–2 seconds |
| Multithreaded dataflow evaluation | 1.5–6 seconds | ~300 ms |

This project gave me the opportunity to help rebuild a production-critical system, work through difficult concurrency and dataflow problems, and balance correctness, memory efficiency, and latency at scale.

<div class="footprint" markdown="1">
**Engineering footprint:** 31,000+ lines added, 344 commits, and over 90% test coverage.

**Technologies:** Java, Spring Boot, PostgreSQL, DB2, Cassandra, Apache Kafka, GraphQL, Kubernetes.
</div>

## 2. Inventory Forecasting: Automating Store-Level Forecast Overrides

On the Inventory Forecasting team, I worked on systems that predict safety-stock requirements for Walmart US. These predictions help determine the inventory needed to support downstream replenishment decisions.

My main 0-to-1 project was an automated pipeline for processing store-level inventory overrides, replacing a previously manual workflow with a more consistent and maintainable system. The manual process was time-consuming and error-prone. I took ownership of turning that workflow into an automated, production-ready system.

**Highlights**

- Served as lead designer and primary developer, owning the project end to end: requirements, system design, implementation, validation, and deployment.
- Built an automated pipeline to classify overrides as additions, edits, or deletions across multiple data sources.
- Developed and coordinated two Airflow workflows and eight Java jobs to process overrides at scale.
- Validated the system against expected production behavior, achieving **100% agreement with expected results** during validation.
- Partnered with cross-functional teams and business stakeholders to coordinate onboarding, document workflows, and produce handbooks for future maintainers.

The part I am most proud of is taking a business-critical workflow that depended on manual intervention and turning it into a repeatable, automated system with validated correctness.

<div class="footprint" markdown="1">
**Engineering footprint:** Millions of overrides processed per day, 10,000+ lines of code, 550 commits, and over 95% test coverage.

**Technologies:** Java, Python, Apache Spark, Apache Airflow, REST APIs, Google Cloud Platform.
</div>

## 3. Inventory Placement: Building Infrastructure for Faster Delivery

My final team focused on inventory placement: predicting where inventory should be positioned to support fulfillment and delivery needs.

One of our major initiatives was building a new forecasting platform supporting faster delivery for marketplace sellers. The platform helped the supply chain better anticipate inventory requirements and determine where inventory should be placed.

This was a challenging 0-to-1 initiative because we were developing the product and its underlying infrastructure simultaneously, with a limited window to bring the core capabilities into production.

**Highlights**

- Built a 0-to-1 third-party seller forecasting platform as part of a four-engineer team, contributing across the pipeline from initial design to production launch, including integration of 23 upstream data sources, model input preparation, and model output delivery.
- Contributed to launching model outputs and refactored DAG operations, schemas, and peak-period processing logic to support reliable production workflows.
- Worked across engineering, data science, and product to integrate upstream data sources and meet forecasting deadlines.
- Helped establish the infrastructure needed to scale the platform as the number of supported sellers grew.

This project strengthened my experience building data infrastructure for machine learning systems, particularly where upstream data availability, processing deadlines, reliability, and model requirements all need to align.

<div class="footprint" markdown="1">
**Engineering footprint:** 300+ PRs authored and merged, and 40,000+ lines of code added.

**Technologies:** Java, Python, Spring Boot, Apache Spark, Scala, Apache Airflow, cloud storage, and distributed data pipelines.
</div>

## 4. Engineering Beyond Individual Projects

Beyond these major initiatives, I also worked on reusable infrastructure and reliability improvements that helped engineers develop, test, and maintain production systems.

### A Reusable Integration-Testing Framework

I designed a reusable, configuration-driven integration-testing framework to simplify testing across multi-job data pipelines.

- Designed a framework that automatically determines job execution order using Kahn's algorithm, eliminating the need for manual dependency mapping.
- Enabled existing unit tests to be orchestrated as integration tests through a single configuration file, without requiring additional test code.
- Evaluated existing integration-testing approaches and patterns across multiple engineering teams to inform the framework's design.
- Addressed common friction points in multi-job testing, including dependency management and Spark local-run configuration.

The goal was to make integration testing easier to configure, more consistent across workflows, and more reusable across teams.

### Production Reliability and Operational Improvements

- Supported on-call investigations and production debugging across multiple services.
- Helped with data-source migrations, schema changes, and downstream compatibility.
- Fixed repository-wide timezone synchronization issues that caused discrepancies between development and production.
- Investigated concurrency, threading, and event-processing issues across service boundaries.
- Automated infrastructure scaling and configuration workflows for disaster recovery.
- Improved observability and diagnostic workflows so that engineers could investigate failures more independently.
- Shared integration-testing findings and setup guidance with engineering teams adopting the tooling, and authored handbooks to accelerate onboarding.

These projects reinforced an important lesson: good engineering is not just about making a system work. It is about understanding the environment in which that system operates and the people and processes that depend on it.

## 5. Looking Back

One of the biggest lessons I am taking away from Walmart is that building reliable systems requires understanding the entire process they support, not just the code you own.

At Walmart’s scale, a seemingly small technical decision can affect inventory availability, replenishment, and fulfillment across the supply chain. A pipeline can be correct in isolation and still fail to deliver what the business needs because an upstream source arrives late, a downstream job misses its deadline, or a failure propagates across services.

These experiences changed how I think about engineering ownership. Performance and correctness are important, but so are operational constraints, failure modes, and the dependencies between systems. Understanding how these pieces interact is essential to building software that works reliably in production.

One lesson that has stayed with me:

> At this scale, you cannot separate the technical system from the business process.

A pipeline is not just a collection of jobs, and a forecasting model is not just an output. Both are part of larger workflows with deadlines, dependencies, and people relying on the results. The challenge is not simply to make each component work, but to understand how the entire system comes together to meet the needs it was built to serve.

## Thank You

None of this work happened in isolation. I am grateful to the engineering leaders who trusted me with increasingly challenging projects, the senior and staff engineers who took the time to mentor me, the product and data science partners who helped translate business needs into technical solutions, and the teammates who made difficult problems easier to solve together.

I am especially grateful to the people who supported me throughout my time at Walmart. From late-night development cycles to countless calls working through difficult problems, these experiences made the challenging moments more rewarding and gave me plenty of memories I will carry into my next chapter.

Thank you to everyone who has been part of these past 2.5 years. I am proud of what we built together, and I will carry the lessons, friendships, and engineering experience with me into the startup space.

On to the next adventure!
