---
title: "I Asked v0 to Sell Pirate Ships"
date: 2026-08-26
draft: false
tags: ["v0", "vercel", "static site", "web development", "github", "automation", "ai"]
categories: ["software engineering", "ai"]
summary: "I gave v0 a strange pirate-ship idea, got a working storefront, and then found the more interesting work hiding after the first generation."
description: "Some thoughts from building The-Wraith with v0, reviewing the generated Next.js site and deploying it through GitHub and Vercel."
keywords: ["v0 static site", "Vercel automatic deployment", "The-Wraith", "AI assisted web development"]
cover:
  image: "https://raw.githubusercontent.com/4j4yk/The-Wraith/main/public/product-ship.png"
  alt: "The-Wraith dimension-traveling pirate ship storefront"
---

I asked v0 to make a store which sells pirate ships.

Not normal pirate ships either. These ships can jump between dimensions.

I don't remember why this was the idea. Probably because another todo app would have made me close the laptop. Anyway, v0 did not question it. A little later I had a dark, dramatic storefront with ships, product details and something which looked like a checkout.

It looked surprisingly convincing.

I called it [The-Wraith](/projects/the-wraith/).

![The-Wraith dimension-traveling pirate ship storefront](https://raw.githubusercontent.com/4j4yk/The-Wraith/main/public/product-ship.png)

## Then I started clicking around

This is where the experiment became interesting for me. The first version was already a proper Next.js project. React components, TypeScript, Tailwind CSS, images and different views were all sitting in the repository. It was much further than a mockup.

At first I was mostly impressed by the speed. You describe something odd and now it exists. But after five minutes of using it, the feeling changed from *this looks cool* to *wait, why is this doing that?*

The ship specifications were present in the data but not easy to see. On a smaller screen I could not comfortably reach everything. And the checkout looked a bit too much like a real checkout.

That last one bothered me more than I expected.

The-Wraith is only a demo. It has no payment system, no real products and no reason to ask anybody for personal information. Still, the interface was borrowing the visual language of a real transaction. A person could reasonably wonder what happens after pressing the button.

So I changed it into a fictional **charter manifest**. It collects no payment or contact details and sends nothing anywhere. That fits the story better too. You don't “buy now” a dimension-jumping pirate ship. Surely there is paperwork. Maybe a suspicious captain. Possibly a curse.

I also added a small **Rift Registry** for range, crew, jump time and cannons, and fixed the mobile scrolling without disturbing the compact desktop layout.

None of these changes sound huge. They were also the difference between something generated and something I had actually thought about.

## Is this still a static site?

While doing this I had another thought. The site looks like ecommerce, but behind the costume it is mostly static information.

The products are in the code. There is no database, login, inventory service, order processing or backend API. React makes the experience interactive, but the site is not running a commerce business. It is presenting an idea.

We sometimes look at a polished interface and assume it needs a large architecture behind it. Maybe it does, but often it does not. A portfolio, event site, documentation, public resource or product showcase can look alive without acquiring six services and an operations problem.

Obviously I would not use this setup for real commerce. The moment money, identity, inventory or private data enters the picture, it becomes a different system. For fake pirate ships though, no database is probably the responsible architectural choice.

## The boring deployment part was nicely boring

After the initial v0 generation, GitHub became the place where the project made sense to me. The first generated version is there, then the product-data changes, the Rift Registry and the charter work. I can see how the thought developed instead of only seeing the final screen.

I connected the repository to Vercel, so the flow is roughly:

```text
try something -> push a branch -> see the preview -> merge when it looks right
```

A branch gets a preview deployment and the production branch updates the live site. I did not create a separate GitHub Actions workflow for this. Vercel's Git integration already handles that normal path, which is described in their [Git integration guide](https://vercel.com/docs/git).

I like that deployment became the boring part. I can spend time wondering whether a charter form feels honest instead of wondering why a server is not serving.

There is also a boundary here which I want to keep. AI agents can make a focused change, run checks and prepare it for review. Pushing or deploying still needs approval. I want help maintaining the ship, not an autonomous ship disappearing into production.

## Mostly, it gave me something to react to

I don't think the useful story is “AI built a website.” Yes, it built a lot of the first version, and very quickly.

The useful part was that I had something concrete enough to disagree with.

Why is that information hidden? Why can I not scroll here? Why does this fake form look real? Do I need a backend, or am I adding one because a product page makes me feel that I should?

Those thoughts came after the generation. Maybe that is how I will use these tools more often: get out of the blank-page stage fast, then slow down where the decisions actually matter.

The [project page](/projects/the-wraith/) has the stack and current features. The code is also on [GitHub](https://github.com/4j4yk/The-Wraith), in case you want to inspect the ship before signing any charter.
