# LLM Systems / Inference Infrastructure Engineer

LLM推論システムを中心に、**性能計測・推論ランタイム・カーネル最適化・Serving Infrastructure・Edge Deployment**まで横断して取り組んでいます。\
主な関心領域は、**vLLM / llama.cpp / Ollama を用いたLLM推論、KV Cache / Prefix Cache、Speculative Decoding、量子化、再現可能な性能計測**です。加えて、**CUDA / Tritonによるカーネル最適化**や、**Kubernetes / K3s、Helm、Gateway、Observability、障害復旧**まで含めた推論基盤の構築・運用にも取り組んでいます。\
特に、LLM推論システムのどこで時間やリソースが使われているのかを実測し、ボトルネックを特定した上で、**Kernel Optimization / Runtime / Serving Infrastructure / Edge Deploymentをまたいで改善すること**に関心があります。

**Kernel Optimization → Inference Runtime → Serving Infrastructure → Edge Deployment**

## Focus Areas

- LLM Inference: vLLM / llama.cpp / Ollama
- KV Cache / Prefix Cache / Speculative Decoding
- Quantization / Reproducible Benchmarking
- CUDA / Triton Kernel Optimization
- Kubernetes / K3s / Helm / Observability
- ARM64 / Edge AI

## Selected Work

vLLMのdecode処理をプロファイルし、mini decoder、Attention / KV Cache、GEMV、RMSNorm、elementwise fusionなどを段階的に検証しています。\
CUDA / Tritonによるカーネル実装とend-to-end検証まで行い、実際のvLLM decode処理で**TPOTを約15%改善**するケースを確認しました。\
**Result: ~15% lower TPOT in end-to-end vLLM decode**

GPU上のLLM推論について、tokens/secだけではなく、**Prefix Cache、RadixAttention、推論条件、キャッシュ再利用**などを含めた再現可能な性能計測環境を構築しています。\
実験スクリプト、条件、測定結果を残し、性能改善だけでなく、**成立条件や制約まで検証可能な形にすること**を重視しています。

ARM64 / WSL2環境を小規模なオンプレミスAI基盤に見立て、LLM Serving Infrastructureを構築しています。\
K3s、Helm、Gateway、OpenAI / Anthropic互換API、SSE、永続ストレージ、Tailscale、Androidクライアント、監視、upgrade / rollback、障害復旧訓練まで含め、**モデルを動かすだけでなく、継続的に運用できる推論基盤**を対象にしています。

## Technical Writing / Research

LLM推論、GPU最適化、Edge AI、ローカルAIを中心に、実装・実験結果をQiitaでも公開しています。\
**Qiita:** [@Marron-chan](https://qiita.com/Marron-chan)\
研究・技術検証では、ベンチマークスコアだけに依存せず、**レイテンシ、メモリ使用量、キャッシュ挙動、量子化誤差などの直接観測可能な指標**を用いた実証的な評価を重視しています。

---

# LLM Systems / Inference Infrastructure Engineer

I work on LLM inference systems across **performance measurement, inference runtimes, kernel optimization, serving infrastructure, and edge deployment**.\
My main areas of interest include **LLM inference with vLLM / llama.cpp / Ollama, KV Cache / Prefix Cache, speculative decoding, quantization, and reproducible performance evaluation**. I also work on **CUDA / Triton kernel optimization** and inference infrastructure spanning **Kubernetes / K3s, Helm, gateways, observability, and failure recovery**.\
I am particularly interested in measuring where LLM inference systems actually spend time and resources, identifying bottlenecks, and improving systems across **Kernel Optimization / Runtime / Serving Infrastructure / Edge Deployment**.

**Kernel Optimization → Inference Runtime → Serving Infrastructure → Edge Deployment**

## Focus Areas

- LLM Inference: vLLM / llama.cpp / Ollama
- KV Cache / Prefix Cache / Speculative Decoding
- Quantization / Reproducible Benchmarking
- CUDA / Triton Kernel Optimization
- Kubernetes / K3s / Helm / Observability
- ARM64 / Edge AI

## Selected Work

I profile vLLM decode workloads and progressively evaluate mini decoder components, Attention / KV Cache, GEMV, RMSNorm, and elementwise fusion.

I implement and evaluate CUDA / Triton kernels and validate their impact end-to-end, including a case where kernel-level optimization achieved an approximately **15% reduction in TPOT in real vLLM decode workloads**.

**Result: ~15% lower TPOT in end-to-end vLLM decode**

I build reproducible environments for evaluating LLM inference on GPUs, covering not only aggregate tokens/sec but also **Prefix Cache, RadixAttention, inference conditions, and cache reuse behavior**.

I preserve experiment scripts, configurations, and measured results so that performance improvements, their **conditions, and their limitations remain reproducible and verifiable**.

I use an ARM64 / WSL2 environment as a small-scale on-premises AI platform and build an LLM serving infrastructure around it.\
The project covers K3s, Helm, gateways, OpenAI / Anthropic-compatible APIs, SSE, persistent storage, Tailscale, Android clients, observability, upgrade / rollback procedures, and recovery drills.\
The goal is not only to run a model, but to build an inference platform that can be **operated, observed, upgraded, and recovered reliably**.

## Technical Writing / Research

I publish implementation notes and experimental results on LLM inference, GPU optimization, Edge AI, and local AI on Qiita.\
**Qiita:** [@Marron-chan](https://qiita.com/Marron-chan)\
In research and technical experiments, I focus on empirical evaluation using **directly observable metrics** such as latency, memory usage, cache behavior, and quantization error rather than relying only on aggregate benchmark scores.
