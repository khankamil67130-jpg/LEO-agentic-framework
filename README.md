# Leo Agentic Framework (Architecture & Design Spec)

> **High-Throughput Hierarchical Agent Orchestration & Deterministic Code Synthesis Engine with Closed-Loop Verification.**

[![Architecture](https://img.shields.io/badge/Architecture-Hierarchical%20Multi--Agent-blue.svg)]()
[![Verification](https://img.shields.io/badge/Verification-Compiler--in--the--Loop%20(C%2B%2B17)-red.svg)]()
[![Inference Engine](https://img.shields.io/badge/Inference-Local%20GGUF%20Quantized-green.svg)]()
[![Status](https://img.shields.io/badge/Status-Systems%20Proof--of--Concept-orange.svg)]()

---

## 📌 Executive Summary

**Leo Agentic Framework** is an enterprise-grade AI systems architecture designed for high-precision workflow automation, deterministic code generation, and multi-agent coordination. 

Large Language Model (LLM) agents often suffer from **context drift, token bloat, and hallucinated function calls**. Leo resolves these failure modes through:
1. **Hierarchical Multi-Agent Task Routing:** Decoupling intent parsing from domain execution with dynamic human-in-the-loop disambiguation.
2. **Context-Isolated Worker Registry:** Restricting prompt formatting rules exclusively to the target worker class, eliminating cross-domain context pollution.
3. **Deterministic 4-Layer Synthesis Pipeline:** A sequential synthesis engine with closed-loop `g++` compiler verification to guarantee zero syntax hallucinations.

---

## 🏛️ Master System Architecture

* **Client Layer:** Ingests raw multi-turn user intent & compound instructions.
* **Master Orchestration Layer:** Normalizes typos, resolves context pronouns, and decomposes inputs into a directed execution plan.
* **Intent Routing Engine:** Dispatches isolated sub-tasks to dedicated worker domains:
  * 🖥️ **Desktop GUI Worker:** Interacts with local workspace applications and window contexts.
  * 💻 **Terminal System Worker:** Sandboxed command execution, directory scaffolding, and file I/O.
  * 🌐 **Web Intelligence Worker:** Retrieval Augmented Generation (RAG) and search data synthesis.
  * 📊 **Diagnostics Worker:** Hardware telemetry, VRAM profiling, and real-time execution audit logging.

---

## ⚙️ Core Subsystem Blueprints

### Subsystem 1: Context-Isolated Multi-Worker Orchestrator

Rather than stuffing all tool definitions into a single massive prompt context, Leo dispatches tasks across isolated worker units.

* **Dynamic Disambiguation:** Automatically detects ambiguous queries (e.g., matching multiple target files) and halts execution to query the user for explicit clarification.
* **State & Audit Registry:** Real-time logging of worker actions, targets, execution status, and error messages to enable automatic failure analysis.
* **Session Memory Store:** Thread-safe multi-turn context retention with pronoun resolution across conversation turns.

---

### Subsystem 2: 4-Layer Deterministic Code Synthesis Pipeline

A closed-loop code generation pipeline designed for strict framework compliance and zero hallucination.

* **Layer 1 (Payload Contract Ingestion):** Ingests structured generation requests containing user intent, syntax rules, algorithmic specs, and roadmaps.
* **Layer 2 (Schema Sanitization & Context Isolation Guard):** Enforces mandatory payload schema contracts and halts pipeline immediately on missing parameters.
* **Layer 3 (True Iterative Modular Synthesis):** Deconstructs roadmaps into sequential module tasks with cumulative context passing to eliminate model state panic.
* **Layer 4 (Closed-Loop Compiler Verification):** Injects framework preprocessor mappings and runs `g++ -std=c++17` syntax verification in a sub-process to intercept syntax drift prior to release.

---
🔬 Core Architectural Contracts (Reference Logic)

### 1. Intent Router & Worker Dispatch Contract

```python
class MasterOrchestratorContract:
    """Decouples natural language parsing from domain execution."""
    
    def process_query(self, raw_query: str) -> str:
        # Step 1: Preprocess & resolve context
        clean_query = self.normalize_typos(raw_query)
        resolved_query = self.resolve_contextual_pronouns(clean_query)
        
        # Step 2: Intent routing & DAG generation
        execution_plan = self.router.route(resolved_query)
        
        # Step 3: Isolated worker execution
        results = []
        for step in execution_plan:
            worker = self.worker_registry.get(step["worker"])
            success, output = worker.execute(step["action"], step["params"])
            self.state_store.record_action(step["worker"], step["action"], success)
            results.append(output)
            
        return "\n".join(results)
```
                                 
2. Closed-Loop Compiler Verification Contract

```python
   class DeterministicSynthesisContract:
    """Iterative synthesis with closed-loop compiler verification."""
    
    def synthesize_and_verify(self, payload: dict, target_file: str) -> bool:
        # Iterative module generation with context accumulation
        source_code = self.iterative_engine.generate(payload)
        
        # Inject macro preamble and write target state
        compilable_code = self.inject_dsl_preamble(source_code)
        self.write_file(target_file, compilable_code)
        
        # Layer 4: Automated compiler syntax verification
        result = subprocess.run(
            ["g++", "-std=c++17", "-fsyntax-only", target_file],
            capture_output=True,
            text=True
        )
        return result.returncode == 0
 ```


🚀 Low-Latency Local Runtime Engine
Model: Quantized Qwen2.5-Coder-7B-Instruct running locally via llama-cpp-python.
Optimization: Flash Attention, VRAM offloading (n_gpu_layers = -1), KV cache offloading, and memory-mapped file execution (mmap).
Telemetry: Real-time VRAM/RAM hardware profiling using pynvml and psutil.
🗺️ Engineering Roadmap

Hierarchical Intent Routing & Dynamic Disambiguation.

4-Layer Deterministic Code Synthesis Pipeline with Compiler Verification.

Domain-Isolated Worker Registry (GUI, Terminal, Web, Diagnostics).

Distributed Agent Event Bus with Pub/Sub Architecture.

Financial Domain Document RAG & Deterministic Reconciliation Agent.      
