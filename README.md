# Scalable-AI-Service-Desk-Solution-RBAC-Based-Ticket-Automation-with-CRAG-LLM-Kafka
This project is a Proof of Concept (PoC) for an AI-powered service desk system that automates ticket creation, classification, and routing using:  Corrective RAG (CRAG) for robust retrieval Large Reasoning Model (LLM) for intent understanding Apache Kafka for event-driven scalability RBAC enforcement for secure, compliant workflows
The system is designed to reduce manual triage, improve assignment accuracy, and ensure auditability.


Objectives
Automate ticket triage and routing
Improve assignment precision (target ≥ 95%)
Reduce triage time (target ≥ 60–70%)
Ensure RBAC-compliant request handling
Enable scalable, real-time processing via Kafka

Architecture
High-Level Flow
User Request → Kafka Producer → RBAC Validator → CRAG Pipeline → LLM Reasoning → Routing Engine → Ticket Creation → Kafka Consumer → Service Desk System

Core Components
1. Input Layer (Kafka Producer)
Captures user requests from UI / API
Publishes events to Kafka topic: ticket_requests
2. RBAC Validation Layer
Validates user roles and permissions
Rejects unauthorised requests early
Prevents invalid LLM processing

CRAG Pipeline (Corrective Retrieval-Augmented Generation)
Steps:
Initial retrieval from vector DB (Pinecone)
Relevance scoring
If low confidence:
Re-query
Use fallback knowledge base
Pass corrected context to LLM

Large Reasoning Model Layer
Performs:
Intent classification
Entity extraction (system, urgency, request type)
Context-aware reasoning using CRAG output
5. Routing Engine
Hybrid logic:
Rule-based (RBAC + department mapping)
ML-based (historical patterns)
Decision:
Confidence ≥ threshold → auto-assign
Else → manual review queue
6. Kafka Consumer Layer
Consumes processed tickets
Pushes to the service desk system (e.g., internal ITSM tool)
7. UI Layer (Streamlit)
User submits requests
Displays:
Generated ticket
Assigned team
Confidence score

Data Flow (Detailed)
User submits request via UI
API publishes event to Kafka (ticket_requests)
RBAC service validates access
CRAG pipeline retrieves + corrects context
LLM processes:
Intent
Entities
Routing engine assigns team
Result published to Kafka (ticket_processed)
Consumer updates service desk system
Logs stored for audit + feedback loop

