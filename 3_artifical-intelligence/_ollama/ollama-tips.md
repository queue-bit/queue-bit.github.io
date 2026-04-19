---
title:  "Ollama Tips"
intro: "A few tips for working with local AI using Ollama"
description: "A few tips for working with local AI using Ollama"
tags: "AI"
date: "2026-04-19"
---

### Run local models in Claude Code

Ollama allows you to install and run Claude Code but you will liekly need to have a larger context window than Ollama will give it by default on most hosts.

Ollama conservatively sets default context window size depending on the amount of VRAM you have, as an example, if you have 48 GiB of VRAM it gives you a 32k context window.

Ollama suggest 64k for Claude Code so you'll need to bump it up (see [Increase Context Window](#increase-context-window))


### Increase Context Window

You can increase the Context Window available to your model but this will increase the amount of VRAM it requires to run. 

In practice, if you run out of VRAM Ollama will utilize "CPU" and system memory if your context window/model is too large for the VRAM you have available - this allows it to run but comes with a performance penalty.


#### Temporarily via the CLI

On Ubuntu:

If you have Ollama running as a service, you'll need to stop it first then start it in the CLI with a context length set:

```
sudo systemctl stop ollama.service
OLLAMA_CONTEXT_LENGTH=64000 ollama serve
```

#### Permanently via a Modelfile

You'll need to create a Modelfile that defines the `num_ctx` parameter the load it into Ollama.

For example, if I wanted to create a modelfile for qwen3.5 with a 64k context I could run this in the CLI:

```
cat > Modelfile << 'EOF'
FROM qwen3.5:latest

PARAMETER num_ctx 65536
EOF
```

Then load the Modelfile:

```
ollama create qwen3.5-64k -f Modelfile
```

Now I can run the model:

```
ollama run qwen3.5-64k
```