# LLM Inference Engineer | GPU Performance × Runtime × Serving Infrastructure

> **「モデルを動かす」で終わらせず、遅い理由を特定し、実装し、実環境で効果を測る。**  
> I find where LLM inference time is actually spent, implement the improvement, and validate it end to end.

CUDA/Tritonカーネル、推論ランタイム、Kubernetes Serving、可観測性、障害復旧まで、
LLM推論システムを層をまたいで扱っています。AIアプリの機能開発よりも、
**推論性能・実行基盤・運用性を成立させる仕事**が専門です。

顧客・on-premises環境を想定した制約を技術要件へ落とし込み、
**deployment、troubleshooting、observability、recovery**まで再現可能な形で検証します。

## 代表的な成果

| 成果 | 実装・検証したこと | 証拠 |
| --- | --- | --- |
| **llama.cppへ実装をマージ** | マルチモーダル入力を含むslot save/restoreを実装。レビュー対応、テスト、ベンチマークまで完遂 | [ggml-org/llama.cpp #26640](https://github.com/ggml-org/llama.cpp/pull/26640) — 限定条件下でprompt processing **13.4×高速化** |
| **実vLLMのdecodeを改善** | Nsightでrequest windowを分解し、Qwen3.5のRMSNorm pathをCUDA/Tritonで最適化 | [CUDA Kernel Engineering](https://github.com/CHIPMUNK-T0T/cuda-kernel-engineering) — decode TPOT **約15%短縮**、94→112 tokens/s |
| **ARM64上に運用可能なLLM基盤を構築** | Windows on ARM / WSL2 / K3sで、Helm、Gateway、監視、private access、upgrade/rollback、復旧試験を実装 | [Edge LLM Platform](https://github.com/CHIPMUNK-T0T/edge-llm-cpu-arm64) — WSL復旧時のK3s API **10.5秒**、外部health **253.9秒** |

数値は記載したハードウェア・モデル・設定での結果です。一般化せず、入力、設定、
raw result、失敗条件、限界をリポジトリに残しています。

## 私の強み

### 1. 性能問題を、層をまたいで追える

GPUカーネルだけ、APIだけを見るのではなく、
**kernel → runtime → serving → infrastructure** のどこがend-to-end latencyを
支配しているかを切り分けます。局所ベンチで速くても実backendで効かなければ、
その理由までprofileで説明します。

### 2. 「速くなった」を再検証できる形にする

TTFT、TPOT/ITL、throughput、acceptance rate、memory、profiler trace、recovery timeを
目的に応じて使い分けます。成功例だけでなく、効かなかった条件やハードウェア制約も
残し、第三者が判断できる証拠にします。

### 3. 制約のある環境で、成立条件を見つける

RTX 4070 12 GB、CPU-only ARM64、Windows/WSL2、single-node K3sのような
現実の制約を隠しません。制約を前提に、再現可能な構成、運用手順、観測方法、
復旧方法まで設計します。

### 4. 調査をOSSで使われる変更まで進める

再現 → 原因分析 → design proposal → 実装 → test/benchmark → maintainer review
までつなげます。llama.cppへのmerged contributionは、手元の実験で終わらず、
既存プロジェクトの設計と品質基準に合わせて変更を届けた実績です。

## 任せられる領域

- 原因が不明なLLM推論のlatency / throughput低下の調査
- CUDA C++ / Tritonによるkernel実装と、実runtimeでの効果検証
- vLLM / llama.cpp / Ollama / SGLang周辺の推論・cache・量子化評価
- Kubernetes / K3s / Helmによるprivate serving基盤とobservability
- 顧客・edge・on-premises環境を想定した技術検証、切り分け、再現手順の作成
- upstream issue、設計提案、patch、review対応

---

## English summary

I specialize in the systems work behind LLM applications: **inference
performance, GPU kernels, runtimes, serving infrastructure, observability, and
recovery**.

My strength is connecting layers. I can start from an end-to-end latency or
throughput problem, locate the controlling bottleneck with benchmarks and
profilers, implement a focused change, and verify whether it still matters in a
real backend. I document both the result and the conditions where it does not
generalize.

### Selected evidence

- **Upstream delivery:** merged multimodal slot save/restore into
  [llama.cpp #26640](https://github.com/ggml-org/llama.cpp/pull/26640), including
  design discussion, tests, and benchmark evidence.
- **GPU-to-runtime optimization:** traced a real vLLM decode request with Nsight,
  implemented CUDA/Triton kernels, and measured **~15% lower TPOT** under the
  documented workload.
- **Constrained infrastructure:** built and recovery-tested a private CPU-only
  ARM64 LLM serving platform using Windows on ARM, WSL2, K3s, Helm, Envoy,
  Prometheus, Grafana, and Tailscale.

This work is relevant to **LLM Inference, ML Systems, GPU Performance, AI
Infrastructure, and Forward Deployed Engineering** roles.

## Core technologies

**Inference:** vLLM, llama.cpp, Ollama, SGLang, KV/prefix cache, speculative decoding, quantization  
**Performance:** CUDA C++, Triton, PyTorch extensions, Nsight Systems/Compute, TTFT, TPOT/ITL  
**Infrastructure:** Kubernetes, K3s, Helm, Envoy Gateway, Prometheus, Grafana, Tailscale  
**Platforms:** NVIDIA consumer GPUs, Windows on ARM, WSL2 Ubuntu ARM64, CPU-only edge

## OSSでの実装 / Open-source delivery

- **Merged / マージ済み:** [llama.cpp #26640 — multimodal slot save/restore](https://github.com/ggml-org/llama.cpp/pull/26640)
- **Under review / レビュー中:** [vLLM #55907 — prevent cache reuse across KV-cache layouts](https://github.com/vllm-project/vllm/pull/55907)
- **Under review / レビュー中:** [Ollama #17953 — prefill cache persistence across runner reloads](https://github.com/ollama/ollama/pull/17953)

レビュー中のPRはマージ済み実績とは分けて表示しています。

## 技術記事 / Technical writing

日本語の実装記録とベンチマークを
[Qiita (@Marron-chan)](https://qiita.com/Marron-chan)で公開しています。
