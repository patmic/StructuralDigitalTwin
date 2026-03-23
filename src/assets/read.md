# MALTG Architecture Validator v2.4 — Live Edition

**Multi-layer Architecture Ledger Technology Governance**

Dashboard completamente data-driven con recarga automática cada 5 segundos.

---

## 📁 Estructura del Proyecto

```
maltg-v2/
├── docker-compose.yml          ← Orquestación (1 servicio)
├── README.md
│
├── backend/
│   ├── Dockerfile              ← Python 3.12-slim + FastAPI
│   ├── main.py                 ← API: parseo OWL + serve JSON
│   └── requirements.txt        ← fastapi + uvicorn
│
├── data/                       ← ⚡ EDITAR AQUÍ para ver cambios
│   ├── MALTG_onto.owl          ← Ontología OWL 2 (RDF/XML)
│   └── dt_arch.json            ← Gemelo Digital estructural
│
└── frontend/
    └── index.html              ← Dashboard SPA (D3 + Chart.js)
```

---

## 🚀 Despliegue

```bash
# 1. Construir e iniciar
docker compose up -d --build

# 2. Verificar
docker compose ps
docker logs maltg-validator -f

# 3. Abrir
open http://localhost:8080

# API docs (FastAPI)
open http://localhost:8080/docs
```

---

## ✏️ Cómo editar la Ontología (MALTG_onto.owl)

El archivo `data/MALTG_onto.owl` es un OWL 2 en formato RDF/XML.
El dashboard lo re-lee cada 5 segundos. **No se necesita rebuild**.

### Agregar un nuevo nodo de clase:

```xml
<!-- Agregar dentro de <rdf:RDF> ... </rdf:RDF> -->
<owl:Class rdf:about="http://maltg.arch/onto#Mi_Nuevo_Concepto">
  <rdfs:subClassOf rdf:resource="http://maltg.arch/onto#AI_Layer"/>
  <rdfs:label>Mi Nuevo Concepto</rdfs:label>
  <maltg:layer>ai</maltg:layer>        <!-- togaf|cobit|nist|ai|blockchain|opendata|security|core -->
  <maltg:radius>9</maltg:radius>       <!-- tamaño del nodo en píxeles -->
  <maltg:description>Descripción visible en el tooltip</maltg:description>
  <maltg:score>75</maltg:score>        <!-- madurez 0-100 -->
</owl:Class>
```

### Agregar una relación cross-layer:

```xml
<owl:ObjectProperty rdf:about="http://maltg.arch/onto#mi_relacion">
  <rdfs:label>mi relacion</rdfs:label>
  <rdfs:domain rdf:resource="http://maltg.arch/onto#AI_Layer"/>
  <rdfs:range  rdf:resource="http://maltg.arch/onto#Blockchain_Layer"/>
  <maltg:weight>1.2</maltg:weight>    <!-- grosor del enlace -->
</owl:ObjectProperty>
```

### Capas disponibles (`maltg:layer`):

| Valor        | Color     | Descripción              |
|--------------|-----------|--------------------------|
| `core`       | #00e5ff   | Nodos raíz MALTG         |
| `togaf`      | #00e5ff   | Foundation — TOGAF       |
| `cobit`      | #ffc947   | Foundation — COBIT       |
| `nist`       | #ff4d6d   | Foundation — NIST CSF    |
| `ai`         | #a855f7   | Tech — Inteligencia Art. |
| `blockchain` | #10e98c   | Tech — Blockchain / DLT  |
| `opendata`   | #ff9a3c   | Tech — Open Data         |
| `security`   | #f472b6   | Tech — Security          |

---

## ✏️ Cómo editar el Gemelo Digital (dt_arch.json)

El archivo `data/dt_arch.json` define **completamente** el diagrama del Tab 03.
El dashboard lo re-lee cada 5 segundos. **No se necesita rebuild**.

### Agregar un nuevo microservicio:

```json
{
  "id":         "ms_nuevo",
  "label":      "Mi Servicio",
  "subtitle":   "Framework usado",
  "colorType":  "service",
  "x": 397, "y": 460,
  "width": 130, "height": 46,
  "status":     "active",
  "maltg_ref":  "AI_Layer",
  "description":"Descripción del servicio en el tooltip"
}
```

### Agregar una conexión:

```json
{ "from": "ms_ai", "to": "ms_nuevo", "style": "solid" }
```

### Tipos de color (`colorType`):

| Tipo        | Color     | Uso                      |
|-------------|-----------|--------------------------|
| `external`  | #ff9a3c   | Clientes y APIs externas |
| `gateway`   | #00e5ff   | API Gateway, Service Mesh|
| `security`  | #ff4d6d   | IAM, WAF, Vault, SIEM    |
| `service`   | #a855f7   | Microservicios core       |
| `data`      | #10e98c   | Bases de datos, Data Lake|
| `event`     | #ffc947   | Kafka, DLT, Streaming    |
| `monitor`   | #f472b6   | Prometheus, Grafana, OPA |
| `infra`     | #64748b   | K8s, CI/CD, Terraform    |

---

## 🌐 API Endpoints

| Endpoint         | Método | Descripción                              |
|------------------|--------|------------------------------------------|
| `/api/ontology`  | GET    | Parse MALTG_onto.owl → JSON graph        |
| `/api/dt-arch`   | GET    | Serve dt_arch.json con hash de cambios   |
| `/api/health`    | GET    | Health check + hashes actuales           |
| `/docs`          | GET    | Documentación interactiva FastAPI        |

---

## 🔄 Flujo de Auto-Reload

```
Usuario edita MALTG_onto.owl
        │
        ▼
  Archivo cambia en ./data/
        │
        ▼ (volumen Docker montado)
  FastAPI lee el archivo fresco en cada request
        │
        ▼
  MD5 hash del archivo cambia
        │
        ▼ (polling cada 5s en el browser)
  Frontend detecta hash distinto
        │
        ▼
  D3 force graph se re-renderiza automáticamente
```

---

## 🛑 Detener

```bash
docker compose down
```

---

*MALTG — TOGAF 9.2 · COBIT 5 · NIST CSF 1.1 · FastAPI · D3.js v7 · Chart.js v4*
