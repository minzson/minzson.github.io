---
permalink: /
title: "I make large-scale systems predictable"
author_profile: true
redirect_from: 
  - /about/
  - /about.html
---

I'm Minji Son, a software engineer at Samsung Electronics — one of three headquarters engineers building the **Samsung Messaging Platform (SMP)**, push-notification relay infrastructure serving 1.26 billion Galaxy devices and relaying over 600 million notifications daily. At this scale, I've cut worst-case query latency in a multi-billion-row warehouse from 6.5 minutes to under one, and kept inference-backed pipelines running through traffic surges. I care about systems whose performance you can predict, measure, and explain.

I'm applying to MS programs in computer science for Fall 2027, to work on **resource management for ML workloads on shared, containerized GPU infrastructure** — because sharing is where predictability breaks, and sharing is economically unavoidable. Concretely: GPU scheduling that contains cross-tenant interference, and inference serving that holds predictable tail latency under co-location. I first saw this problem as an undergraduate, when my experiments showed MPS-based GPU sharing accelerating co-located workloads right up to cache saturation — then inverting. Industry has since shown me the same failure mode at production scale. I want to solve it properly.


<img src="/images/journey-timeline.png" alt="Research journey: from OS memory management, through GPU sharing in containers and production systems at scale, toward graduate research on GPU scheduling for ML workloads" style="width:100%; margin: 1em 0 0.5em;">

<div class="stat-cards">
  <div class="stat-card">
    <span class="stat-num">1.26B</span>
    <span class="stat-label">active devices served by SMP</span>
  </div>
  <div class="stat-card">
    <span class="stat-num">600M+</span>
    <span class="stat-label">push notifications relayed daily</span>
  </div>
  <div class="stat-card">
    <span class="stat-num">7–13×</span>
    <span class="stat-label">worst-case query speedup<br>(6.5 min → under 1 min)</span>
  </div>
  <div class="stat-card">
    <span class="stat-num">87%</span>
    <span class="stat-label">of content reviews automated<br>by ML pipeline I integrated</span>
  </div>
  <div class="stat-card">
    <span class="stat-num">2</span>
    <span class="stat-label">peer-reviewed publications<br>(1 first-author)</span>
  </div>
</div>

## How I got here

The timeline above is one question changing layers. As an undergraduate at **Sungkyunkwan University**, I profiled Linux's zswap subsystem on real mobile devices, then spent two years in Prof. HwanSoo Han's lab characterizing **GPU performance in container environments** — first-author work (KSC 2018) showing that containerization overhead is constant rather than proportional to runtime, and that cache sensitivity predicts when MPS-based GPU sharing helps or hurts. [Read more →](/research/)

Seven years of production engineering since — from a global OEM's connected-car backend at KT to SMP at Samsung — have kept me close to the same question at ever-larger scale: diagnosing a 5–10x regression in a multi-billion-row warehouse, operating ML inference in a serving path where tail latency and multi-tenant contention dominate, and hardening Kubernetes autoscaling so scale-in never drops traffic. These are the resource-management problems I started with in the lab, and I want to spend the next years working on them properly. [Read more →](/work/)

## Publications

1. **MinJi Son**, HyunJun Kim, and HwanSoo Han, "Analyzing GPU Performance on Containers and Characteristics of Multi-Task Scheduling," *Korea Software Congress (KSC)*, 2018.
2. MinSeop Jung, DongEun Lee, **MinJi Son**, JeongHwan Park, and HwanSoo Han, "Performance Analysis of Spark Application through Task Execution," *Korea Software Congress (KSC)*, 2017.

## Elsewhere on this site

- [Research](/research/) — my research experience and where it's headed
- [Work](/work/) — seven years of production systems engineering, told as a methodology
- [Projects](/projects/) — Infrastructure-as-Code at enterprise scale, and older things I still like
- [Activities](/activities/) — teaching, research programs, and community
- [CV](/files/Minji_Son_CV.pdf) — the one-page version of all of the above

<style>
/* 카드 스타일 — 재사용하려면 assets/css/main.scss로 이동 추천 */
.stat-cards {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin: 1.2em 0 2em;
}
.stat-card {
  flex: 1 1 0;          /* 5개 균등 분할 — 한 줄 정렬 */
  min-width: 0;
  border: 1px solid #e2e8f0;
  border-radius: 10px;
  padding: 14px 10px;
  text-align: center;
  background: #fff;
}
@media (max-width: 700px) {
  .stat-card { flex: 1 1 45%; }  /* 모바일: 2열 그리드 */
}
.stat-num {
  display: block;
  font-size: 1.7em;
  font-weight: 700;
  color: #0f766e;
  line-height: 1.1;
}
.stat-label {
  display: block;
  margin-top: 6px;
  font-size: 0.72em;
  line-height: 1.35;
  color: #64748b;
}
</style>
