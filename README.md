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

```mermaid
flowchart TD
    A[Client / Natural Language Query] --> B[Master Agent Orchestrator]
    B --> C[Intent Router Engine]
    C --> D[Desktop GUI Worker]
    C --> E[Terminal System Worker]
    C --> F[Workspace Manager Worker]
    C --> G[Web & RAG Intelligence Worker]
    C --> H[System Diagnostics Worker]

⚙️ Core Subsystem Blueprints
Subsystem 1: Context-Isolated Multi-Worker Orchestrator
code Mermaid

flowchart TD
    Q[User Input Query] --> N[Fuzzy Normalizer & Context Resolver]
    N --> D{Dynamic Disambiguation Check}
    D -->|Ambiguous Request| User[Prompt User For Clarification]
    D -->|Validated Intent| R[Intent Routing & Execution DAG]
    R --> W1[Desktop GUI Worker Context]
    R --> W2[Terminal Worker Context]
    R --> W3[Web Intelligence Worker Context]

Key Engineering Features:

    Dynamic Disambiguation: Halts execution gracefully and queries the user for clarification when ambiguous multi-target inputs are detected.

    State & Audit Registry: Real-time logging of worker actions, targets, execution status, and error messages to enable automatic failure analysis.

    Session Memory Store: Thread-safe multi-turn context retention with pronoun resolution across conversation turns.

Subsystem 2: 4-Layer Deterministic Code Synthesis Pipeline
code Mermaid

flowchart TD
    P[Payload: Intent + Syntax Rules + Algorithm Logic + Roadmap] --> L1[Layer 1: Payload Contract Ingestion]
    L1 --> L2[Layer 2: Schema Sanitization & Context Isolation Guard]
    L2 --> L3[Layer 3: True Iterative Modular Synthesis Engine]
    L3 --> L4[Layer 4: Closed-Loop Compiler Verification]
    L4 -->|Compilation Success| Out[Clean Executable Code Artifact]
    L4 -->|Syntax Error Detected| L3

🔬 Core Architectural Contracts (Reference Logic)
1. Intent Router & Worker Dispatch Contract
code Python

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

2. Closed-Loop Compiler Verification Contract
code Python

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
