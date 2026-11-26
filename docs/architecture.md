# FlowGuard Architecture

## 1. Purpose

FlowGuard automates supplier invoice processing using
workflow orchestration, document processing and AI-assisted
data extraction.

The system validates extracted information and routes
invoices through a human approval process.

## 2. Architectural principles

- Backend owns business logic.
- n8n owns workflow orchestration.
- AI output is untrusted until validated.
- All important operations are auditable.
- Human approval is required before sensitive actions.
- Processing should be idempotent.
- External integrations must handle failures gracefully.

## 3. Components

### API
Node.js, TypeScript and Express.

Responsible for business logic, invoice lifecycle,
validation and approval operations.

### Document Processor
Python-based service.

Responsible for PDF text extraction and OCR.

### Workflow Orchestrator
n8n.

Responsible for coordinating workflows and external integrations.

### Database
PostgreSQL.

Responsible for persistent application data.

flowchart TD
    A[Invoice Submission] --> B[n8n Workflow]
    B --> C[Node.js API]
    C --> D[Python Document Processor]
    D --> E[AI Extraction]
    E --> F[Business Validation]
    F --> G[(PostgreSQL)]
    G --> H{Approval Required?}
    H -->|Yes| I[Human Approval]
    H -->|No| J[Review Required]
    I --> K[Approved or Rejected]