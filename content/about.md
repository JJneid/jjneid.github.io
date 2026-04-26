---
title: "About"
layout: "page"
url: "/about/"
summary: "Platform and infrastructure engineer — what I'm building, the startup chapter, and career."
---

## What I'm Building Now

At Autodesk, I work on the AI/ML platform that research teams and ML engineers run on — the infrastructure between an idea and a model in production.

- **Metaflow infrastructure** — Terraform module provisioning the RDS metadata store, Metaflow UI, and metadata service; currently migrating everything to a centralized account deployment. Gives researchers and ML engineers a path to scale Python pipelines to tens of workers: retraining pipelines, batch inference, petabyte-scale data generation from proprietary CAD files. GPU capacity planning and allocation runs through the same orchestration layer.
- **Kubernetes cluster** — hosts JupyterHub, Ray, and all central platform services.
- **Docker build service** — two backends: BuildKit direct for fast iteration, and a CI pipeline backend that adds image scanning and compliance gating. Reduced container build times by 10x (from days to minutes).
- **DCV visualization VMs** — low-latency VMs accessible directly from SageMaker dev environments; researchers and ML engineers inspect CAD 3D and video model outputs without round-tripping through a separate workstation.
- **AI code review tool** — **built Autodesk's official AI code review tool from zero** using AWS Strands and GitHub MCP, deployed as an ECS service via an internal IaC SDK. Grew it until it became the official AI code review tool used across all of Autodesk engineering, then handed it over.

*Current interests: sandboxing, VM isolation, Firecracker, gVisor.*

---

## The Startup Chapter

I co-founded [slashML](https://slashml.com). The pitch: create AI applications in your private cloud. Data never leaves your premises. We got into Alchemist Accelerator (Class 37). We built things:

- An AI Data Scientist with secure code execution — deployed to 200+ users
- Secure model hosting across multiple clouds — 100+ Llama models deployed
- A tool to chat with GitHub codebases
- A full-stack AI deployment studio with GPU workspaces
- A Python SDK unifying AWS, GCP, and Azure APIs
- Technical content reaching 5,000+ monthly readers

We interviewed 300+ ML engineers and 100+ AI managers to validate the market. We benchmarked and fine-tuned specialized LLMs. We built an agent system modeled after Magentic One. We did the work.

And it didn't work out. I'm a failed startup founder. Tried B2B, tried dev tools. Nothing prepares you for this journey — not the technical skills, not the market research, not the accelerator. The thing that's hard about startups is everything at once. I'd do it differently now, but I wouldn't trade the experience.

---

## Career

**2025 – Present · Senior MLOps Engineer · Autodesk**
Finally doing the thing full time. Hosting services, building platform AI/ML features for distributed compute. Unified control plane, self-service tooling, large-scale training infrastructure. Deployment is the job now.

**2024 – 2025 · Co-Founder · slashML · Alchemist Accelerator (Class 37)**
Took the deployment obsession and tried to make it a product. Private-cloud AI deployment platform. Didn't work out, but the deployment problem was real.

**2022 – 2024 · Data Scientist · TD Bank**
50+ ML model lifecycles across multiple clouds. Rewrote and automated the entire data pipeline feeding risk models. Built no-code tools for actuaries in my free time. Same pattern — the deployment and pipeline work was what pulled me in, not the modeling.

**2019 – 2022 · ML Researcher & Engineer · Hydro Québec**
Got introduced to ML for real. Clustering algorithms that cut simulation compute by 90%, fault detection saving $1M. Published in IEEE and Energies. But getting things deployed and running reliably — that was the part that stuck with me.

**2018 – 2020 · MSc, Electrical Engineering · McGill University**
FRQNT scholarship. Graduate Excellence Award. Power systems forecasting, optimization under uncertainty.

**2014 – 2018 · BSc, Electrical & Computer Engineering · Lebanese American University · Beirut**
100% university scholarship. Constraints, optimization, math equations.

---

## Publications

- Ramos, O., Jneid, J., & Fazio, B. (2022). Non-Linear Clustering of Distribution Feeders. *Energies*, 15(21), 7883. [doi:10.3390/en15217883](https://doi.org/10.3390/en15217883)
- Golder, A., Jneid, J., Zhao, J., & Bouffard, F. (2019). Machine Learning-Based Demand and PV Power Forecasts. *IEEE Canada EPEC*.
