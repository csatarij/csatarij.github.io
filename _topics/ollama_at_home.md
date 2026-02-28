---
slug: ollama
title: ollama @ Home
updated: 2026-02-18
tags: [ai, learning]
---

My experiences running Ollama at home for coding.

## Hardware

GeForce RTX 3090 24 GB
32 GB RAM
Intel Core i7 CPU


## Network accessibility

By default, local only. To make it accessible:
```bash
sudo systemctl edit ollama.service
```
and add:
```bash
[Service]
Environment="OLLAMA_HOST=0.0.0.0"
```

## GPU computing

Enables automatically when NVIDIA driver + CUDA available. Check with:
```bash
a@b:~$ watch -n 1 nvidia-smi
+-----------------------------------------------------------------------------------------+
| NVIDIA-SMI 590.48.01              Driver Version: 590.48.01      CUDA Version: 13.1     |
+-----------------------------------------+------------------------+----------------------+
| GPU  Name                 Persistence-M | Bus-Id          Disp.A | Volatile Uncorr. ECC |
| Fan  Temp   Perf          Pwr:Usage/Cap |           Memory-Usage | GPU-Util  Compute M. |
|                                         |                        |               MIG M. |
|=========================================+========================+======================|
|   0  NVIDIA GeForce RTX 3090        Off |   00000000:01:00.0 Off |                  N/A |
| 32%   65C    P2            348W /  350W |   21774MiB /  24576MiB |     96%      Default |
|                                         |                        |                  N/A |
+-----------------------------------------+------------------------+----------------------+

+-----------------------------------------------------------------------------------------+
| Processes:                                                                              |
|  GPU   GI   CI              PID   Type   Process name                        GPU Memory |
|        ID   ID                                                               Usage      |
|=========================================================================================|
|    0   N/A  N/A            5249      C   /usr/local/bin/ollama                 21766MiB |
+-----------------------------------------------------------------------------------------+
```
```bash
a@b:~$ ollama ps
NAME                    ID              SIZE     PROCESSOR    CONTEXT    UNTIL
glm-4.7-flash:latest    d1a8a26252f1    22 GB    100% GPU     32768      2 minutes from now
```

## Context window

Started at 32k - way too low. Conversations kept going around fixing bugs, causing regressions. Also compared chat context usage with cloud models. Increased to 96k. Works better.

In opencode.jsonc:
```json
{
  "$schema": "https://opencode.ai/config.json",
  "provider": {
    "local-ollama-server": {
      "models": {
        "glm-4.7-flash": {
          "name": "glm-4.7-flash",
          "contextWindow": 98304
        },
      }
    }
  }
}
```

## Tool usage experience

Tried mistral-nemo, Qwen2.5-Coder - tool calling didn't work in OpenCode.

GLM-4.7 Flash worked excellent so far.