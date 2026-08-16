# Workflow Architecture

The system is divided into specialized automation workflows.

Instead of placing the entire transport lifecycle into one large automation, each workflow has a clearly defined responsibility.

This makes the system easier to understand, test, maintain, and extend.

---

# Workflow 01 — Customer Request → Transport Order

## Purpose

Convert a customer quote/request submission into a structured transport order.

## Trigger

A customer submits the transport request through the WordPress website.

## Process

```text
Customer Form
     ↓
Webhook
     ↓
Validate Request
     ↓
Normalize Data
     ↓
Generate Job ID
     ↓
Create Transport Order
     ↓
Calculate / Prepare Pricing
     ↓
Store Order
