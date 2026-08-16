# Setup & Configuration

This repository documents the architecture and implementation approach of the logistics automation system.

The actual production environment contains private credentials and client-specific configuration and is therefore not included in this repository.

---

# Required Components

The complete system requires the following components:

- n8n
- WordPress
- Fluent Forms or equivalent WordPress form solution
- Google Sheets
- Google Drive
- Gmail
- WhatsApp Cloud API
- PDF generation service
- Webhook/API connectivity

---

# 1. n8n

n8n acts as the central automation and orchestration layer.

The required workflows are configured around:

- Webhook triggers
- Data processing
- Google Sheets operations
- Google Drive operations
- Email communication
- WhatsApp communication
- PDF generation
- Business logic
- Error handling

---

# 2. WordPress

WordPress provides the user-facing forms.

Two primary interfaces are required:

### Customer Interface

Used to submit the initial transport request.

### Driver Interface

Used to retrieve and update the assigned transport order.

The driver interface supports mobile-oriented data collection including signatures and photographs.

---

# 3. Google Sheets

A structured transport-order sheet is used as the operational data layer.

The sheet should contain the fields documented in:

`DATA_MODEL.md`

Each transport order is identified by its unique `Auftragsnummer`.

---

# 4. Google Drive

Google Drive is used to store transport-related documents.

The automation can create or use the relevant transport folder and store the generated delivery documentation.

---

# 5. PDF Generation

A PDF generation service converts the prepared delivery-note content into a PDF document.

The exact provider is environment-specific.

The automation architecture is designed so that the PDF generation component can be replaced without changing the core transport-order logic.

---

# 6. Email

The email integration is configured within n8n.

The notification workflow uses the transport-order information to prepare the delivery completion message.

---

# 7. WhatsApp

The WhatsApp integration is configured through the appropriate WhatsApp Cloud API credentials.

The messaging component is separated from the main business logic so communication failures can be isolated and diagnosed independently.

---

# 8. Webhooks

WordPress communicates with n8n using secure webhook endpoints.

Typical events include:

```text
Customer Request
Driver Job Lookup
Driver Submission
Delivery Completion
