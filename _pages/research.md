---
layout: single
title: "Research"
permalink: /research/
author_profile: true
---

## Research Interests

I am interested in **resource management and performance predictability for containerized ML workloads** — in particular, GPU sharing and scheduling in multi-tenant clusters, and systems support for reliable ML inference serving at scale. My interest began with undergraduate research on GPU performance characterization in container environments, and has since been sharpened by my industry experience operating large-scale Kubernetes services and integrating ML inference into production pipelines at Samsung Electronics.

---

## GPU Sharing in Containered Environments

*[Analyzing GPU Performance on Containers and Characteristics of Multi-Task Scheduling](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE07614194)*

**MinJi Son**, HyunJun Kim, and HwanSoo Han · Korea Software Congress (KSC), 2018 · **First Author**

**About KSC:** Korea Software Congress (KSC) is the largest domestic computer science conference in Korea, organized by the Korean Institute of Information Scientists and Engineers (KIISE). Papers are peer-reviewed.
{: .notice--info}

**Motivation.** Containers are the de facto deployment unit for GPU workloads, yet when this work was done it was unclear how much overhead containerization adds to GPU applications, and under what conditions multiple containers can safely share a single GPU. Answering these questions is essential for scheduling decisions in shared clusters: co-locating the wrong workloads wastes hardware, while overly conservative isolation leaves GPUs underutilized.

**Approach.** I designed and led a three-part experimental study of NVIDIA Docker spanning 19 benchmarks from the Rodinia and Polybench/GPU suites, on two GPU generations — Maxwell (GTX 980 Ti) and Volta (V100). The study separately quantified (1) the overhead of the container software stack itself, (2) the behavior of concurrent kernels under MPS-based GPU sharing, and (3) device-memory constraints under container co-location.

**Key findings.**

- **Containerization overhead is a constant, not a tax on runtime.** The container software stack adds a fixed ~0.96 s regardless of workload, meaning the relative cost of GPU containerization vanishes for long-running applications.

<figure>
  <img src="/images/research/container-overhead.png" alt="Constant container overhead across benchmarks">
  <figcaption>Figure 1. Container overhead stays flat (~0.96 s) across all 19 benchmarks, independent of application runtime.</figcaption>
</figure>

- **Cache sensitivity predicts when GPU sharing helps — and when it inverts.** I devised a classification that labels a kernel *cache-sensitive* if its L1 hit rate rises by more than 10% when cache size doubles. MPS-based co-location accelerates execution until the shared cache saturates; beyond that point, performance inverts and co-location hurts. This gives a simple, measurable criterion for deciding which workloads to co-locate.

<figure>
<img src="/images/research/mps-inversion.png" alt="MPS co-location speedup and inversion point">
<figcaption>Figure 2. MPS co-location speeds up execution until cache saturation, after which the benefit inverts.</figcaption>
</figure>

- **Device memory is the hard wall for co-location.** Containers sharing a GPU hit hard device-memory limits well before compute saturates; we proposed unified memory (Pascal and later) as a mitigation path.

**Why it still matters.** Multi-tenant GPU sharing has since become a first-class problem — MPS, MIG, and time-slicing are now standard options in Kubernetes GPU scheduling — and the core question this work addressed (*which workloads can share a GPU without interference?*) remains open at cluster scale. This is precisely the direction I want to pursue in graduate school.

[Download PDF](/files/minji-son-ksc2018-gpu-containers.pdf){: .btn .btn--primary}

---

## Performance Analysis of Spark Applications

*[Performance Analysis of Spark Application through Task Execution](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE07322659)*
MinSeop Jung, DongEun Lee, **MinJi Son**, JeongHwan Park, and HwanSoo Han · Korea Software Congress (KSC), 2017

**Motivation.** Spark performance tuning was (and largely still is) guesswork: it is hard to tell which stage of a job actually dominates end-to-end time, and how that answer changes with cluster configuration and input scale.

**Approach & findings.** We developed the **Task Impact Factor (TIF)**, a metric that quantifies each RDD operation's share of end-to-end job time, and measured it across executor configurations with inputs from 25 GB to 100 GB. The analysis surfaced a counterintuitive **performance inversion**: adding cores *degrades* throughput once the input exceeds available memory. We traced the cause to JVM garbage-collection pressure — more concurrent tasks per executor means more simultaneous object churn, and GC pauses come to dominate task time.

<figure>
<img src="/images/research/spark-tif.png" alt="TIF breakdown and core-count inversion">
<figcaption>Figure 3. Per-operation TIF breakdown; beyond the memory limit, higher core counts increase GC pressure and degrade throughput.</figcaption>
</figure>

[Download PDF](/files/minji-son-ksc2017-spark-tif.pdf){: .btn .btn--primary}

---

## Current Direction

At Samsung, I integrated a multimodal ML inference service into a production content pipeline and operate Kubernetes services that absorb traffic from 1.26B devices. This experience keeps raising the same systems questions my undergraduate research began with: how should heterogeneous inference workloads share accelerators, and how can a serving system make latency predictable under multi-tenancy? These are the questions I hope to work on in graduate school.

---

## Publications

1. **MinJi Son**, HyunJun Kim, and HwanSoo Han, "[Analyzing GPU Performance on Containers and Characteristics of Multi-Task Scheduling](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE07614194)," *Korea Software Congress (KSC)*, 2018.
2. MinSeop Jung, DongEun Lee, **MinJi Son**, JeongHwan Park, and HwanSoo Han, "[Performance Analysis of Spark Application through Task Execution](https://www.dbpia.co.kr/journal/articleDetail?nodeId=NODE07322659)," *Korea Software Congress (KSC)*, 2017.