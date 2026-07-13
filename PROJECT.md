# EKS Pro — Project State

> **If you are an AI assistant (Claude, Gemini, anyone): read this file first.**
> It is the single source of truth for this project. Chat history does not survive
> across devices/sessions — this file does. Update the Progress Log at the end of
> every working session.

## What this is

A hands-on EKS deep-dive teaching project. The owner (13 yrs DevOps) builds
everything himself; the AI acts as a teacher — it assigns ONE small task at a
time with acceptance criteria and hints, then reviews the work critically.
The AI must NOT write the code/config for him unless he is stuck and asks.

Distinct from the LLM inference platform project (`D:\projects\llm-inference-platform`)
and its rebuild (`D:\projects\llm-platform-rebuild`). "EKS Pro" always means THIS repo.

Goal: interview-grade EKS depth — the "walk me through what happens when..."
level: scheduling, VPC CNI networking, identity, autoscaling, upgrades, cost.

## Ways of working

- One assignment at a time. Each has acceptance criteria + hints, never solutions.
- Review is honest and specific; notes must be in the owner's own words.
- **Cost rule: nothing left running at session end.** Every assignment that
  creates AWS resources ends with verified teardown. Design/reading work happens
  before anything touches AWS.
- Secrets/keys (`*.pem`) never live in this repo. `.gitignore` enforces it.
- Session ritual: start by reading this file; end by appending one dated line
  to the Progress Log and committing.

## Curriculum

| # | Assignment | Status |
|---|-----------|--------|
| 1 | Cluster config redesign (no AWS spend) — fix `cluster.yaml`: current K8s version, SSM instead of SSH, cost math | **ISSUED 2026-07-13** |
| 2 | First bring-up + teardown drill — create the cluster, inventory everything eksctl actually made (CloudFormation, VPC, ENIs), delete it, verify $0 left | pending |
| 3 | Workload fundamentals — Deployment/Service/probes/requests+limits; deliberately break scheduling and debug a `Pending` pod | pending |
| 4 | Networking deep dive — VPC CNI, pod IP math, prefix delegation; ALB controller + Ingress | pending |
| 5 | Identity & security — EKS Pod Identity, least-privilege pod→S3, NetworkPolicy egress control | pending |
| 6 | Autoscaling — Karpenter + HPA, spot nodes, forcing and observing scale-up | pending |
| 7 | Observability — kube-prometheus-stack, alert on unschedulable pods | pending |
| 8 | The upgrade — zero-downtime control-plane + nodegroup upgrade, PDBs, API deprecation scanning | pending |

## Progress Log

- 2026-07-13 — Project resurrected under Claude (was started with Gemini; earlier
  Claude planning happened on phone and was lost). Repo moved from
  `eks-project-gemini/eks-portfolio-project` to `D:\projects\eks-pro`; stray `.pem`
  keys moved out to `~\.ssh`; PROJECT.md + .gitignore scaffolded. State before this:
  one commit (README only), untracked `cluster.yaml` (eksctl config, K8s 1.31 —
  outdated). Assignment 1 issued.
