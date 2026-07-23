---
date: '2026-07-23'
draft: false
title: 'What One Year of AI Infra Looked Like'
summary: "A year of platform engineering at Autodesk — what MLOps actually is, from Docker build services and Ray/Metaflow to the AI code review tool we shipped startup-style."
tags: ["MLOps", "Platform Engineering", "Kubernetes", "Autodesk"]
ShowToc: true
---

## The one-line version

The job goes beyond giving researchers every tool they need to train and deploy models — whatever solutions already exist out there, plus everything they're missing. That second half is the whole job. The first half you can self-host. The second half is a little trickier, because it requires some product sense.

Users — aka researchers — are good at telling you what the problem is, aka what the missing feature is. But it's on you to figure out what to build and how to build it: how to integrate that feature into your current setup.

Here's a concrete example of "everything they're missing." We added self-serve Docker build capability to the platform — something that's quietly absent from a lot of ML setups, and it turns out to be exactly the thing that bridges training and inference.

We built it after watching ML engineers lose hours — sometimes days — dealing with ECR and IAM permissions just to move between training and inference environments. That's not exactly part of the model work; it's platform work. A platform's job is to offer this within the researcher's workflow, ideally centrally. I learned that the major piece of platform engineering is central services.

## What we hand researchers

The baseline is a Python environment to work in, a framework to train at scale (Ray), and a framework to orchestrate their pipelines (Metaflow). With just those three, a researcher can go far — mostly in scale. Researchers love compute scale. They'll use every core you give them, and they'll debug and complain loudly when something breaks.

Providing that scale is our job. Once a researcher has prototyped a model on a single GPU, they should be able to launch the big, **expensive** training job with no issues. That means being good at designing the k8s system underneath — proper job scheduling, compute isolation in place, all of it invisible to them.

## The part you don't see: multi-tenancy, auth, k8s-native

A large part of the job is making all of this safe and accessible for many teams at once — multi-tenancy, authentication, and being Kubernetes-native underneath it all. This is the work that never shows up in a platform demo but decides whether a platform survives contact with a hundred users.

## What's next: the training vs. inference question

Everyone says inference is the future. Maybe. But it's worth remembering that behind every inference-optimized model — LLM or otherwise — is a mountain of engineering: figuring out how to extend sequence length, squeeze latency, and fit the thing into production without breaking it.

We're no longer in the business of deploying a model — traditional MLOps. We're now in the era of scaling compute.

## The work I'm proudest of: BeaCode

During an innovation sprint — the kind where you can build anything — Ali Jahani and I decided to build a product, A-to-Z, startup style, inside Autodesk. Within a few months we 10x'd organic adoption with no top-down mandate, and it's now the official AI code review tool at the company.

We poured all our startup and dev-tooling learnings into this experiment: build a really good product, be where developers already are, make it interactive, run a support channel with a real feature-intake loop, and iterate on user feedback fast. I'm glad we got to experience product–enterprise fit.
