# System Architecture

## Overview

This project implements an event-driven logistics automation architecture designed to connect the complete transport lifecycle through a centralized Job ID.

The architecture separates customer-facing interfaces, workflow orchestration, operational data, document storage, document generation, and customer communication into dedicated components.

The result is a modular system where each business event triggers the appropriate automation workflow.

---

## High-Level Architecture

```text
┌───────────────────────┐
│       Customer        │
│   Quote / Request     │
└──────────┬────────────┘
           │
           ▼
┌───────────────────────┐
│       WordPress       │
│   Customer Form       │
└──────────┬────────────┘
           │ Webhook
           ▼
┌────────────────────────────────┐
│              n8n               │
│      Automation Layer          │
│                                │
│ • Request Processing           │
│ • Job ID Generation            │
│ • Business Logic               │
│ • Pricing Calculation          │
│ • Driver Workflow              │
│ • Document Orchestration       │
│ • Notifications                │
└──────────┬─────────────────────┘
           │
           ▼
┌───────────────────────┐
│    Transport Order    │
│     Data Layer        │
│    Google Sheets      │
└──────────┬────────────┘
           │
           ├──────────────────────┐
           │                      │
           ▼                      ▼
┌───────────────────┐    ┌────────────────────┐
│  Driver Interface │    │  Business Services │
│    WordPress      │    │ Pricing / APIs     │
└─────────┬─────────┘    └────────────────────┘
          │
          │ Driver Updates
          ▼
┌────────────────────────────────┐
│       Existing Transport       │
│          Order / Job ID        │
└──────────────┬─────────────────┘
               │
               ▼
┌───────────────────────┐
│ Delivery Documentation│
│   PDF Generation      │
└──────────┬────────────┘
           │
           ▼
┌───────────────────────┐
│     Google Drive      │
│ Secure Document       │
│       Storage         │
└──────────┬────────────┘
           │
           ▼
┌────────────────────────────────┐
│       Notifications            │
│                                │
│   Email + WhatsApp             │
└────────────────────────────────┘
