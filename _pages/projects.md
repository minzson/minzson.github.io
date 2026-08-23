---
layout: single
title: "Projects"
permalink: /projects/
author_profile: true
---

Selected projects outside my day-to-day product work. My production engineering work at Samsung and KT is described on the [Work](/work/) page.

---

## Cloud and Server Starter

**Infrastructure-as-Code provisioning service** · Samsung Electronics internal engineering challenge (Team of 5) · Aug 2024 – Mar 2025

<figure>
  <img src="/images/projects/cloud-starter-overview.png" alt="Cloud and Server Starter provisioning flow">
  <figcaption>Figure 1. Provisioning flow: purpose selection → template composition → policy-compliant infrastructure in under an hour. [PLACEHOLDER]</figcaption>
</figure>

**The problem.** At a large enterprise, provisioning cloud infrastructure is slow not because the cloud is slow, but because *compliance* is: every resource must satisfy strict internal security policies, and developers without infrastructure experience routinely spent **several days** iterating with security reviews before getting a working environment.

**What we built.** A Terraform-based Infrastructure-as-Code service that provisions purpose-specific AWS/Azure infrastructure in **under 1 hour**. The core design decision: instead of teaching developers the security policies, we **embedded the policies into the templates themselves** — every template composes only pre-approved, policy-compliant resource configurations, so the fast path and the compliant path are the same path.

**My part.** I owned the **compute and load-balancing modules** of the Terraform template library — EC2, Lambda, and ELB on AWS, and their Azure equivalents. Designing for users with *no* infrastructure background forced an interesting constraint: every knob I exposed had to be safe at any setting, which meant pushing complexity down into the module rather than out into the interface.

**Recognition.** Selected for the company-wide internal engineering challenge.

---

## PeakPick

**Twitch highlight detection from chat activity** · Capstone Design Project, Sungkyunkwan University (Team of 6) · Fall 2017

<figure>
  <img src="/images/projects/peakpick-gui.png" alt="PeakPick desktop GUI">
  <figcaption>Figure 2. PeakPick desktop client: given a video ID, it returns the top-N highlight timestamps with configurable lead time.</figcaption>
</figure>

**The idea.** Long-form Twitch VODs are hours long, but the community has already annotated the best moments — in chat. PeakPick detects highlights in a VOD by analyzing **chat-activity spikes over time**, then applies **TextRank** keyword extraction to each peak segment's chat to auto-title the highlight (Python, Qt).

**My role.** I owned the **chat ingestion pipeline**: I integrated an open-source Twitch chat downloader into our tool via Python's `subprocess` module, and cut highlight-detection time from **~20 s per run** by **streaming chat logs through the shell instead of writing them to disk** first — the file-write round-trip, not the analysis, turned out to be the bottleneck.

I also contributed to the auto-titling feature (existing visualizers like Crowdcast were closed-source, so we implemented TextRank over per-peak chat text ourselves) and to the Qt Designer GUI and PeakPick logo.

Looking back, this was my first encounter with a pattern I keep meeting: the interesting engineering was not the algorithm, but **making the data path fast** — the same instinct that later drove my data-warehouse and pipeline work.
