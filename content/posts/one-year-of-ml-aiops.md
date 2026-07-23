---
date: '2026-07-23'
draft: false
title: 'What One Year of AI Infra Looked Like'
summary: "A year of platform engineering at Autodesk, and what MLOps actually is: from Docker build services and Ray/Metaflow to the AI code review tool we shipped startup-style."
tags: ["MLOps", "Platform Engineering", "Kubernetes", "Autodesk"]
ShowToc: true
---

<figure style="margin:0 0 2.2em;max-width:760px">
<svg viewBox="0 0 760 560" width="100%" height="auto" role="img" aria-label="The MLOps iceberg: the visible tip is training and deploying a model; the large mass below the surface is scaling, scheduling, isolation, multi-tenancy, auth, and Docker builds." xmlns="http://www.w3.org/2000/svg" style="display:block;border-radius:14px">
  <defs>
    <linearGradient id="sky" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0" stop-color="#d7edf7"/>
      <stop offset="1" stop-color="#f3fafd"/>
    </linearGradient>
    <linearGradient id="ocean" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0" stop-color="#12557e"/>
      <stop offset="1" stop-color="#05263b"/>
    </linearGradient>
    <linearGradient id="tip" x1="0" y1="0" x2="0" y2="1">
      <stop offset="0" stop-color="#ffffff"/>
      <stop offset="1" stop-color="#d6ecf6"/>
    </linearGradient>
  </defs>
  <rect x="0" y="0" width="760" height="210" fill="url(#sky)"/>
  <rect x="0" y="210" width="760" height="350" fill="url(#ocean)"/>
  <polygon points="270,320 210,430 305,478 380,522 468,470 555,408 500,318 445,210 345,210" fill="#ffffff" opacity="0.16"/>
  <polygon points="345,210 305,300 380,470 445,300" fill="#ffffff" opacity="0.10"/>
  <polygon points="345,210 375,112 397,158 419,114 445,210" fill="url(#tip)" stroke="#bcdcef" stroke-width="1.5"/>
  <line x1="0" y1="210" x2="760" y2="210" stroke="#ffffff" stroke-opacity="0.55" stroke-width="2" stroke-dasharray="7 6"/>
  <text x="380" y="52" text-anchor="middle" font-family="system-ui,sans-serif" font-size="23" font-weight="700" fill="#0d3a56">🧊 What people think the job is</text>
  <text x="380" y="88" text-anchor="middle" font-family="system-ui,sans-serif" font-size="16" fill="#2a6484">train a model  →  deploy a model</text>
  <text x="380" y="240" text-anchor="middle" font-family="system-ui,sans-serif" font-size="13" font-style="italic" fill="#bfe3f2">everything below is the part you don't see</text>
  <g font-family="system-ui,sans-serif" font-size="17" fill="#eaf6fb" text-anchor="middle">
    <text x="380" y="292">Scaling one job from a single GPU to a full cluster</text>
    <text x="380" y="332">Kubernetes scheduling + compute isolation</text>
    <text x="380" y="372">Multi-tenancy and authentication</text>
    <text x="380" y="412">Self-serve Docker builds</text>
    <text x="380" y="452">ECR and IAM, dealt with once</text>
  </g>
</svg>
<figcaption style="font-size:0.85em;opacity:0.65;text-align:center;margin-top:0.6em">The MLOps iceberg: the tip is what people picture. The mass below the waterline is where the year actually went.</figcaption>
</figure>

## The one-line version

The job goes beyond giving researchers every tool they need to train and deploy models. It's whatever solutions already exist out there, plus everything they're missing. That second half is the whole job. The first half you can self-host. The second half is a little trickier, because it requires some product sense.

Users (aka researchers) are good at telling you what the problem is, aka what the missing feature is. But it's on you to figure out what to build and how to build it: how to integrate that feature into your current setup.

Here's a concrete example of "everything they're missing." We added self-serve Docker build capability to the platform. It's something that's absent from a lot of ML setups, and it turns out to be exactly the thing that bridges training and inference.

We built it after watching ML engineers set up CI pipelines and deal with ECR and IAM permissions just to move between training and inference environments. That's not exactly part of the model work; it's platform work. A platform's job is to offer this within the researcher's workflow, ideally centrally. I learned that the major piece of platform engineering is central services.

## What we hand researchers

The baseline is a Python environment to work in, a framework to train at scale (Ray), and a framework to orchestrate their pipelines (Metaflow). With just those three, a researcher can go far, mostly in scale. Researchers love compute scale. They'll use every core you give them, and they'll debug and complain loudly when something breaks.

Providing that scale is our job. Once a researcher has prototyped a model on a single GPU, they should be able to launch the big, <strong style="font-size:1.25em">expensive</strong> training job with no issues (everyone is fighting for compute). That means being good at designing the k8s system underneath: proper job scheduling, compute isolation in place, all of it invisible to them.

## The part you don't see: multi-tenancy, auth, k8s-native

A large part of the job is making all of this safe and accessible for many teams at once. That means multi-tenancy, authentication, and being Kubernetes-native underneath it all. This is the work that never shows up in a platform demo but decides whether a platform survives contact with a hundred users.

## What's next: the training vs. inference question

Everyone says inference is the future. Maybe. But it's worth remembering that behind every inference-optimized model, LLM or otherwise, is a mountain of engineering: figuring out how to extend sequence length, squeeze latency, and fit the thing into production without breaking it.

We're no longer in the business of deploying a model (traditional MLOps). We're now in the era of scaling compute. (but you already know that)

## The work I'm proudest of

During an innovation sprint, the kind where you can build anything, Ali Jahani and I decided to build a product, A-to-Z, startup style, inside Autodesk. Within a few months we 10x'd organic adoption with no top-down mandate, and it's now the official AI code review tool at the company.

We poured all our startup and dev-tooling learnings into this experiment: build a really good product, be where developers already are, make it interactive, run a support channel with a real feature-intake loop, and iterate on user feedback fast. I'm glad we got to experience product-enterprise fit.

---

*Want to join the mission? Autodesk is hiring, across the board. [See open AI/ML platform roles at Autodesk →](https://autodesk.wd1.myworkdayjobs.com/en-US/Ext?q=ai/ml&AI-ML-Platform_26WD99140-1=)*

<p style="font-size:0.8em;opacity:0.6;margin-top:2em">AI-assisted editing. AI did 0% of the thinking.</p>
