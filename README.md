# HD Freight Audit

Prototype SaaS for freight-cost control, warehouse shipment entry, carrier tariff management and invoice reconciliation.

## Live demo

https://feelxiaozhu.github.io/hd-freight-audit-demo/

## Current demo features

- Dashboard for freight-cost and discrepancy monitoring
- Chinese / Italian interface with saved language preference
- Employee login screen for the mobile workflow
- Demo employee roles: administrator, data-entry only, and data-entry + edit-own-records
- Admin back office no longer shows the warehouse-entry form
- Admin back office shows warehouse submissions with timestamp, employee, customer/shop, carrier, boxes, pallets, size/weight details and notes
- Mobile warehouse-entry form shown to warehouse employees after login
- Package / pallet configuration
- Pallet quantity, total height and weight entry
- Automatic cargo-height calculation from EPAL total height
- Dynamic carrier management
- New carriers automatically become available in mobile warehouse entry, Tariffario upload and PDF invoice upload
- Tariffario upload for PDF / Excel / CSV / TXT
- Carrier-safe Tariffario import: the user selects the carrier before upload and the selected carrier remains authoritative
- If a document clearly appears to belong to another carrier, the import is blocked
- Automatic detection of common surcharge codes such as IS, L, FUEL / carburante and COD / contrassegno
- Surcharge page starts empty
- Surcharges are created only after a carrier Tariffario is uploaded
- Surcharges are grouped by carrier
- Each carrier keeps its own Tariffario history and surcharge rules
- Uncertain detected surcharge values are marked Da verificare / 待确认
- PDF invoice upload with carrier validation
- If an invoice appears to belong to a different carrier than the selected carrier, import is blocked
- Freight-reconciliation / anomaly prototype
- Company / employee settings prototype
- Employee creation in the demo settings page

## Intended workflow

1. An administrator creates the company structure, warehouses and employee accounts.
2. A warehouse employee logs in from mobile.
3. The employee records the customer/shop, carrier, boxes, pallets, dimensions and weights.
4. The back office sees the submitted records without showing the warehouse input form.
5. The administrator adds/configures carriers.
6. For each carrier, the administrator selects that carrier and uploads its Tariffario.
7. The system validates the document/carrier relationship.
8. The system extracts surcharge codes and stores them only under that carrier.
9. The surcharge page displays separate carrier groups, for example BRT and GLS separately.
10. Carrier PDF invoices are uploaded under an explicitly selected carrier.
11. The system validates the invoice carrier before accepting the file.
12. The reconciliation engine compares theoretical and invoiced freight charges shipment by shipment.

## Carrier isolation rules

- BRT Tariffario data stays under BRT.
- GLS Tariffario data stays under GLS.
- BRT and GLS surcharge rules are not mixed.
- Uploads are bound to the carrier chosen by the user.
- If readable document text clearly identifies another carrier, the import is stopped instead of being assigned incorrectly.
- The same principle applies to PDF invoices.

## Employee login and permissions

The current public demo includes a front-end login flow to demonstrate the intended mobile experience.

Demo accounts:

- Alessandro / 1234 — administrator
- Mario / 1111 — data entry only
- Luca / 2222 — data entry + edit-own-records role model

The administrator sees the back office. Warehouse employees are directed to the mobile warehouse-entry interface.

### Important

The current login is a front-end prototype only. It is not production security. Real multi-device employee authentication, secure passwords, company isolation and centrally enforced permissions require a shared backend/database and server-side authentication.

## Language support

- 中文
- Italiano

The selected language is stored in the browser and restored on the next visit.

## Tariffario parsing

The current browser demo attempts to read PDF, XLSX / XLS, CSV and TXT files.

It can detect some common surcharge codes and percentages / euro amounts from readable text.

Complex carrier Tariffario PDFs, scans, irregular tables and production OCR should be processed by a backend service in the production version.

## Current limitations

This repository currently contains a front-end prototype/demo.

Not yet production-ready:

- Shared multi-user database across devices
- Secure server-side authentication
- Real company/tenant isolation
- Centrally enforced permissions
- Production PDF / OCR parsing
- Complete carrier tariff engine
- Complete invoice extraction
- Production freight-reconciliation engine
- Audit trail / change history
- Secure document storage

Demo data is primarily stored in browser localStorage.

## Roadmap

- Shared backend database for all warehouse employees
- Secure login across phones and computers
- Password hashing / reset flow
- Full permission enforcement
- Edit / deactivate employee accounts
- Editable carrier profiles and carrier settings
- Carrier activation / deactivation
- More reliable server-side Tariffario parsing
- Review / confirmation workflow for detected surcharge values
- Full PDF invoice extraction with shipment-level rows and invoice totals
- Automatic freight reconciliation and dispute reporting
- Monthly close report with theoretical total, invoiced total, difference, match rate and recovered credits

## Changelog

### Current development build

- Changed back office warehouse module into a warehouse-submission records view
- Added employee mobile login prototype
- Added administrator vs warehouse-employee experiences
- Added demo employee roles / permission model
- Added employee creation to company settings
- Added shipment records with employee, customer, carrier, boxes, pallets, size/weight and notes
- Removed pre-filled surcharge rules
- Surcharges now appear only after Tariffario upload
- Grouped surcharge display by carrier
- Added per-carrier Tariffario history display
- Added explicit carrier binding for Tariffario uploads
- Added carrier mismatch protection for Tariffario imports
- Added explicit carrier binding for invoice uploads
- Added carrier mismatch protection for invoice imports
- Preserved dynamic carrier creation across warehouse, Tariffario and invoice modules
- Preserved Chinese / Italian language switching

---

**HD Freight Audit — Prototype**

## 2026-10-04 · Admin / Employee split

- Admin page opens directly without an admin login screen.
- Warehouse records now include an admin **Edit / Modifica** action for correcting customer/store, carrier, boxes, pallets, dimensions/weight and notes.
- Added a separate mobile employee app at `employee.html` with employee-only login.
- Employee roles remain permission-based: `entry` can submit records; `entry_edit` can also edit their own recent records.
- Added PWA files (`manifest.webmanifest`, `service-worker.js`, `employee-icon.svg`) so the employee page can be added to a phone home screen as a standalone web app.
- Current prototype data still uses browser `localStorage`; real multi-phone shared data and secure authentication require a backend/database.


## 2026-10-04 · Customer photo recognition

- Restored **customer photo capture** on the employee mobile app.
- Employee can photograph/select a customer label or document and run browser-side OCR.
- OCR attempts to fill **customer code**, **customer/store name**, and **customer address** automatically.
- Recognition results are always editable before saving.
- Shipment records now store the customer address, and the admin record list can display and edit it.
- The GitHub-only version performs OCR in the browser; no Vercel backend is used.


## 2026-10-04 · Monthly reconciliation workflow

- Added a dedicated **monthly reconciliation** page organized by **month + carrier**.
- Monthly view shows warehouse records, uploaded invoice batches, the Tariffario valid for that month, and open anomaly count.
- Added monthly invoice batching: each uploaded carrier invoice is saved with a reconciliation month.
- Added Tariffario validity ranges (**valid from / valid to**) instead of a single date only.
- Monthly reconciliation selects the Tariffario whose validity range covers the selected month.
- Added anomaly workflow statuses: **Da verificare / 待确认**, **Corretto / 正确**, **Errore corriere / 快递收费错误**, **Corriere contattato / 已联系快递**, and **Nota di credito / 已退款**.
- The demo deliberately leaves theoretical freight, invoiced total, difference, and matched-shipment counts blank until real shipment-level invoice parsing exists; it does not invent reconciliation amounts.
