---
title: "How We Used Karpenter to Slash Costs and Save Engineering Time"
date: 2025-09-10
draft: false
tags: ["Kubernetes", "Karpenter", "Cloud", "AWS", "DevOps", "Autoscaling", "EKS"]
categories: ["Kubernetes", "Cloud Native", "DevOps Tools"]
author: "Francisco Meza"
showHero: true
description: "A real-world case study of how we migrated from Cluster Autoscaler to Karpenter on EKS, saving 28% on costs while simplifying cluster scaling."
---

## 🚀 Introduction

When I first heard about **Karpenter**, I was skeptical.
We’d already invested time tuning the **Cluster Autoscaler**, had spot instances in place, and swapping out a core part of our infrastructure felt risky.

But then the AWS bill landed.

And a few too many Slack messages like:

> “Why are we still scaling to r5.4xlarge for background jobs?”

So, we decided to give Karpenter a shot — and the results were way better than we expected.

---

## The Problem

We run a moderately sized **EKS cluster** that handles both long-running services and bursty background jobs.
Even with autoscaling enabled, we kept running into familiar pain points:

- ❌ Inefficient instance types being selected
- 🐌 Slower pod scheduling during peak traffic
- 💸 Over-provisioning due to rigid node group configurations
- ⚠️ Spot instance churn causing workload disruptions

Managing scaling logic was becoming a **weekly chore**, and the nodes never quite matched the workload.

---

## Why Karpenter?

Karpenter is an open-source **Kubernetes autoscaler** built by AWS.
Unlike the Cluster Autoscaler, it **provisions nodes dynamically**, skipping predefined node groups entirely.

What stood out for us:

- ✅ Works directly with the Kubernetes scheduler
- ✅ Doesn’t require Auto Scaling Groups or Launch Templates
- ✅ Supports smart instance selection (on-demand + spot)
- ✅ Scales nodes up/down within seconds

---

## What Changed

Within the **first week of rollout**, we saw real impact:

- 📉 **28% lower EC2 costs** — mostly from smarter spot instance usage
- ⚡ **2x faster pod scheduling** during bursts
- 🛠️ **Less ops overhead** — no more tweaking node group configs
- 🙂 **Happier developers** — fewer complaints about pods stuck in `Pending`

Karpenter was launching just the right instance types, with just enough resources.
No more overkill, no more lag.

---

## What We Learned

- 🔄 Karpenter **skips node groups entirely** — no ASGs or launch templates needed
- 🎯 Instance selection is **dynamic** and workload-driven
- 🚦 Multiple provisioners help isolate **spot vs. on-demand** workloads
- 👀 You still need to **monitor evictions** and spot availability by region

For bursty jobs or unpredictable traffic, Karpenter really shines.

---

## Would I Recommend It?

**Yes — 100%.**

If you’re running on EKS and still using Cluster Autoscaler, Karpenter is worth trying.
It’s not a magic bullet, but it gave us meaningful cost savings and freed up engineering time.

The cost savings were nice, but the **time saved by our team** was the real win.

---

## Further Reading

- [Karpenter Documentation](https://karpenter.sh/)
- [GitHub: Karpenter](https://github.com/aws/karpenter)
- [EKS Best Practices Guide](https://aws.github.io/aws-eks-best-practices/)
