# Portfolio Case Framing & Copy System (FL-02)
 
**Track:** AI Fluency — Week 2  

---

## 1. Voice Card

> **Voice Card:** `Direct, candid, technically precise, receipts-driven, no buzzwords.`

*Added as a standing instruction to the Claude Project workspace.*

---

## 2. Before / After Copy Contrast

* **Before (Generic AI Draft):**  
  *"Leveraged cutting-edge distributed computing paradigms and advanced deep learning frameworks to drive high-impact artificial intelligence solutions, maximizing throughput and optimizing synergistic workflows across multimodal pipelines."*
* **After (Edited & Grounded):**  
  *"I split LLM tensor weights across two commodity laptops over a local Ethernet switch using `exo` to run un-quantized 8B inference without buying server-grade GPUs."*

---

## 3. Framed Case Studies (The Three Beats)

### Case Study 1: Distributed Multi-Node LLM Inference Cluster

* **Beat 1: The Problem**  
  Running larger open-weight models locally hits immediate single-device VRAM and memory-bandwidth walls. Renting cloud GPUs for every local test is expensive, while standard quantization often degrades generation quality on specialized evaluation tasks.
* **Beat 2: What I Did & Decided**  
  I built a two-node local compute cluster linking an Intel Core i5 laptop and a secondary node over local Ethernet. Using `exo`, Docker, and WSL, I sharded tensor layers across both machines with dynamic layer assignment rather than standard round-robin routing. I prioritized memory locality and minimal network serialization over complex pipeline scheduling.
* **Beat 3: What Came of It (Receipts)**  
  Successfully ran distributed inference on models exceeding single-machine RAM limits at a consistent, usable token generation rate over a standard local subnet without hardware upgrades or cloud bills.

---

### Case Study 2: Real-Time Edge Vision & Navigation System

* **Beat 1: The Problem**  
  Standard computer vision object detection models provide bounding boxes but lack depth context and spatial urgency required for immediate, real-world physical assistive navigation under constrained edge hardware.
* **Beat 2: What I Did & Decided**  
  Engineered a real-time perception pipeline utilizing YOLOv8 and monocular depth heuristics to compute directional distance zones. I chose lightweight bounding-box spatial clustering over heavy 3D point cloud reconstruction to preserve high frame rates on standard CPU/edge hardware.
* **Beat 3: What Came of It (Receipts)**  
  Maintained stable real-time inference (30+ FPS) while generating prioritized low-latency audio cue triggers for obstacles within critical collision thresholds.

---

### Case Study 3: Low-Latency Search Opportunity & Decay Engine

* **Beat 1: The Problem**  
  Content management systems rely on static heuristic rules (like flagging unedited pages after 180 days) to identify search traffic decay, resulting in false positives on evergreen content and missing rapid-decay high-value queries.
* **Beat 2: What I Did & Decided**  
  Built a feature-extraction and scoring pipeline on DuckDB querying 79M+ daily search records (FlyRank Dataset). Trained a Random Forest classifier using a client-holdout validation design (`GroupShuffleSplit`) to prevent cross-domain data leakage. Excluded low-volume pages (≤ 100 impressions) and deleted URLs to suppress signal noise.
* **Beat 3: What Came of It (Receipts)**  
  Outperformed the rule-based baseline by +20.3% in F1-score (0.7842 vs. 0.5812) and generated an automated action playbook sorting candidate URLs into concrete editorial action tiers.

---

## 4. Bio & Hero Copy

### Hero Section
**Building distributed ML pipelines and real-time vision systems that execute under real hardware constraints.**  
I build beyond the notebook: multi-node sharding, edge perception, and leakage-free ranking engines.

### Short Bio (About Section)
I am a Computer Science student and applied machine learning engineer focused on distributed systems and computer vision. I care about systems that actually run: managing VRAM limits, optimizing edge inference latency, and ensuring data pipelines don't leak information across evaluation boundaries.

---

## 5. Contact & Conversion Copy

### Mid-Page CTA (Immediately following Case Studies)
> **Discuss System Architecture**  
> Looking to discuss distributed inference setups, edge vision benchmarks, or low-latency feature pipelines?  
> **[Book a 20-Minute Technical Screen via Cal.com]**

### Footer Section
* **Primary:** `[Schedule a 20-min Call on Cal.com]`
* **Direct Links:** `github.com/nauman024` &bull; `@gmail.com`