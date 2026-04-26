# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Project Purpose

This is a writing project — an educational HTML article explaining the "Load balancers, service discovery, and service meshes" section from Chapter 5 ("Encoding and Evolution") of *Designing Data-Intensive Applications, 2nd Edition* (DDIA). The finished article will be deployed via GitHub Pages.

## Source Material

- `ch5.md` — full text of Chapter 5 from DDIA 2nd Edition, used as the reference/source material. The relevant section is "Load balancers, service discovery, and service meshes" (within the "Dataflow Through Services: REST and RPC" subsection).
- `draft.md` — the author's planning notes and content outline.

## Article Structure (from draft.md)

The article should flow as follows:

1. **Brief context** — formats for encoding data (comparing JSON vs. binary formats like Protobuf/Avro) to establish why encoding/evolution matters.
2. **Modes of dataflow** — how data flows between services, databases, and clients; how REST and RPC handle backward/forward compatibility.
3. **Why load balancing appears here** — during rolling upgrades, different service versions coexist. Load balancers route old clients to old service instances and new clients to new instances. This is the bridge from encoding/evolution into load balancing.
4. **Deployment strategies** (with visuals) — strategies for running multiple service versions simultaneously.
5. **Load balancing techniques** (with diagrams) — the four approaches from the book, each with tradeoffs:
   - Hardware load balancers
   - Software load balancers (NGINX, HAProxy)
   - DNS-based load balancing (with staleness caveat)
   - Service discovery systems (etcd, ZooKeeper) — dynamic registration, heartbeats, richer metadata
   - Service meshes (Istio, Linkerd) — sidecar proxy topology, mTLS, observability

## Output

The deliverable is an HTML file intended for GitHub Pages. No static site generator is configured yet — the HTML can be hand-authored or generated.
