# KV / Prefix Cache & LLM Inference

KV／Prefix Cacheの効果と成立条件を中心に、ローカルLLMの推論性能や状態管理を検証しています。

vLLM・llama.cpp・Ollamaなどでさまざまな構成や手法を試し、キャッシュが効く条件・効かない条件、保存・復元、共有範囲、性能とメモリのトレードオフを調べています。計測結果は、環境・設定・手順・限界とともに公開しています。

その過程で見つけた不具合や改善点は、IssueやPull Requestを通じて各OSSへ還元しています。

## 主な検証

| テーマ | 調べていること | 公開リポジトリ |
|---|---|---|
| KV／Prefix Cacheの保存・復元 | 固定prefixの再計算と保存済みKVの復元による処理時間の違い | [ollama-prefill-kv-restore](https://github.com/ai-systems-notes/ollama-prefill-kv-restore) |
| 投機的デコーディング・量子化 | MTP／D-Flashの速度、受理率、量子化・言語・workloadによる効果の違い | [consumer-gpu-llm-bench](https://github.com/CHIPMUNK-T0T/consumer-gpu-llm-bench) |
| 制約下でのServing | CPU-only ARM64環境でのデプロイ、監視、更新・ロールバック、障害復旧 | [edge-llm-cpu-arm64](https://github.com/CHIPMUNK-T0T/edge-llm-cpu-arm64) |
| カーネルと実ランタイムの性能 | CUDA／Tritonによる最適化と、実vLLM backendで効果が残る条件 | [cuda-kernel-engineering](https://github.com/CHIPMUNK-T0T/cuda-kernel-engineering) |

## 検証からOSSへの改善

キャッシュの利用や状態の保存・復元を試す中で見つけた問題について、再現・修正・テスト・レビュー対応を行っています。

**マージ済み**

- [llama.cpp #25076](https://github.com/ggml-org/llama.cpp/pull/25076)：マルチモーダルモデルでtext-only slotの保存・復元が拒否される問題を修正
- [llama.cpp #26640](https://github.com/ggml-org/llama.cpp/pull/26640)：画像・音声入力を含むslotの保存・復元に対応
- [llama.cpp #27530](https://github.com/ggml-org/llama.cpp/pull/27530)：状態復元の失敗後に残るK/V・recurrent stateのクリーンアップを修正

**提案中・未マージ**

- [vLLM #55907](https://github.com/vllm-project/vllm/pull/55907)：異なるKVキャッシュレイアウト間でのキャッシュ再利用を防止
- [Ollama #17953](https://github.com/ollama/ollama/pull/17953)：runner再読み込みをまたぐprefillキャッシュの永続化

## 計測で重視すること

- キャッシュの有無や状態をそろえ、比較条件を明示する
- TTFT、TPOT／ITL、throughput、受理率、メモリ使用量を目的に応じて確認する
- 観察した結果と原因の仮説を分ける
- 改善が得られた条件と、効果が出なかった条件を残す
- 単体の高速化が、実際の推論処理でも有効か確認する

## English

I investigate the effects and operating conditions of KV and prefix caching in local LLM inference, including reuse, persistence, restoration, and sharing boundaries.

My experiments cover vLLM, llama.cpp, and Ollama, alongside speculative decoding, quantization, and constrained serving environments. I document configurations, measurements, and limitations, and contribute fixes or proposals upstream when these experiments reveal bugs or opportunities for improvement.

## 記事・連絡先

- [Qiita：@Marron-chan](https://qiita.com/Marron-chan) — 日本語の検証記録・技術記事
- [LinkedIn](https://www.linkedin.com/in/ryouichi-kurihara/) — 経歴・連絡先
