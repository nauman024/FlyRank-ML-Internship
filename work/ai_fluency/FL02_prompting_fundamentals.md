# Prompting Fundamentals on Real Tasks (FL-02)

**Track:** AI Fluency 
**Target Paper Analyzed:** FlashAttention: Fast and Memory-Efficient Exact Attention with IO-Awareness (Dao et al., 2022)  
**Selected FL-01 Task:** Target Task 1 — Research Paper & Technical Documentation Synthesis  

---

## 1. Task Definition & Naive Baseline (v0)

### Selected Target Task
Synthesizing dense machine learning systems research papers and technical whitepapers into an executive, leak-free 1-page engineering brief covering problem framing, hardware memory hierarchy trade-offs, comparative complexity tables, and operational guardrails.

### Naive Prompt (v0)
> "Summarize the FlashAttention paper."

### Raw Model Output (v0)
> "The FlashAttention paper is about making transformer attention faster and using less memory. The authors found that standard attention is slow because it reads and writes intermediate matrices to GPU memory. They created a new algorithm called FlashAttention that tiles the computation and computes softmax without saving large matrices. The results show it runs much faster than standard PyTorch attention and allows training with longer context windows. It helps train large language models more efficiently."

### Notes on v0
* **What changed:** Initial naive prompt without structure or constraints.
* **What improved:** N/A (baseline).
* **What still failed:** Generic high-level summary. Lacks exact GPU memory hierarchy definitions (HBM vs. SRAM IO complexity), omits mathematical formulations (online softmax tiling), lacks specific hardware benchmarks, and has no structured schema.
* **What to try next:** Add an expert role assignment to enforce systems engineering standards.

---

## 2. Iterative Technique Ladder (v1 – v5)

---

### Version 1 (v1): Role Assignment

#### The Layer Added
**Layer:** Role & Persona Assignment

#### The Prompt (v1)
> "You are a Principal Machine Learning Systems Researcher and GPU Kernel Engineer. Summarize the FlashAttention paper for a systems engineering team."

#### Raw Model Output (v1)
> "FlashAttention addresses the memory-bandwidth bottleneck in standard Multi-Head Attention (O(N^2) memory reads/writes to GPU High Bandwidth Memory). Standard implementations are compute-bound only in theory; in practice, they are memory-bound (IO-bound).
> 
> The authors introduce an IO-aware exact attention algorithm that leverages GPU SRAM (fast on-chip cache) by fusing the softmax computation and tiling the inputs across blocks. It computes exact attention with sub-quadratic HBM accesses compared to standard accesses. This yields substantial wall-clock speedups and memory footprint reductions on Nvidia A100 GPUs."

#### Four Notes
* **What changed in prompt:** Assigned the persona of a Principal ML Systems Researcher and GPU Kernel Engineer.
* **What actually improved in output:** Shifted framing from generic speedup claims to hardware reality: identified IO/memory bandwidth bottlenecks and introduced exact memory hierarchy terms (HBM vs. SRAM).
* **What still failed:** Unstructured prose; lacks concrete baseline numbers and asymptotic complexity formulas.
* **What to try next:** Provide operational context and engineering motivation.

---

### Version 2 (v2): Context & Motivation

#### The Layer Added
**Layer:** Context & Downstream Motivation

#### The Prompt (v2)
> "You are a Principal Machine Learning Systems Researcher and GPU Kernel Engineer. Summarize the FlashAttention paper.
> 
> **Context & Motivation:** Our engineering team is evaluating whether to implement fused IO-aware attention kernels for training long-context LLMs. We need to evaluate exact IO complexity reductions, numerical stability techniques (online softmax), wall-clock speedups against PyTorch/Megatron baselines, and whether it introduces any precision trade-offs."

#### Raw Model Output (v2)
> "FlashAttention directly addresses the primary memory wall in scaling transformer context length. Standard attention materializes the N x N attention matrix to High Bandwidth Memory (HBM), causing high memory traffic.
> 
> Key technical mechanisms:
> 1. Tiling & Online Softmax: Computes softmax incrementally across blocks loaded into SRAM using scaling factors, avoiding the storage of the full N x N attention matrix.
> 2. Recomputation in Backward Pass: Recomputes attention scores in SRAM during backpropagation instead of storing them, reducing memory footprint from O(N^2) to O(N).
> 
> Hardware Impact: Exact math (no approximation error; exact match to standard attention). Achieves 2–4x speedup on standard GPT-2 and BERT training on A100 GPUs while scaling context length up to 64k tokens."

#### Four Notes
* **What changed in prompt:** Injected specific architectural context (evaluating fused kernels for long-context training) and targeted technical evaluation areas.
* **What actually improved in output:** Clarified exact mathematical mechanisms (online softmax and SRAM recomputation in backward pass) and confirmed numerical exactness.
* **What still failed:** Missing structured scannability and tabular comparison across sequence lengths.
* **What to try next:** Provide a few-shot demonstration of required extraction density.

---

### Version 3 (v3): Few-Shot Example

#### The Layer Added
**Layer:** Few-Shot Demonstration

#### The Prompt (v3)
> "You are a Principal Machine Learning Systems Researcher and GPU Kernel Engineer. Summarize the FlashAttention paper.
> 
> **Context:** Evaluating IO-aware fused kernels for transformer training pipelines.
> 
> **Example of Expected Extraction Depth:**
> - Bottleneck: Standard MHA is IO-bound; HBM bandwidth throttles Tensor Cores.
> - Algorithmic Solution: Block-level tiling over SRAM (M bytes) + Online Softmax tracking running max (m) and normalizer (l).
> - IO Complexity: Reduced from O(N d + N^2) to O(N^2 d^2 M^-1) HBM accesses.
> - Empirical Lift: 2-4x speedup on BERT-large/GPT-2; extends sequence length to 64k tokens.
> 
> Extract the target paper matching this standard of rigor."

#### Raw Model Output (v3)
> "- **Memory Wall Bottleneck:** Standard multi-head attention executes multiple memory-bound operations materializing intermediate N x N matrices in HBM, bound by memory bandwidth rather than GPU compute.
> - **Algorithmic Solution:** Fused CUDA kernel that tiles Q, K, V into on-chip SRAM, uses online softmax normalization vectors (m, l) to update attention blocks incrementally, and stores only normalization statistics for backward recomputation.
> - **IO Complexity:** Reduces memory reads/writes from O(N d + N^2) to O(N^2 d^2 M^-1) where M is SRAM size.
> - **Memory Footprint:** Drops peak attention memory from O(N^2) to O(N) linear memory.
> - **Empirical Speedups:** 15% end-to-end training speedup on BERT-large, 3x speedup on standard attention kernels, enables 64k context extension."

#### Four Notes
* **What changed in prompt:** Provided a few-shot sample illustrating dense, variable-level systems extraction.
* **What actually improved in output:** Extracted exact mathematical symbols (m, l), hardware throughput limits, and exact complexity formulas.
* **What still failed / made things worse (Honest Failure Point):** The response collapsed entirely into a terse bullet list that lost operational deployment constraints and comparative baseline tables.
* **What to try next:** Define a structured output schema with tabular data formatting.

---

### Version 4 (v4): Output Structure Specification

#### The Layer Added
**Layer:** Output Structure & Schema Specification

#### The Prompt (v4)
> "You are a Principal Machine Learning Systems Researcher and GPU Kernel Engineer. Synthesize the FlashAttention paper.
> 
> **Context:** Evaluating IO-aware attention kernels for production LLM training.
> 
> **Output Schema Required:**
> 1. **Core Problem & Hardware Bottleneck:** (1-2 concise sentences on IO complexity)
> 2. **Algorithmic Innovation & Memory Hierarchy:** (Mechanisms of SRAM tiling and online softmax)
> 3. **Comparative Evaluation Table:** (Markdown table comparing Standard Attention vs FlashAttention on IO Complexity, Memory Complexity, and Kernel Speed)
> 4. **Empirical Benchmarks & Scaling:** (Specific numbers on GPT-2/BERT and sequence length limits)
> 5. **Limitations & Hardware Constraints:** (GPU architecture limits, SRAM constraints)"

#### Raw Model Output (v4)
> "### 1. Core Problem & Hardware Bottleneck
> Standard Transformer attention is constrained by memory bandwidth rather than compute, repeatedly reading and writing O(N^2) intermediate attention matrices to high-latency GPU High Bandwidth Memory (HBM).
> 
> ### 2. Algorithmic Innovation & Memory Hierarchy
> FlashAttention computes exact attention with IO-awareness by tiling inputs into high-speed on-chip SRAM (M bytes), fusing operations into a single CUDA kernel, and maintaining numerical stability through online softmax without materializing full N x N matrices.
> 
> ### 3. Comparative Evaluation Table
> | Dimension | Standard Attention (PyTorch) | FlashAttention |
> | :--- | :--- | :--- |
> | **HBM IO Complexity** | O(N d + N^2) | O(N^2 d^2 M^-1) |
> | **Memory Footprint** | O(N^2) (quadratic) | O(N) (linear) |
> | **Numerical Exactness** | Exact | Exact (Identical outputs) |
> | **Kernel Execution** | Multi-kernel (memory-bound) | Single fused kernel (compute-bound) |
> 
> ### 4. Empirical Benchmarks & Scaling
> * **Kernel Speedup:** 2x–4x faster than native PyTorch attention kernels.
> * **End-to-End Training:** 15% speedup on BERT-large, 3x speedup on GPT-2 (1k context).
> * **Sequence Length Scaling:** Scales context length up to 64k tokens on single A100 GPUs without out-of-memory (OOM) errors.
> 
> ### 5. Limitations & Hardware Constraints
> * Tiling efficiency depends heavily on on-chip SRAM capacity (optimized specifically for Nvidia Ampere/Turing architectures).
> * Head dimension d is typically constrained due to shared memory limits."

#### Four Notes
* **What changed in prompt:** Replaced free-form text with a 5-section schema including a Markdown comparison table.
* **What actually improved in output:** Produced an executive-ready systems brief separating hardware limits, mathematical mechanisms, tabular complexity comparisons, and scaling results.
* **What still failed:** Lacked explicit step decomposition and negative verification guardrails.
* **What to try next:** Add step decomposition, verification rules, and explicit negative constraints.

---

### Version 5 (v5): Step Decomposition & Verification Checkpoints (Final Reusable Prompt)

#### The Layer Added
**Layer:** Step Decomposition & Verification Checkpoints

#### The Final Reusable Prompt
> **Role:** You are a Principal Machine Learning Systems Researcher and GPU Kernel Engineer.
> 
> **Objective:** Analyze and synthesize the provided machine learning systems research paper into an executive 1-page engineering brief.
> 
> **Context & Operational Goal:** Our engineering team needs to evaluate the hardware memory hierarchy trade-offs, algorithmic correctness, and empirical lift of this approach to decide whether to integrate it into our production training pipeline.
> 
> **Execution Steps:**
> 1. Extraction Pass: Extract the memory hierarchy bottlenecks, algorithmic tiling mechanisms, exact asymptotic IO/memory complexities, and benchmark receipts.
> 2. Verification Pass: Verify that mathematical exactness is preserved (distinguish exact methods from approximate attention), confirm hardware testbeds (e.g., A100 SRAM/HBM), and eliminate non-technical filler.
> 3. Synthesis Pass: Compile the brief using the exact markdown schema below.
> 
> **Output Structure:**
> 1. Core Problem & Hardware Bottleneck: Precise statement of the compute vs. memory bandwidth limits.
> 2. Algorithmic Innovation & Memory Mechanics: Tiling strategy, online normalization/softmax, and backward pass recomputation.
> 3. Comparative Evaluation Table: Markdown table comparing the Proposed Method vs. Standard Baselines across HBM IO Complexity, Memory Footprint, Exactness, and Runtime.
> 4. Empirical Benchmarks & Scaling Receipts: Measured speedups on standard models (BERT/GPT-2) and maximum context length reached.
> 5. Limitations & Hardware Constraints: Architecture dependencies, SRAM shared memory limits, and prohibited operational assumptions (NO-GO list).
> 
> **Guardrails:**
> - Maintain a direct, technical, receipts-driven tone. No vague marketing buzzwords.
> - Use precise systems terminology (HBM, SRAM, FLOPS, Memory-Bound vs. Compute-Bound).
> - Every claim and metric must cite exact receipts from the paper.

---

## 3. Cross-Model Evaluation: ChatGPT vs. Claude

| Evaluation Dimension | ChatGPT (GPT-5.6 Luna) | Claude (Sonnet 5) |
| :--- | :--- | :--- |
| **Tone & Style** | Rigorous and dense; structured cleanly with explicit block-size mathematical derivations (Theta(M/d)). | Extremely precise, academic, and terse; embedded algorithm proofs and citations directly into headings. |
| **Technical Accuracy** | Accurately captured online softmax running statistics (m, l), IO complexity bounds, and hardware specificities (A100 HBM vs SRAM). | Flawlessly reproduced Theorem 1 equation logic, backward-pass recomputation mechanics, and detailed baseline comparison numbers. |
| **Formatting Rigor** | Rendered the comparative table cleanly with clear markdown formatting and detailed explanatory notes underneath. | Formatted tables cleanly with strict adherence to non-approximate distinctions and isolated approximate methods from exact metrics. |
| **Failure / Weak Point** | Included slight conversational wrapper text at the start of the output. | Maintained a pure systems brief style with zero conversational filler, though slightly denser to parse visually. |

---

## 4. Final Reusable Prompt Template

> **Role:** You are a Principal Machine Learning Systems Researcher and GPU Kernel Engineer.
> 
> **Objective:** Analyze and synthesize the provided machine learning systems research paper into an executive 1-page engineering brief.
> 
> **Context & Operational Goal:** Our engineering team needs to evaluate the hardware memory hierarchy trade-offs, algorithmic correctness, and empirical lift of this approach to decide whether to integrate it into our production training pipeline.
> 
> **Execution Steps:**
> 1. **Extraction Pass:** Extract the memory hierarchy bottlenecks, algorithmic tiling mechanisms, exact asymptotic IO/memory complexities, and benchmark receipts.
> 2. **Verification Pass:** Check for temporal or cross-entity data leakage. Verify that mathematical exactness is preserved (distinguish exact methods from approximate attention), confirm hardware testbeds (e.g., A100 SRAM/HBM), and eliminate non-technical filler.
> 3. **Synthesis Pass:** Compile the brief using the exact markdown schema below.
> 
> **Output Structure:**
> 1. **Core Problem & Hardware Bottleneck:** Precise statement of the compute vs. memory bandwidth limits.
> 2. **Algorithmic Innovation & Memory Mechanics:** Tiling strategy, online normalization/softmax, and backward pass recomputation.
> 3. **Comparative Evaluation Table:** Markdown table comparing the Proposed Method vs. Standard Baselines across HBM IO Complexity, Memory Footprint, Exactness, and Runtime.
> 4. **Empirical Benchmarks & Scaling Receipts:** Measured speedups on standard models (BERT/GPT-2) and maximum context length reached.
> 5. **Limitations & Hardware Constraints:** Architecture dependencies, SRAM shared memory limits, and prohibited operational assumptions (NO-GO list).
> 
> **Guardrails:**
> - Maintain a direct, technical, receipts-driven tone. No vague marketing buzzwords.
> - Use precise systems terminology (HBM, SRAM, FLOPS, Memory-Bound vs. Compute-Bound).
> - Every claim and metric must cite exact receipts from the paper.