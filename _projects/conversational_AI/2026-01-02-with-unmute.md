---
layout: distill
title: A conversatinal bot with unmute
description:
img: assets/img/with_unmute/unmute-1.png
importance: 1
category: Conversational_AI
bibliography: 2026-01-02-conversationalBot-unmute.bib

# Optionally, you can add a table of contents to your post.
# NOTES:
#   - make sure that TOC names match the actual section names
#     for hyperlinks within the post to work correctly.
#   - we may want to automate TOC generation in the future using
#     jekyll-toc plugin (https://github.com/toshimaru/jekyll-toc).
# toc:
#   - name: D1
#     subsections:
#     - name: Motivation
#     - name: Models and tasks
#     - name: 
#   - name: D2
#     subsections:
#     - name: Zero-shot



# Below is an example of injecting additional post-specific styles.
# If you use this post as a template, delete this _styles block.
_styles: >
  .fake-img {
    background: #bbb;
    border: 1px solid rgba(0, 0, 0, 0.1);
    box-shadow: 0 0px 4px rgba(0, 0, 0, 0.1);
    margin-bottom: 12px;
  }
  .fake-img p {
    font-family: monospace;
    color: white;
    text-align: left;
    margin: 12px 0;
    text-align: center;
    font-size: 16px;
  }

---

## High level diagram

Overall connection diagram 

{% mermaid %}
graph TB
    %% User and Browser
    User["👤 User"]
    Browser["🌐 Browser<br/>Next.js Frontend<br/>Port 3000"]
    
    %% Main Backend
    Backend["⚙️ Main Backend<br/>FastAPI<br/>Port 8000"]
    
    %% Microservices
    STT["🎤 STT Service<br/>Port 8090"]
    TTS["🔊 TTS Service<br/>Port 8089"]
    LLM["🧠 LLM Service<br/>Port 8091"]
    VoiceClone["🎭 Voice Cloning<br/>Port 8092"]
    
    %% Direct Connections
    User --> Browser
    Browser -->|"HTTP GET /v1/health"| Backend
    Browser -->|"WebSocket /v1/realtime"| Backend
    
    %% Backend to Microservices
    Backend -->|WebSocket| STT
    Backend -->|WebSocket| TTS
    Backend -->|"HTTP REST"| LLM
    Backend -->|"HTTP REST"| VoiceClone
    
    %% Styling
    classDef frontend fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    classDef backend fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    classDef microservice fill:#fff3e0,stroke:#e65100,stroke-width:2px
    classDef user fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    
    class User user
    class Browser frontend
    class Backend backend
    class STT,TTS,LLM,VoiceClone microservice
{% endmermaid %}


I deployed this service on an AWS EC2 instance. To ensure external accessibility, a custom domain is configured and Nginx is set up as a reverse proxy. The following diagram illustrates the deployment architecture.

{% mermaid %}
graph TB
    %% User and Browser
    User["👤 User"]
    Browser["🌐 Browser<br/>https://IP_ADDRESS"]
    %% Nginx Reverse Proxy
    Nginx["🔀 Nginx<br/>Port 443 HTTPS<br/>IP_ADDRESS"]
    
    %% Local Services
    Frontend["🌐 Frontend<br/>Next.js<br/>localhost:3000"]
    Backend["⚙️ Backend<br/>FastAPI<br/>localhost:8000"]
    
    %% Microservices
    STT["🎤 STT Service<br/>localhost:8090"]
    TTS["🔊 TTS Service<br/>localhost:8089"]
    LLM["🧠 LLM Service<br/>localhost:8091"]
    VoiceClone["🎭 Voice Cloning<br/>localhost:8092"]
    
    %% Connections
    User --> Browser
    Browser --> Nginx
    
    %% Nginx Routing
    Nginx -->|"/" -> Frontend| Frontend
    Nginx -->|"/v1/*" -> Backend API| Backend
    Nginx -->|"/v1/realtime" -> WebSocket| Backend
    
    %% Backend to Microservices
    Backend -->|WebSocket| STT
    Backend -->|WebSocket| TTS
    Backend -->|HTTP REST| LLM
    Backend -->|HTTP REST| VoiceClone
    
    %% Styling
    classDef frontend fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    classDef backend fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    classDef microservice fill:#fff3e0,stroke:#e65100,stroke-width:2px
    classDef nginx fill:#e8f5e8,stroke:#1b5e20,stroke-width:2px
    classDef user fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    
    class User user
    class Browser,Frontend frontend
    class Backend backend
    class STT,TTS,LLM,VoiceClone microservice
    class Nginx nginx
{% endmermaid %}

## Modules

[Kyutai](https://kyutai.org/) is an interesting AI Lab that released some interesting models such [Moshi](https://arxiv.org/abs/2410.00037)<d-cite key=defossez2024moshi></d-cite>. Unlike what they has shown in Moshi, which is an end-to-end spoken dialogue model, [unmute](https://github.com/kyutai-labs/unmute) is a cascaded version that contains three modules: speech-to-text module, LLM, text-to-speech module.

In this cascaded example, the speech-to-text, text-to-speech models are tailored to the models released by Kyutai, especially the text-to-speech models is heavily fused into the backend engine which is written in Rust. The LLM is served with vLLM. To reduce latency, the text-to-speech generates tokens in a streaming fashion, which is a common approach but also may sacrifice controllability of overall sentence like intonation, emotion, etc.

Some key conversational elements like: backchannel, filler words, are not explicitly handled. The backchannel is implicitly handled by the LLM. But interruption are handled explicitly with a VAD function built inside the speech-to-text model.

## Overall impression
I've modified the unmute repo into my own version into my repo [talker](https://github.com/jianboma/talker/tree/main) (https://github.com/jianboma/talker/tree/main). 

There are still several issues to address. For example, the character personas change inconsistently during conversations, and the bot occasionally responds with nonsensical answers. Additionally, running all three models on an A10 GPU does not provide sufficient speed for smooth performance.

Despite these challenges, the system’s overall schema, particularly its approach to handling interruptions and determining when to start and stop generating speech, is well designed and brings the project close to a production-ready state.

Further improvements could focus on fine-tuning a compact LLM specifically for conversational AI, ideally with integrated tool-use capabilities to enable more agentic interactions.





