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
| 1 | Cluster config redesign (no AWS spend) — fix `cluster.yaml`: current K8s version, SSM instead of SSH, cost math | **CLOSED 2026-07-13** |
| 2 | First bring-up + teardown drill — budget alert first; create cluster, inventory everything eksctl made (CloudFormation, VPC, IAM), kube-system pod roles, live SSM shell onto node (carried from A1), delete + verify zero residue | **ISSUED 2026-07-13** |
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
- 2026-07-13 (later) — A1 review round 1: version bump to 1.35 with N-1 reasoning
  PASSED; git hygiene PASSED. Revisions needed: (a) ssh block still in cluster.yaml
  — the SSM trap untouched; (b) cost calc is a hosted screenshot, needs plain
  markdown table; (c) notes missing SSH-replacement paragraph, eksctl surprise,
  and N-1 trade-off answer; (d) typos. Assignment stays open.
- 2026-07-13 (round 2) — ssh block removed from cluster.yaml ✓, cost table now
  proper markdown ✓. Still open: notes explain why SSH was removed but never name
  SSM or how node access works now (core concept unproven); 20GB (yaml) vs 30GB
  (cost table) mismatch; eksctl surprise + N-1 deadline answer missing; "chages"
  typo (2nd flag).
- 2026-07-13 (round 3) — A1 CLOSED. Typo, 20GB consistency, and 1.35 deadline
  (27 Mar 2027) all fixed. SSM answer still one-liner and eksctl "surprise" was
  version strategy not schema — both converted to hands-on criteria in A2 rather
  than more prose loops. A2 ISSUED: budget alert → bring-up (timed) → inventory
  CFN/VPC/IAM → kube-system pod roles → live SSM session (the A1 carry-over) →
  teardown with zero-residue verification → notes/02. User deliberately keeping
  PROJECT.md unpushed for now (his call; recommended pushing for cross-device).
