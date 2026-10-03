# HD Freight Audit

Prototype SaaS for freight-cost control, warehouse shipment entry, carrier tariff management and invoice reconciliation.

## Live demo

https://feelxiaozhu.github.io/hd-freight-audit-demo/

## Current demo features

- Dashboard with shipment, theoretical freight cost, invoiced cost and discrepancy summary
- Warehouse shipment-entry page
- Package / pallet configuration
- Pallet quantity, height and weight entry
- Automatic cargo-height calculation from EPAL total height
- Chinese / Italian language selector
- Selected language saved in the browser
- Dynamic carrier management
- New carriers automatically become available in:
  - Warehouse shipment entry
  - Tariffario upload
  - PDF invoice upload
- Tariffario upload for PDF / Excel / CSV / TXT
- Demo-side tariff text extraction
- Automatic detection of common surcharge codes such as:
  - IS
  - L
  - FUEL / carburante
  - COD / contrassegno
- Automatically detected surcharges are linked to the selected carrier
- Surcharge rules include carrier, code, calculation method, value, effective month and verification status
- Uncertain detected values are marked as **Da verificare / 待确认**
- Carrier PDF invoice upload area
- Freight reconciliation / anomaly view
- Company / employee settings prototype

## Intended workflow

1. A company configures its warehouses, employees, carriers, package types and pallets.
2. Warehouse staff record outgoing shipments.
3. The company uploads each carrier's tariffario.
4. The system extracts tariff rules and surcharge codes and stores them under that specific carrier.
5. Monthly variable surcharges can be updated without overwriting historical periods.
6. Carrier PDF invoices are uploaded.
7. The system compares theoretical freight charges with invoiced charges shipment by shipment.
8. Differences, unexpected surcharges, duplicate charges or weight discrepancies are highlighted for review.

## Multi-carrier logic

Carriers are no longer hard-coded to BRT and GLS.

The demo starts with BRT, GLS, FedEx and DHL, but additional carriers can be created. Once created, a carrier is automatically available in the warehouse, tariffario and invoice modules.

Surcharge rules are carrier-specific so that the same code used by different carriers does not get mixed together.

## Language support

The interface currently supports:

- 中文
- Italiano

The selected language is saved locally and restored on the next visit from the same browser.

## Tariffario parsing

The current browser demo attempts to read:

- PDF
- XLSX / XLS
- CSV
- TXT

It can detect some common surcharge codes and percentages / euro amounts from readable text.

This is still a prototype parser. Complex carrier tariff PDFs, scanned documents, tables with irregular structures and production OCR should be processed by a backend service in the production version.

## Current limitations

This repository currently contains a **front-end prototype/demo**.

The following are not yet production-ready:

- Shared multi-user database
- Secure user authentication
- Real company account isolation
- Server-side PDF / OCR parsing
- Production tariff engine
- Full invoice reconciliation engine
- Audit trail / change history
- Secure document storage
- Production permissions enforcement

Demo data is primarily stored in the browser with localStorage.

## Roadmap

Next planned items:

- Employee login page for desktop / mobile
- Only registered company employees can log in
- Role and permission management
  - Data entry only
  - Edit own entries
  - Edit all warehouse entries
  - View tariffs
  - Manage tariffs and surcharges
  - Upload invoices
  - View reconciliation
  - Administrator
- Create / edit / deactivate employees
- Editable carrier profiles
- Carrier activation / deactivation
- Carrier-specific settings
- More reliable automatic tariff parsing
- Automatic surcharge confirmation workflow
- Shared backend database for multiple warehouse employees
- Full PDF invoice extraction and automatic freight reconciliation

## Goal

The goal is to evolve this prototype into a multi-company freight-audit SaaS platform for wholesalers and distributors, where each company can configure its own carriers, tariffs, packaging rules, employees, permissions and surcharge structures.

## Changelog

### Current development build

- Added Chinese / Italian language switching
- Added persistent language preference
- Added dynamic carrier creation
- Synced carrier list across warehouse, tariffario and invoice modules
- Added tariffario parsing prototype
- Added automatic surcharge-code detection
- Linked surcharge rules to individual carriers
- Added verification status for uncertain surcharge values
- Expanded roadmap for employee login and permission control

---

**HD Freight Audit — Prototype**
