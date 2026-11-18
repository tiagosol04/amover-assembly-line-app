<div align="center">

```
     ╔════════════════════════════════════════════════════════════════════╗
     ║                                                                    ║
     ║                     A - M O V E R                                  ║
     ║                                                                    ║
     ║                     A S S E M B L Y   L I N E                      ║
     ║                                                                    ║
     ╚════════════════════════════════════════════════════════════════════╝
```

### Assembly Line App — AJP Motorcycles
*Guided, step-by-step assembly for the shop floor — part by part, checklist by checklist.*

[![Android](https://img.shields.io/badge/Android-Kotlin-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#)
[![Jetpack Compose](https://img.shields.io/badge/Jetpack_Compose-4285F4?style=for-the-badge&logo=jetpackcompose&logoColor=white)](#)
[![MVVM](https://img.shields.io/badge/MVVM-Architecture-FF9800?style=for-the-badge)](#)
[![JWT](https://img.shields.io/badge/JWT-Auth-000000?style=for-the-badge&logo=jsonwebtokens)](#)

</div>

---

## 📱 What it is

**A-MoVeR Assembly Line** is a native Android app for **operators and mechanics on the assembly line**
at AJP Motorcycles (A-MoVeR project). It guides each motorcycle through the production flow —
identification, serialized parts, assembly checklist, quality control and packaging — and records
every step in the factory backend through the A-MoVeR REST API.

It is the **shop-floor counterpart** of the
[Factory Management app](https://github.com/tiagosol04/amover-factory-control-app): the management app
gives supervisors the macro view; this app gives operators the micro control.

---

## 🧭 Production flow

```
  ┌───────────┐   ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
  │   LOGIN   │──▶│  DASHBOARD   │──▶│  IDENTIFY    │──▶│ REGISTER VIN │
  │  (JWT)    │   │ orders / my  │   │  MOTORCYCLE  │   │ (frame / VIN)│
  └───────────┘   │  motorcycles │   │ QR / VIN     │   └──────┬───────┘
                  └──────────────┘   └──────────────┘          │
                                                               ▼
  ┌──────────────┐   ┌──────────────┐   ┌──────────────┐   ┌──────────────┐
  │  PACKAGING   │◀──│ FINAL QUALITY│◀──│ POST-ASSEMBLY│◀──│  ASSEMBLY    │
  │ & shipping   │   │   CONTROL    │   │  CHECKLIST   │   │ serialized   │
  │  confirmation│   │ approve/fail │   │              │   │ parts (SN)   │
  └──────────────┘   └──────────────┘   └──────────────┘   └──────────────┘
```

Each stage is validated before the operator can move to the next one, so production order is enforced
by the app and by the API.

---

## ⚡ Features

| Screen | What the operator does |
|---|---|
| **Login** | Signs in with the same credentials as the web platform (ASP.NET Identity + JWT). |
| **Dashboard** | Sees production orders and the motorcycles assigned to them. |
| **Identify motorcycle** | Reads the chassis QR code / VIN (hardware scanner input or manual entry) and finds the unit. |
| **Register VIN** | Associates the frame / VIN with the unit of a production order. |
| **Assembly** | Registers **serialized parts** (serial numbers) required by the model's parts template, with input validation. |
| **Post-assembly** | Completes the assembly checklist for the order. |
| **Final quality control** | Runs the control checklist — **approve**, **fail** or **fix** a defect. |
| **Packaging** | Confirms packaging and marks the unit as packed for shipping. |
| **Orders / order detail** | Lists orders, starts an order and follows its progress and summary. |

Shop-floor details:
- **Scanner-friendly input** — `ScannerInputHelper` cleans characters that HID barcode/QR readers inject
  (`\r`, `\n`, `\t`) and validates serial numbers and VINs before calling the API.
- **Haptic feedback** — short vibrations confirm success or signal errors (`HapticHelper`).
- **Readable errors** — API errors are mapped to clear messages in European Portuguese for operators.
- **Persistent session** — JWT stored with DataStore (`SessionManager`).
- **Step indicator** — a stepper shows where the unit is in the flow.

---

## 🏗 Architecture

```
┌──────────────────────────────────────────────────────────────┐
│ UI          Jetpack Compose · Material · Navigation Compose  │
│             10 routes (login → … → packaging)                │
├──────────────────────────────────────────────────────────────┤
│ ViewModel   AuthViewModel · OrdersViewModel · ProductionVM   │
├──────────────────────────────────────────────────────────────┤
│ Repository  AuthRepository · FactoryRepository               │
├──────────────────────────────────────────────────────────────┤
│ Network     Retrofit 2 · Gson · OkHttp logging · JWT header  │
├──────────────────────────────────────────────────────────────┤
│ Backend     A-MoVeR LCM API (ASP.NET Core · SQL Server)      │
└──────────────────────────────────────────────────────────────┘
```

### API endpoints used (23)

| Area | Endpoints |
|---|---|
| Auth | `POST api/Auth/login` |
| Production orders | list, detail, motorcycles of an order, add motorcycle, status, summary, **start**, **finish**, **mark as packed** |
| Motorcycles | detail, **find by VIN**, status, identification (VIN), serialized parts (list / register) |
| Models | serialized parts template |
| Checklists | list per order; update **assembly**, **packaging** and **control** items |
| Customer orders / users | list customer orders; motorcycles assigned to a user |

Backend: [amover-lcm-backend-api](https://github.com/tiagosol04/amover-lcm-backend-api).

---

## 🚀 Setup

**Requirements:** Android Studio (2024.x or newer), Kotlin, and the A-MoVeR API running locally (port `5137`).

The API base URL is defined per build type in `app/build.gradle.kts` (`BuildConfig.API_BASE_URL`):

| Build | URL |
|---|---|
| debug | `http://10.0.2.2:5137/` (Android emulator → host machine) |
| release | must be configured before publishing |

For a physical device on the same network, replace the debug URL with your computer's IP.

---

## 📁 Repository layout

```
app/                         ← current version of the app
LinhaMontagemAMOVER-main/    ← earlier snapshot of the same app (kept for reference)
```

---

## 🧩 A-MoVeR ecosystem

| Repository | Role |
|---|---|
| [amover-lcm-backend-api](https://github.com/tiagosol04/amover-lcm-backend-api) | ASP.NET Core REST API + SQL Server — the central data layer |
| [amover-factory-control-app](https://github.com/tiagosol04/amover-factory-control-app) | Android app for managers, supervisors and quality |
| **amover-assembly-line-app** | Android app for assembly-line operators (this repository) |
| [mobileuserapi-microservices-backend](https://github.com/tiagosol04/mobileuserapi-microservices-backend) | .NET 8 gRPC microservices prototype for the rider app (My Fulgora) |

<div align="center">

*Developed within the A-MoVeR project (UTAD × AJP Motorcycles), Vila Real / Penafiel, Portugal.*

</div>
