---
layout: single
title: "Work"
permalink: /work/
author_profile: true
---

I have spent 7 years building and operating large-scale backend infrastructure in production. This page describes that work not as a job history — my [CV](/cv/) covers that — but as the set of experiences that shaped how I approach systems problems: measure first, find the root cause across layers, and verify that every fix preserves correctness.

---

## Samsung Electronics — Samsung Messaging Platform (SMP)

**Software Engineer, Mobile eXperience** · Jul 2021 – Present

I am one of three headquarters engineers responsible for core development of the **Samsung Messaging Platform (SMP)** — a globally distributed push-notification relay infrastructure serving **1.26 billion active Galaxy devices** and relaying **600M+ push notifications daily** via FCM. Beyond hands-on development, I scope and distribute implementation work to a seven-engineer team in Vietnam.

### Diagnosing a 5–10x regression in a multi-billion-row data warehouse

SMP's audience-targeting workloads run on a multi-billion-row Amazon Redshift warehouse. When query latency degraded 5–10x — with worst-case queries timing out at 6.5 minutes — I led the diagnosis and remediation, ultimately bringing worst-case latency to **under 1 minute (7–13x improvement)**.

What made this problem interesting was that no single cause explained it. The regression emerged from **three interacting root causes across system layers**:

- **Lookup-join cardinality amplification** — a join pattern that multiplied intermediate result sizes far beyond either input table;
- **A distribution-key / join-key mismatch** — forcing full data redistribution across the MPP cluster on every join;
- **Sort-order decay on a 3.3B-row table** — which degraded zone-map pruning and led the optimizer to a **31x cardinality misestimation**, cascading into bad plan choices downstream.

The fix was equally cross-layer: I redesigned distribution and sort keys and restructured join ordering to achieve **collocated (zero-redistribution) joins**. Because these queries feed production targeting decisions, every optimization was verified to preserve result counts via execution-plan diffs before rollout.

Separately, I accelerated a nightly per-service statistics batch by **precomputing an expensive shared join as materialized views**. The interesting part was where *not* to apply it: measurement showed MV maintenance overhead actually regressed small services, so I applied MVs selectively to large services only — roughly **halving total batch time (~2.6 h → ~1.2 h)** with verified output parity.

*Why I describe this in detail:* this project was, in method if not in venue, a systems research exercise — forming hypotheses about interacting causes, isolating them experimentally, and validating that the solution preserved correctness. It is the same methodology I want to bring to graduate research.

### ML inference in the serving path

I integrated an **AI moderation service** — a pipeline combining a multimodal LLM, OCR, and object detection — into SMP's content-approval workflow. The systems challenges were about reliability, not models:

- **Asynchronous request handling**, so that inference latency (highly variable across content types) never blocks the approval pipeline;
- **Fallback-to-human routing**, so that model failures, timeouts, and low-confidence results degrade gracefully instead of dropping submissions.

In production evaluation, the pipeline **automated 87% of content-submission reviews**. Operating this integration is what turned my research interest toward inference serving: production inference is dominated by tail latency, capacity planning, and multi-tenant contention — exactly the resource-management questions I studied in undergraduate research, now at a different layer of the stack.

### Keeping autoscaling from dropping traffic

SMP's core services run on Kubernetes (EKS) and must absorb surges in device-originated and FCM relay traffic. I configured **HPA (Horizontal Pod Autoscaler)** policies for these services, and — the harder part — hardened **scale-in behavior with graceful-termination handling** so that pod removal never drops in-flight push requests. Autoscaling that loses requests on the way *down* is worse than no autoscaling; getting termination right required reasoning carefully about connection draining, shutdown ordering, and FCM retry semantics.

---

## Korea Telecom — Connected Car Platform

**Software Engineer, Connected Car Platform Development Team** · Jul 2019 – Jul 2021

- One of **two engineers owning the third-party integration layer** of a global automotive OEM's membership service in production. I designed, built, and operated backend integrations end-to-end — including API contract coordination with external providers and production incident response.
- Built full-stack administration portals for shuttle-bus operations (React, Spring Boot).

This was my first production ownership role: two engineers, a paying global customer, and no safety net. It taught me operational discipline — designing for failure, reading logs before forming theories, and treating incident response as a first-class engineering activity.

---

## Samsung Electronics — Device Solutions

**Intern** · Jul 2018 – Aug 2018

Enhanced SSD failure-analysis tooling with automated diagnostic summarization and a streamlined dump-loading process — my first exposure to how much engineering time observability tooling can save.

---

## Patents

Co-inventor on **7 patent applications** (KR/US/EP, Samsung Electronics, 2023) in on-device ML applications, including handwriting recognition and content filtering.