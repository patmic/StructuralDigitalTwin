<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=venom&height=150&color=gradient&text=Structural%20Digital%20Twin%E2%80%93Driven%20Validation%20for%20a%20Multidimensional-nl-LegalTech%20Governance%20Architecture%20Ontology&fontSize=27&fontColor=aaf&fontAlign=50&fontAlignY=44&descAlign=32&descAlignY=40" width="100%"/>

  <img src="https://capsule-render.vercel.app/api?type=transparent&height=70&color=gradient&text=🕸️%20⇄%20Δ%20→%20✲&textBg=false&fontColor=696969&fontAlign=50&fontAlignY=50&animation=twinkling" width="50%"/>
  <br/>
  <b>MALTG</b> (Multidimensional Architecture LegalTech Governance) is a formally verified system that connects an <b>OWL 2 governance ontology</b> to a <b>live microservice Structural Digital Twin</b> and automatically measures — in milliseconds — how far your LegalTech enterprise is from full <b>TOGAF® · COBIT® · NIST CSF · GDPR · eIDAS · NIS2</b> compliance.
  <br/>
  <img src="/src/assets/imgLine.svg" height="5px" width="100%"/>
  <a href="https://github.com"><img src="https://img.shields.io/badge/version-1.0_MALTG-00e5ff?style=for-the-badge&labelColor=0d1117&logo=git&logoColor=00e5ff" alt="version"/></a>
  <a href="/data/MALTG_Odontology.owl"><img src="https://img.shields.io/badge/🕸️_OWL_2_Classes-54-a855f7?style=for-the-badge&labelColor=0d1117" alt="OWL Classes"/></a>
  <a href="/data/StructuralDigitalTwin.json"><img src="https://img.shields.io/badge/⬡_DT_Services-39-10e98c?style=for-the-badge&labelColor=0d1117" alt="DT Services"/></a>
  <a href="/src/backend/main.py"><img src="https://img.shields.io/badge/Validation_Dims-9-ffc947?style=for-the-badge&labelColor=0d1117" alt="Dimensions"/></a>
  <a href="/LICENSE"><img src="https://img.shields.io/badge/License-CC_BY_NC_4.0-f472b6?style=for-the-badge&labelColor=0d1117" alt="License"/></a>
  <br/>
  <img src="https://skillicons.dev/icons?i=vscode,github,docker,python,fastapi&theme=dark" alt="Tech Stack"/>
</div>
<div align="center">
  <br/><br/>
  <b>MALTG : Multidimensional Architecture LegalTech Governance</b>
  <br/><br/>
  <img src="/src/assets/imgMALTG.png" alt="MALTG Architecture Diagram"/>
  <br/><br/>
  <sub>
    <b>— Overview —</b> The system has <b>8 vertical architectural layers</b>
    (External → Security → Service Mesh → Microservices → Data → Observability → Infra → CI/CD) plus a horizontal <b>LegalTech Domain Layer</b> — the novel v3 contribution.
    Each service carries <code>maltg_ref</code> annotations linking it to OWL 2 concepts in the ontology.
    Dashed-red boxes indicate <b>governance gaps</b> (concepts defined in Ω but absent from Δ).
  </sub>
</div>

---

[![](https://readme-typing-svg.demolab.com?font=Roboto&weight=500&pause=5000&color=blue&width=500&height=30&lines=🗺️+Quick+Start+Map)]()

```
"I want the theory"            →  § Formal Model
"I want to run it"             →  § Quick Start
"I want the numbers"           →  § Validation Results
"I want to extend it"          →  § Extend the Experiment
"I want the paper"             →  § Academic Contribution
"I want the API"               →  § API Reference
"I want to reproduce results"  →  § ACM Reproducibility
```

---

## 📐 Formal Model — `MALTG = ⟨Ω, Δ, Γ, Ψ, δ⟩`

[![](https://readme-typing-svg.demolab.com?font=Roboto&weight=500&pause=5000&color=blue&width=500&height=30&lines=Formal+Model+/+Validation+Methodology)]()

<div align="center">

<img src="https://img.shields.io/badge/Ω-MALTG_Odontology.owl-00e5ff?style=flat-square&labelColor=0d1117" alt="Ω"/>
<img src="https://img.shields.io/badge/Δ-StructuralDigitalTwin.json-10e98c?style=flat-square&labelColor=0d1117" alt="Δ"/>
<img src="https://img.shields.io/badge/Γ-maltg_ref_mapping-a855f7?style=flat-square&labelColor=0d1117" alt="Γ"/>
<img src="https://img.shields.io/badge/Ψ-coverage_engine-ffc947?style=flat-square&labelColor=0d1117" alt="Ψ"/>
<img src="https://img.shields.io/badge/δ-conformance_gap-ff4d6d?style=flat-square&labelColor=0d1117" alt="δ"/>

</div>

| Symbol | Component | Formal Definition | Artefact |
|:------:|-----------|-------------------|:--------:|
| **Ω** | **Ontological Reference** | `⟨C, P, I, ⊑, A⟩` — 54 classes · 15 properties · maturity scores ∈ [0,100] | `MALTG_Odontology.owl` |
| **Δ** | **Structural Digital Twin** | `⟨V, E, τ, μ⟩` — 39 services · 54 edges · 9 layers · directed graph `G(V,E)` | `StructuralDigitalTwin.json` |
| **Γ** | **Conformance Mapping** | `Γ: C → 2^V` via `maltg_ref` — each OWL class mapped to implementing DT services | `main.py` |
| **Ψ** | **Hierarchical Coverage** | `Ψ(d) = 0.4·𝟙[root∈R] + 0.6·(|sub(d)∩R| / |sub(d)|)` ∈ [0,1] | `main.py → psi()` |
| **δ** | **Conformance Gap** | `δ(d) = score_Ω(d) · (1 − Ψ(d))` — unrealised governance potential | `GET /api/validation` |

### Theorem 1 — Proven Properties of Ψ

| Property | Statement | Verification |
|----------|-----------|:------------:|
| **Determinism** | Same `Ω + Δ` always → identical scores | `pytest` exact float assertions |
| **Monotonicity** | `R ⊆ R′ ⟹ Ψ_R(d) ≤ Ψ_{R′}(d)` | Sensitivity analysis (§ below) |
| **Completeness** | `R ⊇ C_d ⟹ Ψ(d) = 1.0` | Full-coverage boundary test |
| **Boundedness** | `Ψ(d) ∈ [0, 1]` for all `d` | Empty / full DT boundary test |

---

## ⬡ Architecture Layers

[![](https://readme-typing-svg.demolab.com?font=Roboto&weight=500&pause=5000&color=blue&width=500&height=30&lines=⬡+Architecture+Layers)]()

<table>
<tr>
<td width="50%" valign="top">

### 🔵 Foundation Layer

| | Framework | Domains | `score_Ω` |
|---|-----------|---------|:---------:|
| 🏛️ | **TOGAF 9.2** | ADM Cycle · 6 architecture domains · Enterprise Continuum | 91.7 |
| 🎛️ | **COBIT 5** | EDM · APO · BAI · DSS · MEA | 84.3 |
| 🔒 | **NIST CSF 1.1** | Identify · Protect · Detect · Respond · Recover | 77.5 |

### 🟣 Technology Integration Layer

| | Domain | Components | `score_Ω` |
|---|--------|-----------|:---------:|
| 🤖 | **AI / ML** | ML Models · NLP Pipeline · Computer Vision · Predictive Analytics | 87.2 |
| ⛓️ | **Blockchain** | Smart Contracts · DLT Network · Consensus · Tokenization | 76.2 |
| 📡 | **Open Data** | APIs · Data Lakes · Open Standards · Interoperability | 83.4 |
| 🛡️ | **Security** | Zero Trust · Encryption · IAM · Compliance | 87.6 |

</td>
<td width="50%" valign="top">

### 🔵 LegalTech Domain Layer *(v3 — novel contribution)*

| Concept | Regulation | Status |
|---------|-----------|:------:|
| `Contract_Lifecycle_Management` | eIDAS 910/2014 | ✅ |
| `GDPR_Compliance` | GDPR 2016/679 | ✅ |
| `eIDAS_Compliance` | eIDAS 2.0 · 2024/1183 | ✅ |
| `NIS2_Compliance` | NIS2 2022/2555 | ✅ |
| `Regulatory_Compliance_Engine` | Multi-framework | ✅ |
| `eDiscovery_Pipeline` | EDRM · ABA Rule 1.6 | ⚠️ **GAP** |
| `Legal_DLT_Notarization` | eIDAS Art. 41 | ⚠️ **GAP** |
| `Attorney_Client_Confidentiality` | ABA Model Rule 1.6 | ⚠️ **GAP** |
| `Smart_Legal_Contracts` | UNIDROIT · LegalDocML | ⚠️ **GAP** |
| `Legal_Knowledge_Base` | ECLI · EuroVoc | ⚠️ **GAP** |
| `Court_System_Integration` | EU e-Justice Portal | ⚠️ **GAP** |

</td>
</tr>
</table>

---

## 🚀 Quick Start

<details>
<summary><b>📁 Repository Structure</b>
<br/>
<img src="https://img.shields.io/badge/Structure-2496ed?style=for-the-badge&labelColor=0d1117&logo=wikibooks&logoColor=2496ed" alt="Structure"/>
</summary>

```
maltg/
├── 📄  README.md
├── 🐳  docker-compose.yml              ← single-command deploy, port 8080
│
├── 📁  data/                           ← ✏️ Edit here to update dashboard live
│   ├── 🦉  MALTG_Odontology.owl        ← OWL 2 / RDF-XML  (54 classes, 15 props)
│   └── 🔷  StructuralDigitalTwin.json  ← Digital Twin (39 services, 54 connections)
│
├── 📁  src/
│   ├── 📁  backend/
│   │   ├── 🐍  main.py                 ← FastAPI · 5 endpoints · Ψ scoring engine
│   │   ├── 📋  requirements.txt
│   │   └── 🐳  Dockerfile              ← python:3.12-slim
│   ├── 📁  frontend/
│   │   └── 🌐  index.html              ← SPA · 5 tabs · D3.js + Chart.js
│   └── 📁  assets/
│       ├── 🖼️  MALTG.png
│       ├── 🖼️  conformance_dashboard.svg
│       ├── 🖼️  formal_model.svg
│       ├── 🖼️  pipeline.svg
│       └── 🖼️  sensitivity.svg
│
└── 📁  evaluation/                     ← academic replication package
    ├── 📄  expert_survey.pdf
    ├── 📊  responses_anonymized.csv
    ├── 📓  analysis.ipynb
    └── 🧪  test_scoring.py             ← bit-for-bit regression suite
```

</details>

<details>
<summary><b>⚡ Deploy & Run</b>
<br/>
<img src="https://img.shields.io/badge/Docker-ready-2496ed?style=for-the-badge&labelColor=0d1117&logo=docker&logoColor=2496ed" alt="Docker"/>
</summary>

```bash
# 1 · Clone repository
git clone https://github.com/your-org/maltg && cd maltg

# 2 · Launch (requires Docker >= 20.10) · Python 3.12 · FastAPI · D3.js SPA
docker compose up -d --build

# 3 · Open the 5-tab dashboard
open http://localhost:8080

# 4 · Verify system health and all endpoints
curl http://localhost:8080/api/health       # { status: ok, owl_exists: true }
curl http://localhost:8080/api/validation   # 9-dim conformance scores (live)
curl http://localhost:8080/api/methodology  # formal model + 5-phase pipeline
open http://localhost:8080/docs             # Swagger UI

# 5 · Pretty-print full validation report
curl -s http://localhost:8080/api/validation | python3 -m json.tool
```

> 💡 **Live editing:** Modify `data/MALTG_Odontology.owl` or `data/StructuralDigitalTwin.json`
> → press **↺ Reload Data** → scores update instantly, no rebuild required.

</details>

---

## 🎮 Live Dashboard — 5 Tabs

| Tab | Content | Endpoint |
|-----|---------|----------|
| 🦉 **Ontology** | D3.js force graph — 54 OWL 2 classes + 15 properties, interactive zoom | `localhost:8080` |
| 🔷 **Digital Twin** | Interactive canvas — 39-service architecture with layer colour coding | `localhost:8080` |
| 📊 **Validation** | Live 9-dim radar chart + gap bars — recalculates instantly on data change | `localhost:8080` |
| 🔬 **Methodology** | Formal 5-phase pipeline with mathematical definitions and phase outputs | `localhost:8080` |
| 🚀 **Swagger UI** | Try all API endpoints in-browser, inspect request/response schemas | `localhost:8080/docs` |

---

## 📊 Validation Results — v3.0

<div align="center">

![MALTG 9-dimension conformance dashboard](/src/assets/conformance_dashboard.svg)

| Dimension | `score_Ω` | `Ψ` | `score_Δ` | `δ (gap)` | Status |
|:----------|:---------:|:---:|:---------:|:---------:|:------:|
| TOGAF Governance | 91.7 | 70% | 64.2 | 27.5 | ⚠️ Gap |
| COBIT Control | 84.3 | 100% | 84.3 | **0.0** | ✅ Full |
| NIST Resilience | 77.5 | 100% | 77.5 | **0.0** | ✅ Full |
| AI Integration | 87.2 | 85% | 74.1 | 13.1 | ⚠️ Gap |
| Blockchain Adoption | 76.2 | 85% | 64.8 | 11.4 | ⚠️ Gap |
| Open Data Compliance | 83.4 | 100% | 83.4 | **0.0** | ✅ Full |
| Security Posture | 87.6 | 100% | 87.6 | **0.0** | ✅ Full |
| Interoperability | 86.3 | 100% | 86.3 | **0.0** | ✅ Full |
| 🔵 **LegalTech Compliance** | **69.1** | **60%** | **41.5** | **27.6** | 🔵 Critical |
| **OVERALL** | **82.6** | — | **73.7** | **8.9** | |

</div>

> **Top gaps:** `LEGALTECH` (−27.6) · `TOGAF` (−27.5) · `AI` (−13.1)

### Gap Visual Summary

```
Dimension    score_Δ / score_Ω  ──────────────────────────────  δ
────────────────────────────────────────────────────────────────
TOGAF          64 / 91   ████████████████████░░░░░░░  ⚠️  −27.5
COBIT          84 / 84   ████████████████████████████  ✅   0.0
NIST           77 / 77   ██████████████████████████    ✅   0.0
AI             74 / 87   ████████████████████████░░░   ⚠️  −13.1
BLOCKCHAIN     64 / 76   ████████████████████░░░░░░░   ⚠️  −11.4
OPEN DATA      83 / 83   ████████████████████████████  ✅   0.0
SECURITY       87 / 87   █████████████████████████████ ✅   0.0
INTEROP        86 / 86   █████████████████████████████ ✅   0.0
LEGALTECH      41 / 69   ██████████████░░░░░░░░░░░░░   🔵  −27.6
────────────────────────────────────────────────────────────────
OVERALL        73 / 82                             gap −8.9
```

---

## ♟️ Sensitivity Analysis — Monotonicity Verified

![Sensitivity analysis — Theorem 1.2 monotonicity](/src/assets/sensitivity.svg)

Each remediation step adds one missing `maltg_ref` service to Δ. All curves are strictly non-decreasing, **empirically confirming Theorem 1.2 (Monotonicity)**. LegalTech (blue) shows the steepest gain because it starts at the deepest gap.

### LegalTech Remediation Path → δ = 0.0

```
Step  Action                       score_Δ    Ψ       δ
────────────────────────────────────────────────────────
  0   Baseline (Δ₀)                  41.5    60%    27.6  🔵 Critical
  1   + eDiscovery Pipeline          47.3    69%    21.8  ⚠️
  2   + DLT Notarization             53.1    77%    16.0  ⚠️
  3   + Smart Legal Contracts        58.9    85%    10.2  ⚠️
  4   + Attorney Privilege Control   64.7    94%     4.4  ⚠️
  5   + Legal Knowledge Base         66.1    96%     3.0  ⚠️
  6   + Court System Integration     69.1   100%     0.0  ✅ Full
```

---

## 🔬 Ontology Engineering Methodology

The MALTG ontology `Ω` is built through a **4-phase lifecycle** that couples formal knowledge-engineering methods with the MALTG formal model:

| Phase | Base Methodology | Deliverable | Key Artefact |
|-------|-----------------|-------------|--------------|
| **P1 — Requirements** | NeOn | MALTG Specification Document | 36 CQs · 9×6 governance scope matrix |
| **P2 — Design** | SAMOD | OWL 2 T-Box + unit tests | `MALTG_Odontology.owl` (54 classes, 15 props) |
| **P3 — Simulation** | Synthetic Data Generation | High-fidelity A-Box dataset | `StructuralDigitalTwin.json` (39 services, 54 edges) |
| **P4 — Validation** | Structural Digital Twin | Integrity & Compliance Report | Ψ/δ scorecard · ACM-L3 package |

> The pipeline is **iterative**: any dimension with `δ(d) > 0` after Phase P4 triggers a new SAMOD modelet in Phase P2 → new A-Box in Phase P3 → re-validation in Phase P4.

---

## 🔧 Extend the Experiment

### Add an OWL 2 class → `data/MALTG_Odontology.owl`

```xml
<!-- Paste inside <rdf:RDF> … </rdf:RDF> -->
<owl:Class rdf:about="http://maltg.arch/onto#AI_Legal_Reasoning">
  <rdfs:subClassOf rdf:resource="http://maltg.arch/onto#LegalTech_Domain"/>
  <rdfs:label>AI Legal Reasoning</rdfs:label>
  <maltg:layer>legaltech</maltg:layer>
  <maltg:radius>9</maltg:radius>
  <maltg:description>Automated legal reasoning via LLMs — EU AI Act compliance</maltg:description>
  <maltg:score>55</maltg:score>
  <maltg:regulation>EU AI Act 2024/1689 — High-Risk AI Systems</maltg:regulation>
</owl:Class>
```

### Add a microservice → `data/StructuralDigitalTwin.json`

```json
{
  "id": "lt_ediscovery",
  "label": "eDiscovery Pipeline",
  "subtitle": "EDRM · ABA Rule 1.6",
  "colorType": "legaltech",
  "x": 180, "y": 520, "width": 128, "height": 40,
  "status": "active",
  "maltg_ref": ["eDiscovery_Pipeline", "Attorney_Client_Confidentiality", "LegalTech_Domain"],
  "description": "Automated legal hold, collection, review pipeline with privilege logging"
}
```

→ Press **↺ Reload Data** → **LegalTech δ drops 27.6 → ≈18.2** instantly.

<details>
<summary><b>🎨 Available <code>maltg:layer</code> colour values</b></summary>

| Value | Swatch | Layer |
|-------|:------:|-------|
| `core` | ![](https://img.shields.io/badge/--%20-00e5ff?style=flat-square&labelColor=00e5ff) | MALTG root nodes |
| `togaf` | ![](https://img.shields.io/badge/--%20-00e5ff?style=flat-square&labelColor=00e5ff) | Foundation — TOGAF 9.2 |
| `cobit` | ![](https://img.shields.io/badge/--%20-ffc947?style=flat-square&labelColor=ffc947) | Foundation — COBIT 5 |
| `nist` | ![](https://img.shields.io/badge/--%20-ff4d6d?style=flat-square&labelColor=ff4d6d) | Foundation — NIST CSF |
| `ai` | ![](https://img.shields.io/badge/--%20-a855f7?style=flat-square&labelColor=a855f7) | Tech Integration — AI/ML |
| `blockchain` | ![](https://img.shields.io/badge/--%20-10e98c?style=flat-square&labelColor=10e98c) | Tech Integration — Blockchain/DLT |
| `opendata` | ![](https://img.shields.io/badge/--%20-ff9a3c?style=flat-square&labelColor=ff9a3c) | Tech Integration — Open Data |
| `security` | ![](https://img.shields.io/badge/--%20-f472b6?style=flat-square&labelColor=f472b6) | Tech Integration — Security |
| `legaltech` | ![](https://img.shields.io/badge/--%20-60a5fa?style=flat-square&labelColor=60a5fa) | LegalTech Domain *(v3 — novel)* |

</details>

---

## 📡 API Reference

| Method | Endpoint | Description | Key Fields |
|:------:|----------|-------------|------------|
| `GET` | `/api/health` | System status + SHA-256 file hashes | `owl_exists` · `owl_hash` · `dt_hash` |
| `GET` | `/api/ontology` | OWL 2 → D3.js force graph | `nodes[54]` · `links[15]` · `node_count` |
| `GET` | `/api/dt-arch` | Structural Digital Twin graph | `services[39]` · `connections[54]` |
| `GET` | **`/api/validation`** | **9-dim conformance scores (live)** | `dimensions[]` · `overall_gap` · `top_gaps` |
| `GET` | `/api/methodology` | Formal 5-phase model metadata | `formal_model` · `phases[]` · `validation_properties[]` |
| `GET` | `/docs` | Swagger UI — try all endpoints in-browser | — |

---

## 🏆 ACM Reproducibility

| Level | ACM Standard | MALTG Guarantee |
|:-----:|:------------:|-----------------|
| **L1** Repeatability | Artifact Available | `docker compose up` → identical scores on any Docker ≥ 20.10 machine |
| **L2** Replicability | Artifact Evaluated | Zenodo DOI · OWL in Turtle + RDF/XML · `pytest evaluation/test_scoring.py` |
| **L3** Reproducibility | Results Reproduced | Anonymised expert survey · open CSV · executable Jupyter analysis |

### Regression Suite

```bash
pip install requests pytest
pytest evaluation/test_scoring.py -v
```

```
TOGAF     onto=91.7  dt=64.2  gap=27.5  PASS  ✅
COBIT     onto=84.3  dt=84.3  gap=0.0   PASS  ✅
NIST      onto=77.5  dt=77.5  gap=0.0   PASS  ✅
AI        onto=87.2  dt=74.1  gap=13.1  PASS  ✅
BC        onto=76.2  dt=64.8  gap=11.4  PASS  ✅
OD        onto=83.4  dt=83.4  gap=0.0   PASS  ✅
SEC       onto=87.6  dt=87.6  gap=0.0   PASS  ✅
INTEROP   onto=86.3  dt=86.3  gap=0.0   PASS  ✅
LEGALTECH onto=69.1  dt=41.5  gap=27.6  PASS  ✅
OVERALL   onto=82.6  dt=73.7  gap=8.9   PASS  ✅
```

---

## 📚 Academic Contribution

<div align="center">

| Attribute | Value |
|-----------|-------|
| **Title** | *Structural Digital Twin–Driven Validation for a Multidimensional Architecture LegalTech Governance Ontology* |
| **Target** | Applied Sciences · MDPI — **Q1** |
| **Model** | `MALTG = ⟨Ω, Δ, Γ, Ψ, δ⟩` — 5-tuple · 4 proven mathematical properties |
| **Frameworks** | TOGAF 9.2 · COBIT 5 · NIST CSF 1.1 · GDPR · eIDAS 2.0 · NIS2 |
| **Scientific gap** | First formal multi-framework validator with LegalTech ontology + automated DT conformance scoring |
| **Structural validation** | OWL consistency · μ-closure · graph acyclicity · monotonicity suite (10/10) |
| **Reproducibility** | ACM L1 · L2 · L3 |

</div>

### Research Questions

| # | Question | Method | Result |
|:---:|----------|--------|:------:|
| **RQ1** | Can OWL 2 formalise TOGAF/COBIT/NIST/LegalTech semantics in one machine-processable model? | HermiT reasoning · structural metrics | ✅ Consistent · μ-closure 100% |
| **RQ2** | Can a Structural Digital Twin automatically quantify governance gaps? | Ψ engine · monotonicity regression suite | ✅ 10/10 assertions pass |
| **RQ3** | Which dimensions have the largest gaps in LegalTech microservice ecosystems? | 9-dim conformance scoring · remediation path | LegalTech δ = 27.6 · 6-step path |
| **RQ4** | How does MALTG compare to ArchiMate+TOGAF and SABSA? | 6-attribute comparison matrix (Table 1) | **6/6** vs 3/6 vs 2/6 |

### Impact Research Questions

| # | Question | Scientific Significance |
|:---:|----------|------------------------|
| **IQ1** | Does the bimodal governance maturity pattern generalise across LegalTech organisations of varying scale? | Enables statistically significant benchmarking across N≥3 production deployments |
| **IQ2** | Can the Ψ/δ engine extend to a federated multi-organisation Digital Twin preserving all 4 proven properties? | Opens cross-organisational LegalTech governance benchmarking — currently unaddressed |
| **IQ3** | What is the minimal ontological extension to formally capture EU AI Act 2024/1689 high-risk obligations in the MALTG T-Box? | Establishes the first AI-Act-complete LegalTech governance ontology ahead of August 2026 obligations |

---

<div align="center">

[![OWL Classes](https://img.shields.io/badge/OWL_2_Classes-54-a855f7?style=for-the-badge&labelColor=0d1117)](/data/MALTG_Odontology.owl)
[![DT Services](https://img.shields.io/badge/DT_Services-39-10e98c?style=for-the-badge&labelColor=0d1117)](/data/StructuralDigitalTwin.json)
[![Dimensions](https://img.shields.io/badge/Governance_Dims-9-ffc947?style=for-the-badge&labelColor=0d1117)](/src/backend/main.py)
[![Docker](https://img.shields.io/badge/Docker-ready-2496ed?style=for-the-badge&labelColor=0d1117&logo=docker)](/docker-compose.yml)
[![ACM](https://img.shields.io/badge/ACM_Reproducibility-L1·L2·L3-00e5ff?style=for-the-badge&labelColor=0d1117)](/evaluation)
[![DOI](https://img.shields.io/badge/DOI-zenodo.XXXXX-64748b?style=for-the-badge&labelColor=0d1117&logo=zenodo)](https://zenodo.org)

<br/>

[![TOGAF](https://img.shields.io/badge/TOGAF-9.2-00e5ff?style=for-the-badge&labelColor=0d1117)](https://www.opengroup.org/togaf)
[![COBIT](https://img.shields.io/badge/COBIT-5-ffc947?style=for-the-badge&labelColor=0d1117)](https://www.isaca.org/resources/cobit)
[![NIST](https://img.shields.io/badge/NIST_CSF-1.1-ff4d6d?style=for-the-badge&labelColor=0d1117)](https://www.nist.gov/cyberframework)
[![GDPR](https://img.shields.io/badge/GDPR-2016%2F679-60a5fa?style=for-the-badge&labelColor=0d1117)](https://gdpr.eu)
[![eIDAS](https://img.shields.io/badge/eIDAS-2.0-60a5fa?style=for-the-badge&labelColor=0d1117)](https://digital-strategy.ec.europa.eu)
[![NIS2](https://img.shields.io/badge/NIS2-2022%2F2555-60a5fa?style=for-the-badge&labelColor=0d1117)](https://www.enisa.europa.eu)
[![EU AI Act](https://img.shields.io/badge/EU_AI_Act-2024%2F1689-f472b6?style=for-the-badge&labelColor=0d1117)](https://digital-strategy.ec.europa.eu/en/policies/regulatory-framework-ai)

<br/>

<sub><b>MALTG Architecture Validator</b> · FastAPI · D3.js v7 · Chart.js v4 · OWL 2 DL · Docker Compose · Python 3.12</sub>
<br/>
<img src="https://readme-typing-svg.demolab.com?font=Fira+Code&size=14&pause=1000&color=475569&center=true&vCenter=true&width=750&lines=TOGAF®+·+COBIT®+ISACA+·+NIST+CSF+·+GDPR+EUR-Lex+·+eIDAS+EU+Commission+·+NIS2+ENISA" alt="Compliance frameworks"/>

</div>

<img src="https://capsule-render.vercel.app/api?type=waving&color=gradient&customColorList=6,11,20&height=120&section=footer" width="100%"/>
