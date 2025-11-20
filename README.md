# NutriDry — Local frontend + optional Node.js + MongoDB backend

This repository contains:
- `index.html` — Updated single-file frontend with:
  - Brand treatment: "N" in green, "D" in orange, and slogan with capital letters highlighted.
  - Hero area replaced the checklist with centered brand logo and slogan.
  - Product detail page shows the selected product, and "You may also like" cards underneath (like Flipkart).
  - About section center-aligned, larger/fatter founder and team cards.
  - Packaging page includes an inline SVG flowchart for process steps.
  - Optional integration with a backend API (set `API_BASE` in `index.html`).

- Optional backend (Node/Express + MongoDB) files and instructions are below.

---

## Quick frontend notes

- Place your resource images in a `resources/` folder served by your server / static host:
  - `resources/nutridry-mark.png` — small mark (used in header/footer)
  - `resources/nutridry-full.png` — full brand image shown in hero (optional)
- If image files are missing, the textual brand (N green, D orange) will be shown instead.

- To use the API (optional), set `API_BASE` at the top of `index.html`, for example:
  - const API_BASE = "http://localhost:4000"

---

## Optional Backend: Node.js + Express + MongoDB

Below is a minimal backend you can run locally (or on a server). It exposes:
- GET /api/products
- GET /api/products/:id
- POST /api/orders

Files (examples):

- server.js — main server
- models/product.js — Mongoose product model
- models/order.js — Mongoose order model
- seed.js — script to seed product data into MongoDB
- .env — environment variables (MONGODB_URI, PORT)

### 1) Prerequisites

- Node.js (>=14)
- npm
- MongoDB instance (local or Atlas). If using Atlas, grab the connection string.

### 2) Install and run

- Create a project directory and add the server files (see below).
- Run:
  ```bash
  npm install express mongoose cors dotenv
  node seed.js          # seeds products into MongoDB (once)
  node server.js
  ```
- Server will run on PORT (default 4000).

### 3) How frontend connects

- In `index.html` set `API_BASE` to the server origin, e.g. `http://localhost:4000`.
- Frontend will fetch product list and single product; the checkout will POST orders if API_BASE is set.

---

## Database schema (MongoDB example)

- Product
  - id (string) — slug like 'moringa'
  - name, short, prices (object), description, fssai
- Order
  - orderId, date, name, mobile, email, address, payment, items (array), total

---

## Security & production notes

- Do not expose your MongoDB credentials publicly. Use environment variables.
- Add input validation & sanitization on server side for production.
- Implement rate-limiting, logging, and authentication for administrative endpoints.
- Serve `index.html` via a static server (nginx, or `express.static`) and point API calls to same or a proxied origin.

If you'd like, I can also provide the exact server files (server.js, models, seed) in separate code blocks now — let me know and I'll add them. 
