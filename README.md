# 🏭 AI Invoice Processing & Oracle ERP Integration Agent

![n8n](https://img.shields.io/badge/n8n-EA4B71?style=for-the-badge&logo=n8n&logoColor=white)
![Gemini](https://img.shields.io/badge/Google_Gemini_2.5_Flash-4285F4?style=for-the-badge&logo=google&logoColor=white)
![Oracle](https://img.shields.io/badge/Oracle_ERP-F80000?style=for-the-badge&logo=oracle&logoColor=white)
![Google Drive](https://img.shields.io/badge/Google_Drive-34A853?style=for-the-badge&logo=google-drive&logoColor=white)
![Retool](https://img.shields.io/badge/Retool_Dashboard-3D3D3D?style=for-the-badge&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=for-the-badge&logo=javascript&logoColor=black)

> **Industry**: Textile Manufacturing | **Country**: Pakistan
> **Pattern**: AI Document Extraction → Oracle Multi-Table Validation → Human Approval

---

## 🧩 What This System Does

An hourly automation agent that:
1. 📂 **Scans a Google Drive folder** for new supplier invoice PDFs
2. 🤖 **Uses Gemini AI** to extract 11 structured fields from each invoice
3. 🏦 **Validates against Oracle ERP** — supplier NTN lookup + GRN matching
4. ✅ **Routes matched invoices** to a Retool dashboard for human approval
5. ❌ **Logs and files errors** with structured error codes for manual resolution

---

## 🔄 Workflow at a Glance

```
Hourly Cron → Google Drive Scan → Download PDF
    → Gemini 2.5 Flash (AI Extraction)
    → JS Parser & Cleaner
    → Oracle: Supplier Lookup (NTN)
        ├── NOT FOUND → Error: SUPPLIER_NOT_FOUND → Error Folder
        └── FOUND → Oracle: GRN Match Query (Date + Amount + Supplier)
                ├── 0 matches → Error: NO_GRN_MATCH → Error Folder
                ├── 2+ matches → Error: MULTIPLE_GRN_MATCH → Error Folder
                └── 1 exact match → Retool Dashboard (status: PENDING)
```

---

## 📊 Fields Extracted by Gemini AI

| Field | Example |
|---|---|
| Supplier Name | ABC Textile Co. |
| Supplier NTN | 1234567-8 |
| Invoice Number | INV-2025-0042 |
| PO Number | PO-9981 |
| GRN Number | GRN-445 |
| Invoice Date | 2025-12-03 |
| Total Amount | 850,000 PKR |
| Tax Amount | 127,500 PKR |
| Subtotal | 722,500 PKR |
| Currency | PKR |
| Line Items | Array with item, qty, rate, amount |

---

## 🗄️ Oracle ERP Tables Used

| Table | Purpose |
|---|---|
| `SGD_03DEC25.SUPPLIER_MT` | Supplier master — NTN lookup |
| `SGD_03DEC25.GRN_MT` | Goods Receipt Note master |
| `SGD_03DEC25.GRN_DETAIL` | GRN line item details |
| `SGD_03DEC25.PURCHASE_INVOICE_MT` | Existing purchase invoice records |
| `SGD_03DEC25.PURCHASE_INVOICE_DETAIL` | Invoice line items |
| `SGD_03DEC25.INV_BOOKS_MT` | Invoice book reference |

---

## ⚠️ Error Taxonomy

| Error Code | Meaning | Resolution |
|---|---|---|
| `SUPPLIER_NOT_FOUND` | NTN not in Oracle SUPPLIER_MT | Add supplier to master table |
| `NO_GRN_MATCH` | No GRN matches date + subtotal + supplier | Manual GRN lookup required |
| `MULTIPLE_GRN_MATCH` | 2+ GRNs match same criteria | Human to select correct GRN |
| `PARSE_ERROR` | Gemini output not valid JSON | Review invoice quality |

---
---

## Interested in a Similar System?

Want to build something like this? Let's talk.

Whether you want to:
- Replicate this exact system for your own business
- Build a custom automation tailored to your workflow
- Discuss how AI automation can solve your specific problem

**Feel free to reach out — I would love to help.**

[![LinkedIn](https://img.shields.io/badge/Connect_on_LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](http://linkedin.com/in/aina-asim-659b67369)
[![GitHub](https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white)](https://github.com/AinaAsim)
[![WhatsApp](https://img.shields.io/badge/WhatsApp_Me-25D366?style=for-the-badge&logo=whatsapp&logoColor=white)](https://wa.me/923206455471)

**WhatsApp:** +92 320 6455471
**LinkedIn:** [Aina Asim](http://linkedin.com/in/aina-asim-659b67369)
**GitHub:** [github.com/AinaAsim](https://github.com/AinaAsim)

---

## Workflow Files — Confidential

The n8n workflow JSON for this project is **not published** and is kept private for security purposes.

This includes protecting:
- Real business logic and internal process flows
- Live API endpoint configurations
- Actual database schemas and credentials
- Client data and proprietary automation architecture

> This is a production system. Workflow internals are intentionally kept confidential to maintain security and client trust.
---

## 📜 License & Copyright

© 2024 Aina Asim. All Rights Reserved.

The documentation, architecture diagrams, and system designs presented in this repository are provided for **portfolio demonstration purposes only**. Unauthorized copying, modification, or distribution is prohibited.
