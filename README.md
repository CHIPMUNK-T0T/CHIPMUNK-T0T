# LLM Inference & AI Infrastructure Engineer

I build and optimize LLM systems across **inference runtimes, CUDA/Triton
kernels, Kubernetes serving, observability, and edge deployment**.

My work is measurement-driven: identify the bottleneck, change the smallest
useful layer, validate the effect end to end, and document the conditions and
limitations.

**Kernel Optimization → Inference Runtime → Serving Infrastructure → Edge Deployment**

## Selected impact

- **Merged into llama.cpp:** implemented slot save/restore for multimodal inputs
  in [ggml-org/llama.cpp#26640](https://github.com/ggml-org/llama.cpp/pull/26640).
  A bounded Qwen3.5-2B benchmark measured **13.4× faster prompt processing**
  after restore.
- **Real vLLM optimization:** profiled the decode path, implemented CUDA/Triton
  kernels, and measured approximately **15% lower TPOT** in a bounded
  end-to-end workload
  ([repository](https://github.com/CHIPMUNK-T0T/cuda-kernel-engineering)).
- **Operable ARM64 serving platform:** built a CPU-only LLM platform on Windows
  on ARM, WSL2, and K3s with Helm, Envoy, Prometheus, Grafana, private client
  access, upgrade/rollback, and measured recovery drills
  ([repository](https://github.com/CHIPMUNK-T0T/edge-llm-cpu-arm64)).

## Engineering strengths

### 1. Cross-layer LLM systems work

I can move between **GPU kernels, inference runtimes, serving APIs, and
infrastructure**. This lets me trace an end-to-end latency problem to the layer
that actually controls it instead of optimizing an isolated component.

### 2. Measurement before claims

I evaluate changes with **TTFT, TPOT/ITL, throughput, acceptance rate, memory
usage, profiler traces, and recovery time**. Benchmark inputs, configurations,
raw results, and limitations are kept together so another engineer can inspect
the conclusion.

### 3. Engineering under real constraints

I work with constraints such as a **12 GB consumer GPU, CPU-only ARM64,
Windows/WSL2, and single-node K3s**. I make the trade-offs explicit and design
for the environment that exists rather than assuming unlimited hardware.

### 4. From investigation to upstream contribution

I turn observations into minimal reproductions, design proposals, tests,
benchmarks, and reviewable changes. The merged llama.cpp contribution shows
that I can respond to maintainer feedback and carry a systems change through
upstream review.

## What I work on

- LLM inference with **vLLM, llama.cpp, Ollama, and SGLang**
- **KV Cache, Prefix Cache, speculative decoding, and quantization**
- **CUDA C++ and Triton** kernel implementation and profiling
- **Kubernetes, K3s, Helm, gateways, observability, and failure recovery**
- Reproducible evaluation of **TTFT, TPOT/ITL, throughput, memory, and cache
  behavior**
- **ARM64 and edge AI** under real hardware and operating-system constraints

## Selected projects

| Project | Engineering focus | Evidence |
| --- | --- | --- |
| [CUDA Kernel Engineering for LLM Decode](https://github.com/CHIPMUNK-T0T/cuda-kernel-engineering) | PyTorch/Triton/CUDA C++, Nsight profiling, mini-decode to real vLLM | ~15% lower TPOT under documented conditions |
| [Edge LLM Platform on ARM64](https://github.com/CHIPMUNK-T0T/edge-llm-cpu-arm64) | K3s, Helm, Envoy, Tailscale, Prometheus/Grafana, recovery | Deployment contracts and measured recovery evidence |
| [Ollama Prefill KV Restore](https://github.com/ai-systems-notes/ollama-prefill-kv-restore) | Persistent prefix-cache reuse and TTFT measurement | Reproducible benchmark and upstream design work |
| [Local LLM RAG vs CAG Benchmark](https://github.com/ai-systems-notes/local-llm-rag-cag-benchmark) | Accuracy, TTFT, and token-cost comparison | Same-model, same-hardware evaluation |

## Open-source work

I contribute findings and implementations upstream instead of keeping every
result in a standalone demo.

- [llama.cpp #26640 — multimodal slot save/restore](https://github.com/ggml-org/llama.cpp/pull/26640)
  — merged
- [llama.cpp #27942 — byte-oriented per-sequence payload design](https://github.com/ggml-org/llama.cpp/issues/27942)
- [Ollama #17247 — warm prefill cache across model unload/reload](https://github.com/ollama/ollama/issues/17247)

## Technical writing

I publish Japanese implementation notes and benchmark results on
[Qiita (@Marron-chan)](https://qiita.com/Marron-chan).

## Role interests

I am interested in **LLM Inference Engineer, ML Systems Engineer, AI
Infrastructure Engineer, GPU Performance Engineer, and Forward Deployed
Engineer** roles where measured systems work matters.

---

## 日本語

LLM推論を中心に、性能計測、推論ランタイム、CUDA/Tritonカーネル最適化、
KubernetesによるServing Infrastructure、Observability、障害復旧、
ARM64 Edge Deploymentまで横断して取り組んでいます。

単にモデルを動かすのではなく、ボトルネックを実測し、改善を実装し、
end-to-endで効果を検証し、成立条件と限界まで再現可能な形で残すことを
重視しています。

主な成果は、llama.cppへのマルチモーダルslot save/restore実装のマージ、
限定条件下での実vLLM decode TPOT約15%短縮、Windows ARM64・WSL2・K3s上の
CPU-only LLM serving基盤と復旧実測です。
