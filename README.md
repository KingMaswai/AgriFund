# 🌱 AgriFund - Smart Agricultural Credit & AgriScore Platform

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![NASA POWER API](https://img.shields.io/badge/NASA%20POWER-Agroclimatology-0284c7)](https://power.larc.nasa.gov/)
[![Supabase Auth](https://img.shields.io/badge/Supabase-Unified%20Auth-3ecf8e)](https://supabase.com/docs/guides/auth)
[![Zero-Default Architecture](https://img.shields.io/badge/DZDA-0.00%25%20Default-059669)](#deterministic-zero-default-architecture-dzda)

AgriFund is an agricultural credit assessment and risk management platform designed for the African smallholder ecosystem. It bridges the gap between commercial banks, smallholder farmers, and agricultural extension officers through real-time satellite agroclimatology, closed-loop M-Pesa escrow disbursements, and a 100-point standardized credit evaluation rubric.

---

## 🌟 Key Features

### 1. Unified Authentication (Supabase Auth)
Rather than maintaining fragmented login portals, AgriFund employs a **single, unified login pool** powered by [Supabase Auth](https://supabase.com/docs/guides/auth) with role-based routing for:
* 👨‍🌾 **Farmers:** Full Name, National ID, Phone Number, County, Email, Mpesa Number / Preferred Payment Method, Farm Size, Crop.
* 🏛️ **Administrators:** Full Name, Official Email, Phone Number, Employee ID, Department.
* 🔬 **Agricultural Extension Officers:** Full Name, Phone Number, Email, Staff/Employer ID, Organization/Institution (e.g., KALRO), County, Verification Status, Specialization.
* 🏦 **Banks:** Bank Name, Bank Registration Number, Head Office Address, Official Email, Official Phone Number, Partnership Status (`Pending`, `Active`, `Suspended`).

### 2. Live NASA POWER Agroclimatology & 20-Point Climate Rubric
Directly queries the [NASA POWER Daily API](https://power.larc.nasa.gov/api/pages/) using coordinates for Kenyan counties (Nakuru, Uasin Gishu, Kiambu, Machakos, Meru, Trans Nzoia, etc.) to assess:
* **Rainfall suitability (Max 7 pts):** Analyzes seasonal rainfall depth and coefficient of variation against crop water demand curves ($ET_c$).
* **Temperature suitability (Max 5 pts):** Validates mean 2m air temperature against optimal crop thermal envelopes ($18^\circ\text{C} - 28^\circ\text{C}$).
* **Drought and extreme-weather exposure (Max 5 pts):** Tracks maximum consecutive dry spells ($P < 1\text{mm}$) and flash storm frequency.
* **Environmental resilience (Max 3 pts):** Verifies on-farm adaptive infrastructure (drip irrigation, mulching, water retention ponds).
* **Climate Subtotal: 20 Points.**

### 3. Comprehensive 100-Point AgriScore Rubric
An institutional-grade credit appraisal model:
1. **Climate & Agro-Ecological Risk (NASA POWER):** 20 Points
2. **Financial Track Record & M-Pesa Mobile Money Flows:** 25 Points
3. **Agronomic Capacity & Land Tenure:** 20 Points
4. **Extension Officer Field Audit & Ground Verification:** 20 Points
5. **Off-Take Contracts & Parametric Micro-Insurance:** 15 Points

**Credit Rating Policy:**
* **Grade A (85 – 100):** Prime Low Risk · Instant disbursement · $9.5\%$ p.a.
* **Grade B (70 – 84):** Standard Low Risk · Standard terms · $11.5\%$ p.a.
* **Grade C (50 – 69):** Conditional Approval · Extension officer co-monitoring · $14.0\%$ p.a.
* **Grade D (< 50):** High Risk · Agronomic remediation required.

### 4. Deterministic Zero-Default Architecture (DZDA)
The platform operationally decouples debt service from individual farmer discretion:
* **0% Fund Diversion:** Loans are disbursed as encrypted M-Pesa digital vouchers redeemable exclusively at certified KALRO agro-dealers for seeds and fertilizers.
* **Parametric Micro-Insurance Trigger:** If NASA POWER satellite telemetry detects rainfall $< 220\text{mm}$ or dry spells $> 21\text{ days}$, insurance automatically indemnifies the bank loan balance.
* **Tripartite Contract Off-Take Floor:** Guaranteed buyer agreements (e.g., Unga Group, Twiga Foods) eliminate commodity price drop exposure.
* **Custodian Escrow Split Settlement:** Buyer pays into a bank escrow account where loan principal + interest is deducted first, and net profit is sent to the farmer's M-Pesa.

$$\text{Coverage} = \frac{(Y_{\text{actual}} \cdot P_{\text{floor}}) + \text{Indemnity}_{\text{NASA}}}{L_{\text{due}}} \ge 1.00 \implies \mathbf{P(\text{Default}) = 0.00\%}$$

---

## 🚀 Quick Start

### Prerequisites
* [Node.js](https://nodejs.org/) (v18 or newer)
* Modern web browser

### Running the App
1. Clone the repository:
   ```bash
   git clone https://github.com/KingMaswai/AgriFund.git
   cd AgriFund
   ```
2. Start the server:
   ```bash
   node server.js
   ```
3. Open your browser:
   ```
   http://localhost:3000
   ```

---

## 📁 Project Structure

```
├── DOCUMENTATION_PROOF_OF_NON_DEFAULT.md  # Comprehensive underwriting whitepaper
├── README.md                              # Project overview and documentation
├── .gitignore                             # Clean Git ignore file
├── server.js                              # Node.js server with NASA POWER API bridge
└── public/
    ├── index.html                         # Full single-page dashboard UI
    ├── app.js                             # Client-side logic, charts & Supabase auth
    └── styles.css                         # Custom styling & print layout
```

---

## 📜 Regulatory References
* **Central Bank of Kenya (CBK):** Prudential Guidelines on Agricultural Credit Risk Mitigation.
* **NASA POWER Project:** NASA Langley Research Center Agroclimatology Archive.
* **KALRO:** Kenya Agricultural & Livestock Research Organization Agro-Ecological Standards.

---

**Developed for KingMaswai / AgriFund**
