# Pultio

**A friendly, hardware-connected point-of-sale system for Czech retail shops.**

Runs on a common laptop plus one thermal printer — no expensive dedicated hardware. Works out of the box with a real barcode scanner, ESC/POS receipt printer, and cash drawer. Czech-first, EET 2.0 ready for 1 Jan 2027.

Pultio grows out of the bachelor thesis *Pokladní systém pro maloobchody* (Hai Hung Nguyen, MFF UK, 2024), which proved the design but never connected real hardware. This is the design made into a real product.

## What makes it different

- **Real hardware, out of the box** — keyboard-wedge scanner, 80mm ESC/POS printer, cash-drawer kick, all tested on real devices.
- **Named parked receipts** — unlimited, each labelled with a note. A gap in the competition (VShop, Vinasoft, Dotykačka, iProSoft).
- **Sell items without a barcode** — instant sale with name, price, VAT.
- **Runs offline on your own machine** — LAN-local deployment, no forced cloud dependency.
- **EET 2.0 day one** — sale pipeline integrates the fiscalization API, certified before competitors.

## Architecture

One backend API, three clients:

| Component | Stack | Job |
|---|---|---|
| **Backend** | Java · Spring Boot 3 · PostgreSQL · Docker Compose | Auth (Spring Security + JWT), catalog, stock, sales, statistics, EET. |
| **POS app** | Electron · React · Vite · TypeScript | The register: checkout, closure, receipt printing, drawer kick (hardware from the main process). |
| **Management web** | React · Vite SPA · TypeScript | Back office: catalog, stock, suppliers, statistics, users, settings. |
| **Mobile** | React Native (Expo) | Manager on the go: dashboard, stock overview, catalog. No checkout. |

One OpenAPI spec is the contract; typed clients are generated for all three frontends.
