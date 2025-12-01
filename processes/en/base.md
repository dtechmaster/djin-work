# 🧩 DJIN Tech — Universal Base Process

[← Back to Processes](./README.md)

---

The DJIN Base Process defines **how any creation is born and evolves**, whether internal (DJIN products) or external (client projects).
It's simple, scientific, and iterative: **PoC → MVP → Final Product**.

No stage advances without passing through the 5 fundamental pillars:

1. **Definition (要件定義)**
2. **Architecture (設計)**
3. **Engineering (開発)**
4. **Quality Assurance / QA (品質保証)**
5. **Deploy (納品・展開)**

This is DJIN's most basic flow — and also the most powerful.
It guarantees technical truth, clarity, and continuous evolution.

---

## 🔄 1. Overview (Main Flowchart)

```mermaid
flowchart LR

    A[PoC<br>Proof of Concept] --> B[MVP<br>First Usable Version]
    B --> C[Final Product<br>Stable, Polished, Scalable]

    %% Post-conditions
    C --> D((Long-Term\nDelivery))
```

---

## 🧪 2. Natural Process Iteration

PoCs rarely become products directly.
First we prove ideas.
Then we shape them.
Then we refine them.

```mermaid
flowchart TD

    subgraph S1[First Iterations]
        A1[PoC 1] --> A2[PoC 2] --> A3[PoC 3]
    end

    S1 --> B1[MVP 1]
    B1 --> B2[MVP 2]
    B2 --> C1[Final Product]

    C1 --> D1((Complete Cycle))
```

*Each iteration reduces risk and increases clarity.*

---

## 🧱 3. The 5 Pillars (Invariable)

No phase (PoC, MVP, or Final Product) advances without passing through the 5 fundamental pillars of DJIN Engineering.

```mermaid
flowchart LR

    D1[Definition<br>要件定義] --> D2[Architecture<br>設計]
    D2 --> D3[Engineering<br>開発]
    D3 --> D4[Quality Assurance<br>品質保証]
    D4 --> D5[Deploy<br>納品・展開]
```

### Pillar functions:

* **Definition**: we understand what must exist (clarity → avoid ambiguity)
* **Architecture**: we decide *how* it must exist (design → avoid rework)
* **Engineering**: we implement with technical rigor
* **QA**: we ensure the system works and continues working
* **Deploy**: we close the cycle and deliver with confidence

These pillars repeat **in each PoC, each MVP, each final product**.

---

## 🔁 4. Integration of Pillars with PoC → MVP → Final Product Cycle

```mermaid
flowchart TD

    A[PoC] --> B[MVP] --> C[Final Product]

    %% Pillars applied to each phase
    subgraph X1[PoC]
        P1[Definition] --> P2[Architecture] --> P3[Engineering] --> P4[QA] --> P5[Deploy]
    end

    subgraph X2[MVP]
        M1[Definition] --> M2[Architecture] --> M3[Engineering] --> M4[QA] --> M5[Deploy]
    end

    subgraph X3[Final Product]
        F1[Definition] --> F2[Architecture] --> F3[Engineering] --> F4[QA] --> F5[Deploy]
    end

    A --> X1 --> B --> X2 --> C --> X3
```

---

## 🧠 5. Why does this work?

Because this process:

* reduces risk
* accelerates learning
* allows changes without trauma
* creates solid products
* standardizes quality
* guarantees visibility
* works for hardware, software, AI, systems, research, everything
* and scales as the company grows

This is **DJIN's Universal Base Process** —
the smallest unit of order that organizes all creative chaos.

---

**[← Back to Processes](./README.md)**
