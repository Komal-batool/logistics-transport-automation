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


## Core Architectural Principle

The system is built around one central concept:

One transport order. One Job ID. One connected operational lifecycle.

The Job ID acts as the correlation key across the entire process.

Customer Request
       ↓
Job ID
       ↓
Transport Order
       ↓
Pricing
       ↓
Driver Operations
       ↓
Pickup Evidence
       ↓
Delivery Evidence
       ↓
Delivery Documentation
       ↓
Customer Notification

This prevents the workflow from creating disconnected records at different stages.

## Main Components

### 1. WordPress

WordPress provides the web-facing layer.

It is used for:

Customer request submission
Driver-facing mobile forms
Structured form data collection
Signature capture
Photo submission

The website layer is intentionally separated from the automation layer.

### 2. n8n

n8n acts as the central orchestration engine.

Responsibilities include:

Receiving webhooks
Processing incoming data
Generating Job IDs
Applying business rules
Calculating internal pricing
Searching transport orders
Updating transport records
Processing driver submissions
Triggering document generation
Managing notifications
Handling workflow errors

This creates a centralized automation layer between the website and external services.

### 3. Google Sheets

Google Sheets acts as the operational transport-order data layer.

Each transport order contains a unique Job ID and related operational information.

The sheet provides a simple structured data source for:

Customer information
Transport information
Driver assignment
Scheduling
Pickup information
Delivery information
Document references
Workflow status
### 4. Google Drive

Google Drive is used as the document storage layer.

Transport-related documents can be organized around the transport order and Job ID.

Examples include:

Delivery notes
Generated PDFs
Delivery evidence
Operational files

### 5. PDF Generation

The automation layer prepares the structured delivery information and sends it to the configured PDF generation service.

The generated document becomes the final digital delivery note.

### 6. Email

Email is used for automated delivery communication.

The workflow can send the completed delivery documentation to the relevant recipient once the transport is completed.

### 7. WhatsApp

WhatsApp integration provides an additional communication channel for delivery completion notifications.

The communication layer is separated from the core transport-order logic so that the transport process remains independent from a specific messaging provider.

Event-Driven Workflow

The system follows an event-oriented model.

Customer Request
Customer submits form
        ↓
Webhook received
        ↓
Request processing
        ↓
Job created
Driver Request
Driver opens assigned transport
        ↓
Job ID identified
        ↓
Existing transport order retrieved
        ↓
Operational information displayed
Driver Submission
Driver submits evidence
        ↓
Job ID validated
        ↓
Existing order identified
        ↓
Transport record updated
Delivery Completion
Delivery completed
        ↓
Delivery information processed
        ↓
PDF generated
        ↓
Document stored
        ↓
Customer notified
Separation of Responsibilities

### The architecture intentionally separates responsibilities.

Layer	Responsibility
WordPress	User interface
n8n	Orchestration and business logic
Google Sheets	Transport-order data
Google Drive	Document storage
PDF Service	Document generation
Gmail	Email communication
WhatsApp	Messaging

This makes the system easier to maintain and modify.

Reliability Considerations

The automation architecture incorporates:

Input validation
Job ID correlation
Explicit workflow boundaries
Error-handling paths
Service-level separation
Structured data processing
Document status tracking

The architecture is designed so failures in one external service can be identified without losing the core transport-order relationship.
