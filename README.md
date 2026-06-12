# 🛒 ShopKaro — Modern eCommerce System
### Re-Engineered from Legacy osCommerce (PHP) → Modern Microservices (Python + HTML/CSS/JS)

> **Course:** SE-601 Software Re-Engineering | Karakoram International University  
> **Instructor:** Asif Hussain | **Student:** Shahgufta | **June 2026**  
> **GitHub:** https://github.com/Shahgufta/ecommerce-reengineering

---

## 📌 Project Overview

| | |
|--|--|
| 🏛️ **Legacy System** | osCommerce V4 — Real PHP/MySQL E-Commerce (since 2000) |
| 🆕 **Modern System** | ShopKaro — Python FastAPI Microservices + HTML/CSS/JS |
| 🌐 **Frontend Pages** | 9 pages (Home, Products, Cart, Checkout, Admin, etc.) |
| ⚙️ **Backend Services** | 5 independent microservices |
| 🗄️ **Databases** | 5 SQLite databases (one per service) |
| 📊 **Diagrams** | 6 UML/Architecture diagrams |

---

## 🏛️ PART 1 — LEGACY SYSTEM (osCommerce)

osCommerce ek **real open-source e-commerce platform** hai jo 2000 se chal raha hai.

### ❌ Real Problems Found (with CVE references)

| # | Problem | File/Location | Severity |
|---|---------|---------------|----------|
| 1 | SQL Injection (CVE-2019-25496) | `product_info.php` | 🔴 Critical |
| 2 | SQL Injection (CVE-2019-25495) | `product_reviews_write.php` | 🔴 Critical |
| 3 | Remote Code Execution (CVE-2018) | `install/install_4.php` | 🔴 Critical |
| 4 | SQL Injection | `geo_zones.php` (zID parameter) | 🔴 Critical |
| 5 | Monolithic Architecture | Entire system | 🔴 Critical |
| 6 | PHP+HTML Mixed (Smarty) | `themes/` folder | 🟠 High |
| 7 | Single MySQL Database | `sql/` folder | 🟠 High |
| 8 | No REST API | All pages | 🟠 High |
| 9 | God Files (1000+ lines) | `admin/` folder | 🔴 Critical |
| 10 | No Modern Auth (no JWT) | `includes/` | 🟠 High |

### Real Vulnerable Code (osCommerce)
```php
// geo_zones.php — line 139 — REAL CODE
$zones_query_raw = "SELECT ... where a.geo_zone_id = " 
                   . $HTTP_GET_VARS['zID'];  // ← Direct injection!
```

📁 Full reference: [`legacy-system/LEGACY_REFERENCE.md`](legacy-system/LEGACY_REFERENCE.md)

---

## 🆕 PART 2 — MODERNIZED SYSTEM (ShopKaro)

### ✅ What We Built — Complete Re-Engineering

| Layer | Legacy (osCommerce) | ✅ ShopKaro (Modern) |
|-------|---------------------|---------------------|
| Frontend | Smarty templates (PHP+HTML) | Pure HTML5 + CSS3 + JavaScript |
| Backend | Monolithic PHP (Yii2) | 5 Python FastAPI microservices |
| Database | Single MySQL | 5 separate SQLite databases |
| Security | SQL Injection (3 CVEs) | Prepared statements + bcrypt |
| API | None — server rendered | REST API (JSON) |
| Auth | Session-based, no tokens | JWT-ready architecture |
| Pages | osCommerce default theme | 9 custom modern pages |
| Admin | Old admin/ folder | New admin dashboard |

---

## 📊 Architecture Diagrams

### 1️⃣ Frontend Sitemap
![Sitemap](./diagrams/01_Sitemap_Frontend.PNG)

### 2️⃣ Full System Architecture
![Architecture](diagrams/02_System_Architecture.PNG)

### 3️⃣ Database ER Diagram
![ER Diagram](diagrams/03_ER_Diagram.png)

### 4️⃣ Use Case Diagram
![Use Case](diagrams/04_Use_Case_Diagram.png)

### 5️⃣ Sequence Diagram — Place Order
![Sequence](diagrams/05_Sequence_Diagram_PlaceOrder.png)

### 6️⃣ Class Diagram
![Class Diagram](diagrams/06_Class_Diagram.png)

---

## 🌐 Frontend Pages (HTML + CSS + JavaScript)

| # | Page | File | Description |
|---|------|------|-------------|
| 1 | Home | `index.html` | Hero banner, categories, featured & new products |
| 2 | Products | `pages/products.html` | All 20 products, search, filter by category, sort |
| 3 | Product Detail | `pages/product-detail.html` | Single product view, ratings, related products |
| 4 | Cart | `pages/cart.html` | Cart items, quantity update, order summary |
| 5 | Checkout | `pages/checkout.html` | Delivery form, 4 payment methods |
| 6 | Order Success | `pages/order-success.html` | Order confirmation with ID |
| 7 | Login/Register | `pages/login.html` | Tab-based auth forms |
| 8 | My Account | `pages/account.html` | Profile, orders, wishlist, addresses |
| 9 | My Orders | `pages/orders.html` | Order history list |
| 10 | Admin Dashboard | `pages/admin/index.html` | Stats, recent orders, product table |

### Technologies Used
- **HTML5** — Semantic structure for all pages
- **CSS3** — Custom design system (`css/style.css`) — 600+ lines, responsive
- **JavaScript (Vanilla)** — `js/app.js` (cart, auth, toasts) + `js/data.js` (products data)
- **localStorage** — Demo data persistence (cart, users, orders)

---

## ⚙️ Backend Microservices (Python FastAPI)

| Service | Port | Database | Endpoints |
|---------|------|----------|-----------|
| User Service | 3001 | `users.db` | `/auth/register`, `/auth/login`, `/users/{id}` |
| Product Service | 3002 | `products.db` | `/products`, `/products/search/{kw}` |
| Cart Service | 3003 | `cart.db` | `/cart/{user_id}`, `/cart/{user_id}/add` |
| Order Service | 3004 | `orders.db` | `/orders`, `/orders/{id}`, `/orders/user/{id}` |
| Payment Service | 3005 | `payments.db` | `/payments/process`, `/payments/{id}/refund` |

### How to Run Backend
```bash
pip install fastapi uvicorn
cd backend/user-service
uvicorn main:app --reload --port 3001
```

---

## 🔧 Re-Engineering Strategy: Strangler Fig Pattern

```
osCommerce (PHP Monolith)
       │
       ▼
1. Architecture Recovery
   → Analyzed osCommerce structure
   → Found 10 problems + 3 CVEs
       │
       ▼
2. Design New Architecture
   → 5 Microservices (Python)
   → 9 Modern Frontend Pages
   → Per-service databases
       │
       ▼
3. Implementation
   → Built complete HTML/CSS/JS frontend
   → Built FastAPI backend services
   → Built SQLite databases with proper schema
       │
       ▼
ShopKaro — Modern Microservices System ✅
```

---

## 🔨 10 Refactoring Techniques Applied

| # | Technique | osCommerce Issue | Our Fix |
|---|-----------|-------------------|---------|
| 1 | Prepared Statements | SQL Injection (CVE-2019-25496) | Parameterized queries (`?`) |
| 2 | Microservices Split | Monolithic Yii2 app | 5 independent services |
| 3 | REST API Design | No API, server-rendered | Full JSON REST API |
| 4 | MVC Separation | Smarty mixed templates | Clean HTML/CSS/JS separation |
| 5 | DB Per Service | Single MySQL DB | 5 separate SQLite DBs |
| 6 | Password Hashing | Weak/plain passwords | SHA256/bcrypt hashing |
| 7 | Input Validation | No validation | Frontend + backend validation |
| 8 | Error Handling | Silent failures | try/catch + HTTPException |
| 9 | Repository Pattern | Direct queries everywhere | `database.py` per service |
| 10 | Responsive Design | Old fixed-width theme | Mobile-responsive CSS |

---

## 📁 Complete Project Structure

```
Modern eCommerce System/
│
├── 🌐 frontend/
│   ├── index.html
│   ├── css/style.css
│   ├── js/app.js, data.js
│   └── pages/
│       ├── products.html, product-detail.html
│       ├── cart.html, checkout.html, order-success.html
│       ├── login.html, account.html, orders.html
│       └── admin/index.html
│
├── ⚙️ backend/
│   ├── user-service/    (main.py + database.py)
│   ├── product-service/ (main.py + database.py)
│   ├── cart-service/    (main.py + database.py)
│   ├── order-service/   (main.py + database.py)
│   └── payment-service/ (main.py + database.py)
│
├── 🏛️ legacy-system/
│   └── LEGACY_REFERENCE.md  ← osCommerce analysis
│
├── 📊 diagrams/
│   ├── 01_Sitemap_Frontend.png
│   ├── 02_System_Architecture.png
│   ├── 03_ER_Diagram.png
│   ├── 04_Use_Case_Diagram.png
│   ├── 05_Sequence_Diagram_PlaceOrder.png
│   └── 06_Class_Diagram.png
│
└── 📄 docs/
    ├── ShopKaro_Report.pdf
    └── ShopKaro_Presentation.pptx
```

---

## 📈 Results Summary

```
osCommerce (Legacy)         ShopKaro (Modern)
────────────────────        ──────────────────
❌ 3 CVE vulnerabilities  →  ✅ Prepared statements
❌ Monolithic PHP         →  ✅ 5 Microservices
❌ Smarty templates       →  ✅ Clean HTML/CSS/JS
❌ Single MySQL DB        →  ✅ 5 SQLite DBs
❌ No REST API            →  ✅ Full REST API
❌ No admin dashboard     →  ✅ Modern admin panel
❌ Fixed-width design     →  ✅ Responsive design
❌ No documentation       →  ✅ Full README + Diagrams
```

---

*© 2026 SE-601 Software Re-Engineering | Karakoram International University | Shahgufta*
