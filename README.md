# LLM Systems / Inference Infrastructure Engineer

LLM推論システムを中心に、**性能計測・推論ランタイム・カーネル最適化・Serving Infrastructure・Edge Deployment**まで横断して取り組んでいます。
主な関心領域は、**vLLM / llama.cpp / Ollama を用いたLLM推論、KV Cache / Prefix Cache、Speculative Decoding、量子化、再現可能な性能計測**です。
また、**CUDA / Tritonによるカーネル最適化**や、**Kubernetes / K3s、Helm、Gateway、Observability、障害復旧**まで含めた推論基盤の構築・運用にも取り組んでいます。
特に、LLM推論システムのどこで時間やリソースが使われているのかを実測し、ボトルネックを特定した上で、**推論ランタイムやカーネルからServing Infrastructureまでシステム全体を横断して改善すること**に関心があります。

## 主な関心領域

- LLM Inference & Performance Engineering
- vLLM / llama.cpp / Ollama
- KV Cache / Prefix Cache
- Speculative Decoding
- Quantization
- CUDA / Triton Kernel Optimization
- Reproducible Benchmarking
- Kubernetes / K3s / Helm
- AI Serving Infrastructure
- Observability / Recovery Engineering
- ARM64 / Edge AI

## 主な取り組み
### LLM推論性能最適化

vLLMを中心に、プロファイリングによるボトルネック特定、CUDA / Tritonカーネルの実装・最適化、推論性能のend-to-end検証に取り組んでいます。
`cuda-kernel-engineering` では、mini decoder、Attention / KV Cache、GEMV、RMSNorm、elementwise fusionなどを段階的に検証し、実際のvLLM decodeにおいて**TPOTを約15%改善**するケースまで確認しています。

### 再現可能なLLM性能評価

`consumer-gpu-llm-bench` では、GPU上のLLM推論について、単純なtokens/secだけではなく、Prefix Cache、RadixAttention、推論条件などを含めた再現可能な性能計測環境を構築しています。

実験条件、スクリプト、測定結果を残し、改善効果だけでなく**成立条件や制約も検証可能な形にすること**を重視しています。

### ARM64 / Edge Inference Infrastructure

`edge-llm-cpu-arm64` では、ARM64 / WSL2環境を小規模なオンプレミスAI基盤に見立て、LLM Serving Infrastructureを構築しています。

K3s、Helm、Gateway、OpenAI / Anthropic互換API、SSE、永続ストレージ、Tailscale、Androidクライアント、監視、upgrade / rollback、障害復旧訓練まで含め、**モデルを動かすだけでなく、継続的に運用できる推論基盤**を対象にしています。

## Technical Writing / Research

LLM推論、GPU最適化、Edge AI、ローカルAIを中心に、実装・実験結果をQiitaでも公開しています。
**Qiita:** `@Marron-chan`
研究・技術検証では、ベンチマークスコアだけではなく、レイテンシ、メモリ使用量、キャッシュ挙動、量子化誤差など、**直接観測可能な指標を用いた実証的な評価**に関心があります。

---

# LLM Systems / Inference Infrastructure Engineer

I work on LLM inference systems across **performance measurement, inference runtimes, kernel optimization, serving infrastructure, and edge deployment**.
My main areas of interest include **LLM inference with vLLM / llama.cpp / Ollama, KV Cache / Prefix Cache, speculative decoding, quantization, and reproducible performance evaluation**.
I also work on **CUDA / Triton kernel optimization** and inference infrastructure spanning **Kubernetes / K3s, Helm, gateways, observability, and recovery engineering**.
I am particularly interested in measuring where LLM inference systems actually spend time and resources, identifying bottlenecks, and improving the system **across layers—from inference runtimes and kernels to serving infrastructure**.

## Focus Areas

- LLM Inference & Performance Engineering
- vLLM / llama.cpp / Ollama
- KV Cache / Prefix Cache
- Speculative Decoding
- Quantization
- CUDA / Triton Kernel Optimization
- Reproducible Benchmarking
- Kubernetes / K3s / Helm
- AI Serving Infrastructure
- Observability / Recovery Engineering
- ARM64 / Edge AI

## Selected Work
### LLM Inference Performance Optimization

I work on profiling LLM inference workloads, identifying bottlenecks, implementing CUDA / Triton kernels, and validating their impact on end-to-end inference performance, primarily with vLLM.
In `cuda-kernel-engineering`, I progressively explore mini decoders, Attention / KV Cache, GEMV, RMSNorm, and elementwise fusion, including a case where kernel-level optimization resulted in an approximately **15% improvement in TPOT in real vLLM decode workloads**.

### Reproducible LLM Performance Evaluation

In `consumer-gpu-llm-bench`, I build reproducible environments for evaluating LLM inference on GPUs, including Prefix Cache, RadixAttention, and different inference conditions rather than relying only on aggregate tokens/sec.

I aim to preserve experiment configurations, scripts, and measured results so that not only performance improvements, but also their **conditions and limitations remain reproducible and verifiable**.

### ARM64 / Edge Inference Infrastructure

In `edge-llm-cpu-arm64`, I use an ARM64 / WSL2 environment as a small-scale on-premises AI platform and build an LLM serving infrastructure around it.

The project covers K3s, Helm, gateways, OpenAI / Anthropic-compatible APIs, SSE, persistent storage, Tailscale, Android clients, observability, upgrade / rollback procedures, and recovery drills.

The goal is not only to run a model, but to build an inference platform that can be **operated, observed, upgraded, and recovered reliably**.


## Technical Writing / Research

I publish implementation notes and experimental results on LLM inference, GPU optimization, Edge AI, and local AI on Qiita.
**Qiita:** `@Marron-chan`
In research and technical experiments, I am particularly interested in empirical evaluation based on **directly observable metrics** such as latency, memory usage, cache behavior, and quantization error rather than relying only on aggregate benchmark scores.
