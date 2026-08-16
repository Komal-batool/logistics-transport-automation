# System Architecture

## Architecture Overview

This project implements a modular, event-driven logistics automation architecture designed to connect the complete transport lifecycle through a centralized Job ID.

The architecture separates customer-facing interfaces, business logic, operational data, document management, and communication into distinct layers.

This approach makes the system easier to maintain, test, extend, and integrate with additional business services.

---

## High-Level Architecture

```text
                         CUSTOMER
                            │
                            ▼
                 ┌─────────────────────┐
                 │      WordPress      │
                 │ Customer Request    │
                 │      Form           │
                 └──────────┬──────────┘
                            │
                         Webhook
                            │
                            ▼
                 ┌─────────────────────┐
                 │        n8n          │
                 │ Automation &        │
                 │ Orchestration Layer │
                 └──────────┬──────────┘
                            │
              ┌─────────────┼─────────────┐
              │             │             │
              ▼             ▼             ▼
         Job ID         Pricing       Validation
        Generation       Engine          Logic
              │             │             │
              └─────────────┼─────────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │    Google Sheets    │
                 │ Transport Order    │
                 │    Data Layer       │
                 └──────────┬──────────┘
                            │
                            │ Job ID
                            ▼
                 ┌─────────────────────┐
                 │ Driver Mobile       │
                 │ Interface           │
                 │ WordPress / Form    │
                 └──────────┬──────────┘
                            │
                     Driver Submission
                            │
                            ▼
                 ┌─────────────────────┐
                 │        n8n          │
                 │ Driver Processing   │
                 └──────────┬──────────┘
                            │
             ┌──────────────┼──────────────┐
             │              │              │
             ▼              ▼              ▼
        Signatures       Photos        Timestamps
             │              │              │
             └──────────────┼──────────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ Delivery Processing │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │ PDF Generation      │
                 │ Delivery Note       │
                 └──────────┬──────────┘
                            │
                            ▼
                 ┌─────────────────────┐
                 │    Google Drive     │
                 │ Document Storage    │
                 └──────────┬──────────┘
                            │
                            ▼
              ┌────────────────────────────┐
              │ Customer Communication     │
              │                            │
              │ Email + WhatsApp           │
              └────────────────────────────┘
