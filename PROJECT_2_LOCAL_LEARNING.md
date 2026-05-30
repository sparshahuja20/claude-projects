# 🚀 Project 2 (Local): TransactionAI - Local Learning Setup

**Status:** 🟢 Ready for Development  
**Cost:** $0 (Free & Open Source)  
**Duration:** 8 weeks (Month 1-2)  
**Learning Focus:** All Month 1-2 concepts implemented locally  

---

## 📋 Table of Contents

1. [Project Overview](#project-overview)
2. [Architecture](#architecture)
3. [Tech Stack](#tech-stack)
4. [Setup & Installation](#setup--installation)
5. [Running Locally](#running-locally)
6. [Features Implemented](#features-implemented)
7. [Learning Path](#learning-path)
8. [API Endpoints](#api-endpoints)
9. [Code Structure](#code-structure)
10. [Example Workflows](#example-workflows)
11. [Extending the Project](#extending-the-project)

---

## 🎯 Project Overview

### What is This Project?

A **complete, locally-running AI fraud detection and customer analytics system** that demonstrates all Month 1-2 learning concepts:

- **What it does:** Analyzes transaction data, detects fraud, segments customers, generates insights
- **Who uses it:** You (learning locally) + Can be extended for banks
- **Why it matters:** Production-grade patterns + zero cost + full control

### Key Characteristics

```
✅ 100% Local Execution (no cloud)
✅ All Month 1-2 Concepts Implemented
✅ Production-Grade Architecture
✅ Free & Open Source
✅ Docker-based (reproducible)
✅ Real-time & Batch Processing
✅ ML Feature Engineering
✅ LLM Integration (with your API key)
```

---

## 🏗️ Architecture

### High-Level Architecture

```
┌─────────────────────────────────────────────────┐
│           YOUR LOCAL LAPTOP/DESKTOP             │
├─────────────────────────────────────────────────┤
│                                                  │
│  PRESENTATION LAYER                             │
│  ├─ FastAPI Swagger UI (http://localhost:8000) │
│  ├─ Jupyter Notebooks                           │
│  └─ Grafana Dashboards                          │
│                                                  │
├─────────────────────────────────────────────────┤
│                                                  │
│  APPLICATION LAYER                              │
│  ├─ FastAPI Backend (8000)                      │
│  ├─ Feast API Server (6566)                     │
│  └─ Error handling & validation                 │
│                                                  │
├─────────────────────────────────────────────────┤
│                                                  │
│  ML/FEATURE ENGINEERING LAYER                   │
│  ├─ Embeddings (OpenAI)                         │
│  ├─ RAG System (Chroma + Feast)                 │
│  ├─ Fraud Detection (Scikit-learn)              │
│  └─ Forecasting (Statsmodels)                   │
│                                                  │
├─────────────────────────────────────────────────┤
│                                                  │
│  DATA LAYER (All Local)                         │
│  ├─ PostgreSQL (port 5432)                      │
│  ├─ Chroma Vector DB (port 8001)                │
│  ├─ Redis Cache (port 6379)                     │
│  ├─ Kafka Streaming (port 9092)                 │
│  └─ Feast Feature Store                         │
│                                                  │
├─────────────────────────────────────────────────┤
│                                                  │
│  MONITORING & ANALYTICS                         │
│  ├─ Prometheus (port 9090)                      │
│  ├─ Grafana Dashboards (port 3000)              │
│  └─ Jupyter Notebooks (port 8888)               │
│                                                  │
└─────────────────────────────────────────────────┘
```

### Data Flow

```
User Transaction
    ↓
[FastAPI] - Validation & parsing (Week 4)
    ↓
[Embeddings] - Convert to vectors (Week 2)
    ↓
[Chroma] - Semantic similarity search (Week 2, 5)
    ↓
[Feast] - Real-time feature retrieval (Week 5)
    ↓
[RAG System] - Build context from retrieval (Week 5)
    ↓
[Anomaly Detection] - Statistical + semantic (Week 6-7)
    ↓
[LLM Prompting] - Generate explanation (Week 3, 7-8)
    ↓
[Response] - Fraud score + explanation + recommendations
```

---

## 🛠️ Tech Stack

### Core Components

| Layer | Technology | Version | Purpose |
|-------|-----------|---------|---------|
| **Frontend/API** | FastAPI | 0.104.1 | REST API framework |
| **Server** | Uvicorn | 0.23.2 | ASGI server |
| **Database** | PostgreSQL | 15.3 | Transactional storage |
| **Vector DB** | Chroma | 0.4.7 | Embeddings storage (Week 2) |
| **Feature Store** | Feast | 0.35.0 | Feature management (Week 5) |
| **Cache** | Redis | 7.0.12 | In-memory caching |
| **Messaging** | Kafka | 3.5.0 | Event streaming |
| **Notebooks** | Jupyter | Latest | Exploration & learning |
| **Monitoring** | Prometheus + Grafana | Latest | Metrics & dashboards |

### ML/AI Libraries

| Capability | Library | Purpose |
|-----------|---------|---------|
| **Embeddings** | OpenAI, Sentence-Transformers | Text to vectors (Week 2) |
| **Feature Engineering** | Scikit-learn, Pandas | Feature extraction (Week 2-3) |
| **Anomaly Detection** | Scikit-learn | Statistical detection (Week 6-7) |
| **Time Series** | Statsmodels, TSFresh | Forecasting (Week 7-8) |
| **ML Pipelines** | LangChain | LLM orchestration (Week 3-8) |
| **LLM** | OpenAI GPT-4 | Natural language (Week 3-8) |

### Container Orchestration

| Tool | Purpose |
|------|---------|
| Docker | Containerization |
| Docker Compose | Local multi-container setup |

---

## 🚀 Setup & Installation

### Prerequisites

```bash
# System Requirements
- macOS/Linux/Windows with WSL2
- Docker & Docker Compose installed
- 8GB+ RAM
- 50GB+ free disk space
- OpenAI API key (for LLM features)

# Installation Time: ~15 minutes
```

### Step 1: Install Docker

**macOS:**
```bash
# Using Homebrew
brew install docker docker-compose

# Or download Docker Desktop
# https://www.docker.com/products/docker-desktop
```

**Linux:**
```bash
# Ubuntu/Debian
sudo apt-get install docker.io docker-compose

# Start Docker service
sudo systemctl start docker
```

**Windows:**
```bash
# Download Docker Desktop for Windows
# Enable WSL2 in Settings
```

### Step 2: Clone/Setup Project

```bash
# Create project directory
mkdir transactionai-local
cd transactionai-local

# Create all project files (see structure below)
# Copy docker-compose.yml, Dockerfile, requirements.txt, etc.
```

### Step 3: Configure Environment

```bash
# Create .env file
cat > .env << 'EOF'
OPENAI_API_KEY=sk-your-key-here
DATABASE_URL=postgresql://user:password@postgres:5432/transactionai
CHROMA_SERVER_HOST=chroma
CHROMA_SERVER_HTTP_PORT=8000
REDIS_URL=redis://redis:6379
KAFKA_BROKER=kafka:9092
ENVIRONMENT=development
EOF

# Replace with your actual OpenAI API key
```

### Step 4: Start All Services

```bash
# Start all containers
docker-compose up -d

# Check status
docker-compose ps

# View logs
docker-compose logs -f api

# Stop all services
docker-compose down
```

---

## 🎬 Running Locally

### Quick Start (5 minutes)

```bash
# 1. Start services
docker-compose up -d

# 2. Initialize database
docker-compose exec api alembic upgrade head

# 3. Test API
curl http://localhost:8000/health

# 4. Access Swagger UI
open http://localhost:8000/docs
```

### Access Points

```
API Documentation:      http://localhost:8000/docs
Chroma Vector DB:       http://localhost:8001
PostgreSQL:             localhost:5432
Redis:                  localhost:6379
Kafka:                  localhost:9092
Feast UI:               http://localhost:8080
Jupyter Notebooks:      http://localhost:8888
Prometheus Metrics:     http://localhost:9090
Grafana Dashboards:     http://localhost:3000 (admin/admin)
```

### Sample API Requests

**1. Score a Transaction for Fraud**
```bash
curl -X POST http://localhost:8000/api/v1/transactions/score \
  -H "Content-Type: application/json" \
  -d '{
    "transaction_id": "TXN-001",
    "customer_id": "CUST-123",
    "amount": 150.00,
    "merchant": "Whole Foods",
    "merchant_category": "5411",
    "timestamp": "2026-05-29T14:30:00Z",
    "channel": "debit_card"
  }'
```

**Response:**
```json
{
  "transaction_id": "TXN-001",
  "fraud_score": 0.15,
  "fraud_risk": "low",
  "decision": "APPROVE",
  "confidence": 0.98,
  "reasons": [
    "Amount is normal for this customer",
    "Merchant category is typical",
    "Transaction time is consistent"
  ],
  "processing_time_ms": 87
}
```

**2. Get Customer Features**
```bash
curl http://localhost:8000/api/v1/customers/CUST-123/features
```

**3. Get Historical Features (Point-in-time)**
```bash
curl "http://localhost:8000/api/v1/customers/CUST-123/features-historical?as_of_date=2026-05-28T14:30:00Z"
```

**4. Investigate Transaction with RAG**
```bash
curl http://localhost:8000/api/v1/fraud/investigate/TXN-001
```

**5. Real-time Fraud Alerts (WebSocket)**
```bash
# Using websocat
websocat ws://localhost:8000/ws/fraud-alerts

# Or Python
import asyncio
import websockets

async def listen():
    async with websockets.connect('ws://localhost:8000/ws/fraud-alerts') as ws:
        async for message in ws:
            print(message)

asyncio.run(listen())
```

### Jupyter Notebooks (Learning)

```bash
# Access Jupyter at http://localhost:8888

# Create a new notebook and explore:
from app.services.embeddings import get_text_embedding
from app.services.chroma_client import ChromaVectorStore
from app.services.feast_client import FeastFeatureStoreClient

# Week 2: Explore embeddings
embedding = await get_text_embedding("Whole Foods purchase")
print(f"Embedding dimension: {len(embedding)}")
print(f"First 5 values: {embedding[:5]}")

# Week 5: Explore RAG
chroma = ChromaVectorStore()
results = await chroma.search_similar(
    collection_name="customers",
    query_embedding=embedding,
    k=5
)
print(f"Found {len(results['similar_items'])} similar customers")

# Week 5: Explore Feast
feast = FeastFeatureStoreClient()
features = await feast.get_customer_features("CUST-123")
print(f"Features: {features}")
```

---

## ✨ Features Implemented

### Core Features

#### 1. Transaction Ingestion & Validation (Week 4)
```
✅ Validate transaction data (Pydantic)
✅ Parse merchant categories
✅ Timestamp handling
✅ Error logging & recovery
```

#### 2. Embeddings (Week 2) ⭐
```
✅ Text-to-vector conversion (OpenAI)
✅ Customer behavioral embeddings
✅ Merchant embeddings
✅ Store in Chroma vector DB
✅ Cosine similarity search
```

#### 3. Feature Store (Week 5) ⭐
```
✅ Feast feature definitions
✅ Real-time feature serving (<100ms)
✅ Point-in-time correct retrieval
✅ Feature versioning
✅ PostgreSQL + SQLite backends
```

#### 4. RAG System (Week 5) ⭐⭐
```
✅ Retrieve context from Chroma + Feast
✅ Format context for LLM
✅ Generate answers with context
✅ Transaction investigation endpoint
✅ Similar transaction discovery
```

#### 5. Fraud Detection (Week 6-7) ⭐
```
✅ Embedding-based anomalies (Week 2)
✅ Statistical anomalies (z-score)
✅ Temporal pattern detection
✅ Velocity detection (transactions/time)
✅ Combined fraud scoring
```

#### 6. Prompt Engineering (Week 3) ⭐
```
✅ Few-shot categorization
✅ Chain-of-thought reasoning
✅ Role-based prompting
✅ Complex prompt templates
```

#### 7. Multi-turn Conversations (Week 6)
```
✅ Conversation memory
✅ Context-aware responses
✅ Scenario planning
✅ Stateful advisor
```

#### 8. Forecasting & Reporting (Week 7-8)
```
✅ Time-series trend analysis
✅ Churn probability prediction
✅ LLM-generated reports
✅ Customer insights
```

---

## 📚 Learning Path

### Week 1: Setup & Fundamentals
- [ ] Install Docker & Docker Compose
- [ ] Start all services (`docker-compose up`)
- [ ] Access API documentation (http://localhost:8000/docs)
- [ ] Test basic endpoints
- [ ] Review embeddings concept

### Week 2: Embeddings
- [ ] Study `backend/app/services/embeddings.py`
- [ ] Understand OpenAI embedding API
- [ ] Create embeddings for transactions
- [ ] Store in Chroma
- [ ] Search similar items
- [ ] **Exercise:** Create customer embedding

### Week 3: Prompt Engineering
- [ ] Study `backend/app/services/prompting.py`
- [ ] Learn few-shot prompting
- [ ] Understand chain-of-thought
- [ ] Try different prompt templates
- [ ] **Exercise:** Write categorization prompt

### Week 4: API & Error Handling
- [ ] Review `backend/app/main.py`
- [ ] Study request validation (Pydantic)
- [ ] Test error handling
- [ ] Review error logs
- [ ] **Exercise:** Add custom validation

### Week 5: RAG System
- [ ] Study `backend/app/services/rag_system.py`
- [ ] Understand retrieval pipeline
- [ ] Learn Feast feature store
- [ ] Test point-in-time retrieval
- [ ] **Exercise:** Build RAG query

### Week 6: Anomaly Detection & Conversation
- [ ] Study `backend/app/services/fraud_detection.py`
- [ ] Understand multiple detection methods
- [ ] Test conversation API
- [ ] **Exercise:** Detect custom anomalies

### Week 7-8: Forecasting & Reporting
- [ ] Study `backend/app/services/forecasting.py`
- [ ] Understand time-series analysis
- [ ] Generate reports
- [ ] **Exercise:** Predict churn

---

## 🔌 API Endpoints

### Transaction Endpoints

```
POST /api/v1/transactions/ingest
  Score and ingest a transaction
  
POST /api/v1/transactions/score
  Score transaction for fraud in real-time
  
GET /api/v1/fraud/alerts
  Get recent fraud alerts
  
WebSocket /ws/fraud-alerts
  Real-time fraud alert stream
```

### Feature Endpoints

```
GET /api/v1/customers/{customer_id}/features
  Get real-time features for customer
  
GET /api/v1/customers/{customer_id}/features-historical
  Get historical features (point-in-time)
  
POST /api/v1/features/compute
  Compute features for customer
```

### Fraud Endpoints

```
GET /api/v1/fraud/investigate/{transaction_id}
  Full RAG investigation of transaction
  
GET /api/v1/fraud/similar/{transaction_id}
  Find similar transactions (embedding-based)
```

### Segmentation Endpoints

```
GET /api/v1/segments
  Get all customer segments
  
GET /api/v1/segments/{segment_id}/customers
  Get customers in segment
```

### Insights Endpoints

```
GET /api/v1/insights/{customer_id}/monthly-report
  Generate monthly report with insights
  
GET /api/v1/insights/{customer_id}/recommendations
  Get personalized recommendations
```

### Advisor Endpoints

```
WebSocket /ws/advisor
  Multi-turn conversational advisor
```

### Health Endpoints

```
GET /health
  System health check
  
GET /health/database
  Database connectivity check
  
GET /health/chroma
  Chroma vector DB check
  
GET /health/feast
  Feast feature store check
```

---

## 📁 Code Structure

```
transactionai-local/
│
├── docker-compose.yml           (All services definition)
├── Dockerfile                   (Backend image)
├── requirements.txt             (Python dependencies)
├── .env.example                 (Environment template)
├── prometheus.yml               (Metrics config)
└── init.sql                     (Database initialization)

backend/
├── app/
│   ├── __init__.py
│   ├── main.py                  (FastAPI app, Week 4)
│   │
│   ├── routers/                 (API endpoints)
│   │   ├── transactions.py      (Week 3-4)
│   │   ├── features.py          (Week 5)
│   │   ├── fraud.py             (Week 6-7)
│   │   ├── segmentation.py      (Week 2, 5)
│   │   ├── insights.py          (Week 7-8)
│   │   └── advisor.py           (Week 6)
│   │
│   ├── services/                (Business logic)
│   │   ├── embeddings.py        (Week 2: Text to vectors)
│   │   ├── chroma_client.py     (Week 2, 5: Vector DB)
│   │   ├── feast_client.py      (Week 5: Feature store)
│   │   ├── feature_engineering.py (Week 2-8: All features)
│   │   ├── prompting.py         (Week 3: LLM prompting)
│   │   ├── rag_system.py        (Week 5: RAG)
│   │   ├── fraud_detection.py   (Week 6-7: Anomalies)
│   │   ├── conversation.py      (Week 6: Multi-turn)
│   │   ├── forecasting.py       (Week 7-8: Predictions)
│   │   ├── reporting.py         (Week 7-8: Reports)
│   │   └── segmentation.py      (Week 2, 5: Clustering)
│   │
│   ├── schemas/                 (Request/response models)
│   │   └── transaction.py       (Week 4: Validation)
│   │
│   └── models/                  (Database models)
│       ├── transaction.py
│       ├── customer.py
│       └── feature.py
│
├── migrations/                  (Database migrations)
│   └── versions/
│
├── tests/                       (Unit tests)
│   ├── test_embeddings.py
│   ├── test_fraud_detection.py
│   └── test_rag.py
│
└── alembic.ini                  (Migration config)

feast/
├── feature_repo.yaml            (Feast config)
├── feature_definitions.py       (Feature views)
└── data/                        (Offline store)

notebooks/
├── 01_exploration.ipynb         (Data exploration)
├── 02_feature_engineering.ipynb (Feature creation)
└── 03_fraud_detection.ipynb     (Fraud analysis)

docs/
├── API.md                       (API documentation)
├── SETUP.md                     (Setup guide)
├── ARCHITECTURE.md              (Architecture details)
└── EXAMPLES.md                  (Code examples)
```

---

## 📖 Example Workflows

### Workflow 1: Score a Transaction (End-to-End)

```python
# Step 1: API receives transaction
# backend/app/routers/fraud.py

@router.post("/api/v1/transactions/score")
async def score_transaction(request: TransactionRequest):
    """
    Week 4: API receives validated request
    """
    # Week 2: Generate embedding
    txn_embedding = await get_text_embedding(
        f"{request.merchant} - ${request.amount}"
    )
    
    # Week 5: Get customer embedding from Chroma
    customer_embedding = await chroma_store.find_similar_customers(
        txn_embedding, k=5
    )
    
    # Week 5: Get features from Feast
    features = await feast_store.get_customer_features(
        request.customer_id
    )
    
    # Week 6-7: Detect anomalies
    anomalies = await fraud_detector.detect_anomalies(
        request,
        features
    )
    
    # Week 3: Generate LLM explanation
    explanation = await generate_fraud_explanation(
        request,
        anomalies,
        features
    )
    
    # Week 6-7: Score fraud
    fraud_score = calculate_fraud_score(anomalies)
    
    return {
        "fraud_score": fraud_score,
        "explanation": explanation,
        "decision": "BLOCK" if fraud_score > 0.7 else "APPROVE"
    }
```

### Workflow 2: Generate Customer Insights (RAG)

```python
# backend/app/routers/insights.py

@router.get("/api/v1/insights/{customer_id}/monthly-report")
async def get_monthly_report(customer_id: str):
    """
    Week 7-8: Generate LLM report
    Uses: All previous weeks' features
    """
    
    # Week 5: Get features
    features = await feast_store.get_customer_features(customer_id)
    
    # Week 2, 5: Find similar customers
    similar = await chroma_store.find_similar_customers(
        customer_embedding, k=5
    )
    
    # Week 7-8: Time-series analysis
    churn_risk = await forecasting.predict_churn(customer_id)
    
    # Week 3: Create prompt
    prompt = f"""
    Generate a monthly report for customer:
    - Income: ${features['income']}
    - Spending: ${features['spending']}
    - Churn Risk: {churn_risk}
    - Similar Customers: {len(similar)}
    
    Include: insights, risks, recommendations
    """
    
    # Week 3-8: Generate report
    report = await client.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    
    return {
        "customer_id": customer_id,
        "report": report.choices[0].message.content
    }
```

---

## 🚀 Extending the Project

### Add Custom Features (Week 2-3)

```python
# In backend/app/services/feature_engineering.py

async def extract_custom_feature(transactions: list) -> dict:
    """Add your own feature"""
    
    # Your logic here
    
    return {
        "feature_name": "value"
    }
```

### Add Custom Prompts (Week 3)

```python
# In backend/app/services/prompting.py

async def custom_classification(data: dict) -> str:
    """Create custom LLM classification"""
    
    prompt = f"Classify this: {data}"
    
    response = await client.chat.completions.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    
    return response.choices[0].message.content
```

### Add Custom Alerts (Week 6)

```python
# In backend/app/services/fraud_detection.py

async def detect_custom_anomaly(transaction: dict) -> bool:
    """Detect your custom anomaly pattern"""
    
    # Your detection logic
    
    return is_anomaly
```

---

## 🧪 Testing

### Run Tests

```bash
# All tests
docker-compose exec api pytest

# Specific test file
docker-compose exec api pytest tests/test_embeddings.py

# With coverage
docker-compose exec api pytest --cov=app tests/
```

### Test Coverage

```
✅ Unit tests for embeddings
✅ Integration tests for RAG
✅ Fraud detection tests
✅ API endpoint tests
```

---

## 📊 Monitoring & Debugging

### View Logs

```bash
# API logs
docker-compose logs -f api

# PostgreSQL logs
docker-compose logs -f postgres

# Chroma logs
docker-compose logs -f chroma

# All services
docker-compose logs -f
```

### Monitor Metrics

```
Prometheus: http://localhost:9090
Grafana: http://localhost:3000
```

### Debug Mode

```python
# Set DEBUG in .env
DEBUG=true

# Get detailed logging
# All requests/responses will be logged
```

---

## 💡 Key Takeaways

### What You'll Learn

✅ **Week 1-2:** Embeddings and vector databases  
✅ **Week 3:** Prompt engineering with LLMs  
✅ **Week 4:** API design and error handling  
✅ **Week 5:** RAG systems and feature stores  
✅ **Week 6:** Anomaly detection and multi-turn AI  
✅ **Week 7-8:** Forecasting and LLM-powered reporting  

### Production Patterns

✅ Type-safe APIs (Pydantic)  
✅ Async/await for performance  
✅ Error handling & logging  
✅ Feature versioning  
✅ Point-in-time correctness  
✅ Real-time feature serving  
✅ WebSocket for streaming  

### Next Steps

1. **Start locally** - Run `docker-compose up`
2. **Explore notebooks** - Learn interactively
3. **Make API calls** - Test endpoints
4. **Extend features** - Add your own logic
5. **Deploy to cloud** - Use same code (optional)

---

## 🎓 Learning Resources

### Documentation
- FastAPI: https://fastapi.tiangolo.com/
- Chroma: https://docs.trychroma.com/
- Feast: https://docs.feast.dev/
- Pydantic: https://docs.pydantic.dev/

### Notebooks
- Jupyter: http://localhost:8888
- Exploration notebook: notebooks/01_exploration.ipynb

### Community
- Discord: [FastAPI Discord]
- GitHub: [Project repository]

---

## ❓ FAQ

**Q: Do I need a credit card?**  
A: Only if you use OpenAI API (minimal cost, ~$5-10/month for learning)

**Q: Can I run this on a laptop?**  
A: Yes! Requires 8GB RAM, 50GB disk

**Q: How do I scale to production?**  
A: Same code, just replace local services with cloud equivalents

**Q: What if Docker isn't installed?**  
A: Install from https://www.docker.com/products/docker-desktop

**Q: Can I add more services?**  
A: Yes, add to docker-compose.yml

---

## 📞 Support

For issues:
1. Check logs: `docker-compose logs -f`
2. Review error in detail
3. Check API docs: http://localhost:8000/docs
4. Search existing issues

---

## ✅ Checklist for Success

- [ ] Docker installed and running
- [ ] All services started (`docker-compose ps` shows all green)
- [ ] API accessible (http://localhost:8000/docs)
- [ ] Can make sample API call
- [ ] OpenAI API key configured
- [ ] PostgreSQL initialized
- [ ] Chroma vector DB running
- [ ] Feast feature store initialized

**Once all checked: You're ready to learn!** 🚀

---

**Created:** May 2026  
**Status:** Active Development  
**License:** MIT  
**Author:** Learning Project
