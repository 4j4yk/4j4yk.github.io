---
date: '2025-07-17'
lastmod: '2026-09-16'
draft: false
title: 'Strawberry Aviation'
tags: ["projects", "mage-os", "e-commerce", "aem", "cloudflare", "architecture"]
summary: "An AEM aviation storefront connected to a Mage-OS commerce backend with a tested catalog fallback."
description: "A hands-on commerce project connecting an AEM front store, a small GraphQL gateway, and a Mage-OS backend."
status: "Live demo"
cover:
  image: "https://raw.githubusercontent.com/4j4yk/strawberry-aviation-aem/main/media/brand/strawberry-aviation-social.jpg"
  alt: "Aircraft undergoing maintenance inside the Strawberry Aviation hangar"
---

Strawberry Aviation has reached the point where I can call it a baseline. Not finished, not production-ready, but stable enough that I can improve it without changing the whole direction every few days.

The project is a fictional aviation supply business. Nothing in it is valid for real aviation use. I chose the domain because it gives me more interesting problems than a basic product grid: aircraft compatibility, urgent AOG requests, company purchasing, approvals, fulfillment, and an audit trail.

![Aircraft undergoing maintenance inside the Strawberry Aviation hangar](https://raw.githubusercontent.com/4j4yk/strawberry-aviation-aem/main/media/brand/strawberry-aviation-social.jpg)

## Try the project

- [AEM front store](https://aviation.ajayk.xyz/)
- [Mage-OS reference store](https://store.ajayk.xyz/)
- [AEM storefront source](https://github.com/4j4yk/strawberry-aviation-aem)

Both sites are online. The AEM storefront is currently using a dated catalog snapshot while I restore and verify the live Mage-OS connection. Browsing still works, but product actions stay disabled until the commerce path is healthy again.

## What I built

`strawberry-aviation-aem` is the front store. AEM Edge Delivery Services handles the pages and presentation. It includes blocks for the catalog, aircraft compatibility, an exploded-parts view, an AOG timeline, and a visual explanation of the architecture.

A small GraphQL gateway sits between AEM and Mage-OS. Its job is deliberately narrow: return public catalog data, limit what can be queried, and say whether the result came from Mage-OS or from the dated snapshot.

The backend is Mage-OS Minimal 3.4 running on an ARM64 Oracle VM with PHP-FPM, MariaDB, Redis, OpenSearch, nginx, and Caddy. Mage-OS owns catalog, price, inventory, customer, cart, and order data.

I have also built the aviation-specific pieces around it:

- company purchasing and role-based access
- aircraft-on-ground purchase requests
- manager approval before order creation
- fulfillment and shipment tracking
- audit history and cross-company data isolation
- catalog and compatibility services for the AEM front store

Some of those workflows passed earlier acceptance runs, but I am not treating those older results as proof of the current public deployment. The authoritative Mage-OS baseline and the version currently online need to be brought back together, then tested again.

## The architecture decision that mattered

One decision I am keeping is the failure path. If Mage-OS is offline, I do not want the AEM site to invent availability or quietly present old prices as current.

I use two explicit paths:

```text
Live:     Browser -> AEM block -> GraphQL gateway -> Mage-OS services
Fallback: Browser -> AEM block -> dated catalog snapshot -> actions disabled
```

The snapshot has a date, contains no customer or order data, and disables transactional actions. That part is working as intended today. The live path is what I am recovering.

## What comes next

Now that the shape of the system is established, the next work is less about adding features and more about making the existing path dependable end to end.

I need to restore one authoritative Mage-OS deployment, reconnect the live catalog path, and rerun the buyer and manager journey against that exact version. After that come performance traces, automated accessibility checks, backup and reset rehearsal, and the remaining credential rotation work.

The baseline gives me something useful to improve. The goal now is to tighten the connection from authored AEM content to catalog discovery, compatibility, cart, approval, order, and fulfillment, with evidence at each boundary. I will update this page as those paths move from previously tested to currently verified.

For questions about the implementation or ecommerce development work, contact `hire[at]ajayk[dot]me`.
