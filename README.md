# 🚚 Logistics Transport Automation System

### Enterprise-Grade Transport Operations Automation with n8n

> Transforming a fragmented transport workflow into a connected digital operations system — from the first customer request to the final delivery document.

---

## Overview

Managing a transport order involves far more than receiving a customer request.

Customer information must be captured, transport orders created, pricing calculated, drivers assigned, pickup and delivery evidence collected, documents generated, files stored, and customers notified.

When these activities are handled manually across disconnected tools, information becomes fragmented and operational work increases.

This project connects the complete transport lifecycle through a unified, event-driven automation architecture.

### The result:

**One Transport Order.  
One Job ID.  
One connected operational workflow.**

---

## What This System Automates

The system connects:

Customer Request
→ Transport Order
→ Internal Pricing
→ Driver Operations
→ Pickup Evidence
→ Delivery Confirmation
→ Digital Delivery Note
→ Cloud Storage
→ Customer Notification

Every stage remains linked to the same transport order through a unique Job ID.

---

## Core Capabilities

### Customer Request Automation

Customer requests submitted through the website enter the automation layer through a secure webhook.

The system validates incoming information, prepares the transport data, generates a unique Job ID, and creates the transport order.

### Intelligent Internal Pricing

Each transport request can be evaluated against internal pricing rules including:

- distance
- transport time
- fuel costs
- vehicle costs
- driver costs
- fixed operating costs
- profit margin
- business pricing rules

The pricing engine operates internally and does not expose business pricing logic to customers.

### Unified Transport Order

Every transport operation is associated with a single Job ID.

This keeps customer information, scheduling information, driver information, pickup evidence, delivery evidence and final documentation connected throughout the lifecycle.

### Driver Mobile Workflow

The driver receives access to the transport order and can submit operational evidence from a mobile device.

The workflow supports:

- sender signature
- receiver signature
- pickup photographs
- pickup timestamp
- delivery timestamp
- driver information
- transport status updates

### Automated Delivery Documentation

Once delivery information is submitted, the system prepares the delivery documentation automatically.

The final delivery note can contain:

- Job ID
- customer information
- pickup address
- delivery address
- transport details
- signatures
- delivery evidence
- timestamps

### Document Storage

Generated documents and operational files are organized in cloud storage and remain associated with the corresponding transport order.

### Automated Notifications

Once the delivery process is completed, the system can automatically distribute the final delivery information through configured communication channels including:

- Email
- WhatsApp

---

# System Architecture

```text
                         CUSTOMER
                            │
                            ▼
                  ┌───────────────────┐
                  │   WordPress Form  │
                  │ Customer Request  │
                  └─────────┬─────────┘
                            │
                            ▼
                  ┌───────────────────┐
                  │       n8n         │
                  │ Automation Layer  │
                  └─────────┬─────────┘
                            │
             ┌──────────────┼──────────────┐
             ▼              ▼              ▼
       Job ID Engine   Pricing Engine   Validation
             │              │              │
             └──────────────┼──────────────┘
                            ▼
                  ┌───────────────────┐
                  │ Transport Order   │
                  │   Google Sheets   │
                  └─────────┬─────────┘
                            │
                            ▼
                  ┌───────────────────┐
                  │   Driver Mobile   │
                  │     Workflow      │
                  └─────────┬─────────┘
                            │
              ┌─────────────┼─────────────┐
              ▼             ▼             ▼
          Signatures      Photos      Timestamps
              │             │             │
              └─────────────┼─────────────┘
                            ▼
                  ┌───────────────────┐
                  │ Delivery Document │
                  │      Engine       │
                  └─────────┬─────────┘
                            │
                            ▼
                  ┌───────────────────┐
                  │   Google Drive    │
                  │ Secure Documents  │
                  └─────────┬─────────┘
                            │
                 ┌──────────┴──────────┐
                 ▼                     ▼
              Email                 WhatsApp
