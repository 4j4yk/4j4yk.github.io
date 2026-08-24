---
title: "Your AI Rig Can Stay Home: Using Local AI Anywhere with LM Link"
date: 2026-08-23
draft: false
tags: ["ai", "llm", "LM Studio", "local ai", "privacy", "Tailscale"]
summary: "LM Link lets the noisy, powerful computer stay home while you use its local AI models from the laptop in your bag."
---

Like everyone else, I carried my laptop (almost) everywhere with AI. It's easy for us to crank out more work with AI in the mix (setting new benchmarks of productivity, or maybe an illusion). If you are paying for AI models and using them, this article may not be for you. 

Some of us prefer local models and believe in the open source realm. We run local models and enjoy the same benefits (sort of). 

I also run local models, but when I ran a large language model, my laptop attempted to achieve flight with its fans. So I figured, is this better hardware? I might have a desktop under the desk, a home server in a closet, or a GPU machine in the cloud that I can connect to and use to offload inference from a laptop. 

[LM Link](https://lmstudio.ai/link) solved this problem. It connects those machines to LM Studio, so a model running elsewhere feels as though it is running on the same machine, much like accessing your EC2 instance via SSH. I am happy with these offerings because I have to deal with less to make it work.

## quick setup

The setup is simple:

1. Install [LM Studio](https://lmstudio.ai/download) on the computers you want to connect. For a headless server or dedicated AI rig, you can use **llmster**.
2. Sign in and request access through the [LM Link page](https://lmstudio.ai/link). Note: It is still in preview, so access is rolling out in batches.
3. Create a Link, then add your devices.
4. Download your model to the machine with the muscle.
5. Open LM Studio on your laptop or other everyday computer. The remote model should appear in the model loader next to the models stored locally.
6. Select and chat, boom !!

It behaves like another local model. Your chat remains on the device you are using, while the heavier inference work happens on the remote machine.

##  developers PoV

LM Link also works through LM Studio’s local API. If a tool already talks to LM Studio, you keep pointing it to the familiar address:

```text
http://localhost:1234
```

Codex, Claude Code, OpenCode, and applications built around LM Studio’s OpenAI-compatible API can all use the remote model this way. The model may be running across town, but your integration does not need to care.

You are not streaming an entire desktop just to reach one model. You are connecting the model itself to the tools and chat interface you already use.

The connection runs through an end-to-end encrypted mesh powered by **Tailscale**. It does not require opening your machine to the public internet, and LM Studio says only the device list reaches its backend for discovery; the conversations stay local.

That makes LM Link useful in situations:
- Your desktop has the GPU, but you love the couch.
- You want one AI rig to serve several personal devices.
- You need local-model privacy without paying or carrying separate hardware.
- You already have dev tools connected to LM Studio and do not want to rebuild flows.

“Local AI” has often meant sitting in front of the one machine capable of running it. LM Link stretches the meaning of *local*: the hardware can live elsewhere, while the model remains yours and the experience stays close to home.

It's free in preview; maybe pricing tiers will come along the way.

*Source: [LM Studio — LM Link](https://lmstudio.ai/link).*
