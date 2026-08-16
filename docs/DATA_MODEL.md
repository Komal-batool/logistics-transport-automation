# Transport Order Data Model

The transport-order data model is centered around a single unique identifier:

## Auftragsnummer

The `Auftragsnummer` represents the Job ID for the transport order.

It acts as the correlation key throughout the entire automation lifecycle.

---

# Transport Order Fields

| Field | Description |
|---|---|
| Auftragsnummer | Unique transport Job ID |
| Status | Current transport status |
| Kundenname | Customer name |
| Firma | Customer/company name |
| E-Mail | Customer email |
| Telefonnummer | Customer telephone number |
| Abholadresse | Pickup address |
| Lieferadresse | Delivery address |
| Warenbeschreibung | Description of transported goods |
| Referenz | Customer or internal reference |
| Anfragedatum | Date the request was received |
| Fahrer | Assigned driver |
| Fahrer Telefon | Driver telephone number |
| Abholzeit | Pickup time |
| Lieferzeit | Delivery time |
| Unterschrift Absender | Sender signature |
| Unterschrift Empfänger | Receiver signature |
| Abholfotos | Pickup photo references |
| PDF-Link | Link/reference to generated delivery PDF |
| Google Drive Ordner | Transport document storage location |
| Fahrerformular-Link | Driver mobile form link |
| Notizen | Operational notes |

---

# Data Relationship

The Job ID connects all major transport information.

```text
                 Auftragsnummer
                       │
       ┌───────────────┼────────────────┐
       │               │                │
       ▼               ▼                ▼
   Customer        Transport         Driver
    Data             Data             Data
       │               │                │
       └───────────────┼────────────────┘
                       │
                       ▼
                Pickup Evidence
                       │
                       ▼
               Delivery Evidence
                       │
                       ▼
                Delivery PDF
                       │
                       ▼
                 Notifications
