---
layout: distill
title: Transcript service with Whisper
description:
img: assets/img/1Paper-7D/radford2023robust/whisper.png
importance: 1
category: Conversational_AI
---

<!-- ## High level diagram

Overall connection diagram

{% mermaid %}
graph TB
    User[User]
    Browser[Browser]
    Frontend[Frontend]
    Backend[Backend]
    WhisperLive[WhisperLiveServer]
    TranscriptAPI[TranscriptAPI]
    OptionalLLM[OptionalLLM]
    OptionalTTS[OptionalTTS]

    User --> Browser
    Browser --> Frontend

    Frontend -->|"StreamingAudio"| Backend
    Backend -->|"AudioChunks"| WhisperLive
    WhisperLive -->|"PartialAndFinalText"| Backend
    Backend -->|"TranscriptUpdates"| Frontend

    Backend -->|"StoreAndQuery"| TranscriptAPI

    Backend -->|"Optional"| OptionalLLM
    Backend -->|"Optional"| OptionalTTS
{% endmermaid %}

I use [WhisperLive](https://github.com/collabora/WhisperLive/tree/main) as the speech-to-text (STT) engine. The main idea is to treat transcription as a streaming service: the frontend continuously sends audio chunks, while the backend returns incremental (partial) and finalized transcript segments as soon as they become available.

I deployed this service behind a reverse proxy so the browser can access it securely over HTTPS. The following diagram illustrates the deployment architecture.

{% mermaid %}
graph TB
    User[User]
    Browser[Browser]
    Nginx[NginxReverseProxy]
    Frontend[Frontend]
    Backend[Backend]
    WhisperLive[WhisperLiveServer]

    User --> Browser
    Browser --> Nginx

    Nginx -->|"RouteRoot"| Frontend
    Nginx -->|"RouteAPI"| Backend
    Nginx -->|"RouteStreaming"| Backend

    Backend -->|"InternalAudioStream"| WhisperLive
{% endmermaid %} -->

## Modules

WhisperLive provides a server/client pattern for near-live transcription, which fits well when the audio source is a browser microphone and the user expects partial updates. WhisperLive also supports multiple inference backends (e.g., CPU/GPU-optimized implementations), which makes it practical to adapt to different hardware environments without changing the overall service contract.

Operationally, a few design knobs matter a lot for a stable service: whether you load one model per session or share a single model across clients, how you cap concurrent clients and enforce connection time limits, and whether you use voice activity detection (VAD) to avoid spending compute on silence.

[Faster-Whisper](https://github.com/SYSTRAN/faster-whisper) is used as the transcription engine. It provides faster inference based on the optimization from [CTranslate2](https://github.com/OpenNMT/CTranslate2/). 

There are many other variants based on Faster-Whisper, such as [WhisperX](https://github.com/m-bain/whisperX) that integrated speaker diarization and word-level timestamps based on wav2vec2 and it's useful for online meeting transcription.

<!-- The rest of the system is mostly “glue” that makes the experience robust:

- **Frontend (browser)**: captures microphone audio, chunks it into a stream-friendly format, and renders partial transcript updates with low latency.
- **Backend (API + streaming gateway)**: manages sessions, forwards audio to the STT engine, merges partial/final results into a stable transcript, and exposes a clean API to the frontend.
- **WhisperLive STT service**: runs the model and returns incremental transcription updates.
- **Transcript API / storage (optional)**: persists transcripts, supports search, and provides replay/debugging for failure cases.

Even if the long-term goal is “conversational AI”, keeping the transcription service as a distinct module is useful: it clarifies latency budgets, makes scalability easier (separate STT autoscaling), and allows future upgrades like diarization or better punctuation without touching the rest of the stack. -->

<!-- ## Overall impression

Using WhisperLive as the transcription engine is a pragmatic choice when you want to get to a production-shaped streaming STT service quickly.

The best parts are the clear server/client abstraction and the near-live feedback loop (partial results). The main trade-offs are operational: model loading and concurrency policy, resource sizing (CPU/GPU and memory), and sensitivity to network jitter when the audio source is a browser.

In practice, I prefer keeping WhisperLive behind the backend boundary (instead of connecting the browser directly) so authentication, rate limiting, and protocol evolution stay centralized.

Future improvements that are likely worth exploring:

- **VAD policy**: reduce unnecessary inference on silence and stabilize endpointing.
- **Transcript quality**: punctuation and capitalization post-processing.
- **Diarization**: useful for meetings and multi-speaker audio.
- **Warm pools / caching**: reduce cold-start latency when new sessions connect. -->

