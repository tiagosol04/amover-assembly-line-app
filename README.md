
```
     ╔════════════════════════════════════════════════════════════════════╗
     ║                                                                    ║
     ║      █████╗       ███╗   ███╗  ██████╗ ██╗   ██╗ ███████╗██████╗   ║
     ║     ██╔══██╗      ████╗ ████║ ██╔═══██╗██║   ██║ ██╔════╝██╔══██╗  ║
     ║     ███████║█████╗██╔████╔██║ ██║   ██║██║   ██║ █████╗  ██████╔╝  ║
     ║     ██╔══██║╚════╝██║╚██╔╝██║ ██║   ██║╚██╗ ██╔╝ ██╔══╝  ██╔══██╗  ║
     ║     ██║  ██║      ██║ ╚═╝ ██║ ╚██████╔╝ ╚████╔╝  ███████╗██║  ██║  ║
     ║     ╚═╝  ╚═╝      ╚═╝     ╚═╝  ╚═════╝   ╚═══╝   ╚══════╝╚═╝  ╚═╝  ║
     ║                                                                    ║
     ║                     A S S E M B L Y   L I N E                      ║
     ║                                                                    ║
     ╚═══════════════════════════════════════════════════════════════════ ╝
```

### Mobile Management App — AJP Motorcycles

*A 360° view of the factory, in the manager's pocket.*

[![Android](https://img.shields.io/badge/Android-Kotlin-3DDC84?style=for-the-badge&logo=android&logoColor=white)](#)
[![Jetpack Compose](https://img.shields.io/badge/Jetpack_Compose-4285F4?style=for-the-badge&logo=jetpackcompose&logoColor=white)](#)
[![MVVM](https://img.shields.io/badge/MVVM-Architecture-FF9800?style=for-the-badge)](#)
[![JWT](https://img.shields.io/badge/JWT-Auth-000000?style=for-the-badge&logo=jsonwebtokens)](#)

---

</div>

## 📱 What it is

**A-MoVeR Factory Management** is a native Android app for **managers, supervisors and quality leads** at AJP Motorcycles. It's the mobile companion to the web platform — bringing all production, service, warranty and team information to the phone, enabling real-time decisions without being tied to a computer.

```
  ┌──────────────────────────────────────────────────────────────────┐
  │                                                                  │
  │   📊 DASHBOARD    →   Instant view of the whole factory          │
  │   🏭 PRODUCTION   →   Orders, states, checklists, parts          │
  │   🔧 SERVICES     →   Maintenance, breakdowns, warranties        │
  │   📦 ORDERS       →   Customer order pipeline                    │
  │   📈 TRACKING     →   Full history per unit / VIN                │
  │   👥 TEAM         →   Availability and workload                  │
  │   👤 PROFILE      →   Session, roles, preferences                │
  │                                                                  │
  └──────────────────────────────────────────────────────────────────┘
```

---

## ⚡ Features

### 🎯 Operational Dashboard

The dashboard doesn't show generic numbers — it shows **what needs attention right now**:

| Indicator | What it means |
|-----------|----------------|
| **Blocked orders** | Production stopped — needs an immediate decision |
| **No unit registered** | Units in production without traceability |
| **VIN pending** | Frame not closed out — a risk for shipping |
| **Control pending** | Almost ready, missing final validation |
| **Open services** | Maintenance and warranties still unresolved |
| **Team unavailable** | Insufficient shift coverage |

The dashboard computes **immediate actions** and sorts them by priority. Factory zones (Assembly, Packaging, Control, Exceptions) show live workload.

### 🏭 Production

- Order list with filters (state, model, priority)
- Full **Operational Sheet** per order:
  - Traceability gates (Unit ✓ → VIN ✓ → Quality ✓)
  - Checklist status (assembly, packaging, control)
  - Context (customer, model, destination)
  - **Start** and **Finish** an order via the API with full validation
- Risk summary and suggested next action

### 🔧 Services, Maintenance & Warranties

A complete after-sales module:

```
                    ┌──────────────────┐
                    │  SERVICES LIST   │
                    │  KPIs + Filters  │
                    │  + VIN search    │
                    └────────┬─────────┘
                             │
                    ┌────────▼─────────┐
                    │ SERVICE DETAIL   │
                    │ ┌──────────────┐ │
                    │ │ Unit info    │ │
                    │ │ Type/State   │ │
                    │ │ Changed parts│ │
                    │ │ Notes        │ │
                    │ └──────────────┘ │
                    │ ┌──────────────┐ │
                    │ │ Common       │ │
                    │ │ issues for   │ │
                    │ │ the model    │ │
                    │ └──────────────┘ │
                    │ ┌──────────────┐ │
                    │ │  Actions:    │ │
                    │ │ Start        │ │
                    │ │ Complete     │ │
                    │ └──────────────┘ │
                    └──────────────────┘
```

**8 service types**: Maintenance, Breakdown, Warranty, Inspection, Diagnosis, Prep/Delivery, Technical Campaign, Other

**Per-model analysis**: common issues grouped together + total warranties — surfacing patterns and enabling engineering decisions.

### 📦 Orders

A view of the commercial pipeline:
- KPIs: Pending / In production / Completed
- Customer, model, quantity, delivery date
- Accessible via a top-bar shortcut (for managers/admins)

### 📈 Tracking (History)

- Search by order, VIN or destination
- Filters: With VIN, Completed, With services
- Technical summary per unit: model, VIN, country, services, checklist status

### 🔐 Role System

The app adapts to the user's profile:

| Profile | Dashboard | Production | Services | Orders | Team | Tracking |
|--------|:---------:|:----------:|:--------:|:------:|:----:|:--------:|
| **Administration** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Supervisor** | ✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| **Quality** | ✅ | ✅ | ✅ | — | ✅ | ✅ |
| **After-sales** | — | ✅ | ✅ | — | ✅ | ✅ |
| **Operator** | — | ✅ | ✅ | — | ✅ | — |

The bottom bar shows only the modules the profile can access. Top-bar shortcuts for orders, incidents and team appear only for those allowed to see them.

---

## 🏗 Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                      UI LAYER                               │
│   Jetpack Compose · Material 3 · Role-based navigation      │
│                                                              │
│   ┌───────────┐ ┌──────────┐ ┌──────────┐ ┌────────────┐   │
│   │ Dashboard │ │Production│ │ Services │ │   Orders   │   │
│   └───────────┘ └──────────┘ └──────────┘ └────────────┘   │
│   ┌───────────┐ ┌──────────┐ ┌──────────┐                  │
│   │  Tracking │ │   Team   │ │ Profile  │                  │
│   └───────────┘ └──────────┘ └──────────┘                  │
├─────────────────────────────────────────────────────────────┤
│                   VIEWMODEL LAYER                           │
│   DashboardRealVM · OrdensRealVM · OrdemDetalheRealVM        │
│   ServicosVM · ServicoDetalheVM · EncomendasVM               │
│   AlertasVM · HistoricoVM · EquipaVM · PerfilRealVM          │
├─────────────────────────────────────────────────────────────┤
│                   REPOSITORY LAYER                          │
│   FabricaRepository (interface) → FabricaRepositoryImpl      │
│   AuthRepository (interface) → AuthRepositoryImpl            │
├─────────────────────────────────────────────────────────────┤
│                    NETWORK LAYER                            │
│   Retrofit 2 · OkHttp · JWT Interceptor · DataStore         │
│   ApiService (65+ mapped endpoints)                          │
├─────────────────────────────────────────────────────────────┤
│                     BACKEND                                 │
│   A-MoVeR API (ASP.NET Core) · SQL Server · Identity + JWT  │
└─────────────────────────────────────────────────────────────┘
```

### Principles

- **MVVM** with a full UI ↔ Logic ↔ Data separation
- **StateFlow** for reactive state — the UI recomposes automatically
- **Repository Pattern** — the UI never touches the API directly
- **Role-Based Access** — navigation and features adapt to the JWT profile
- **Offline-Resilient** — the token persists in DataStore, the session survives restarts

---

## 📁 Project Structure

```
app/src/main/java/com/example/aplicacaodecontrolofabrica/
│
├── auth/
│   ├── AuthDataStore.kt              ← JWT persistence
│   ├── AuthHeaderInterceptor.kt      ← Injects the token into requests
│   ├── AuthFailureInterceptor.kt     ← Handles 401/403
│   └── UserSession.kt                ← Session data
│
├── data/
│   ├── dto/
│   │   ├── AuthDtos.kt              ← Login/Me
│   │   ├── OrdemDtos.kt             ← Orders + Summary
│   │   ├── ServicoDtos.kt          ← 15+ service DTOs ★
│   │   ├── EncomendasAlertasDto.kt  ← Orders
│   │   ├── ChecklistDtos.kt        ← Checklists
│   │   ├── MotaPecasDtos.kt        ← Units + Serialized parts
│   │   ├── UtilizadorDtos.kt       ← Users + Assignments
│   │   ├── ModelosDtos.kt          ← Vehicle models
│   │   ├── ClientesDtos.kt         ← Customers
│   │   └── ExtraDtos.kt            ← Generic requests
│   ├── model/                       ← UI domain models
│   │   ├── Servico.kt              ← 8 types, 3 states, coverage
│   │   ├── RoleAccessUi.kt         ← 6 operational profiles ★
│   │   ├── Alerta.kt               ← Incidents with severity
│   │   └── ...
│   ├── mapper/
│   │   ├── DtoHelpers.kt           ← Safe DTO→UI conversions
│   │   └── DtoMappers.kt           ← Complex mappings
│   └── repository/
│       ├── FabricaRepository.kt     ← Interface (40+ methods)
│       ├── FabricaRepositoryImpl.kt ← Implementation
│       ├── AuthRepository.kt        ← Auth interface
│       ├── AuthRepositoryImpl.kt    ← Auth implementation
│       └── ServiceLocator.kt        ← Manual DI
│
├── features/
│   ├── cockpit/
│   │   ├── Dashboard.kt            ← 515 lines of UI ★
│   │   └── DashboardRealViewModel.kt ← Zones, KPIs, actions
│   ├── operacao/
│   │   ├── OperacaoScreen.kt       ← Order list
│   │   ├── FichaOperacionalScreen.kt ← Detail + start/finish ★
│   │   ├── OrdensRealViewModel.kt   ← List with filters
│   │   └── OrdemDetalheRealViewModel.kt ← Start/Finish/VIN ★
│   ├── servicos/                    ★ NEW
│   │   ├── ServicosScreen.kt        ← List + KPIs + filters
│   │   ├── ServicosViewModel.kt     ← Search + filters
│   │   ├── ServicoDetalheScreen.kt  ← Detail + model issues
│   │   └── ServicoDetalheViewModel.kt ← Loads service + analysis
│   ├── encomendas/                  ★ NEW
│   │   ├── EncomendasScreen.kt      ← Order pipeline
│   │   └── EncomendasViewModel.kt   ← Resolves customers/models
│   ├── alertas/
│   ├── historico/
│   ├── equipa/
│   ├── perfil/
│   └── login/
│
├── network/
│   ├── ApiService.kt               ← 65+ endpoints ★
│   ├── ApiModule.kt                ← Retrofit configuration
│   ├── ApiConfig.kt                ← Base URL
│   └── UiErrors.kt                 ← Error handling
│
├── ui/
│   ├── components/                  ← 8 reusable components
│   └── theme/                       ← Customized Material 3
│
├── di/
│   └── ViewModelFactory.kt         ← 11 registered ViewModels
│
├── AppNavigation.kt                ← 10 routes + role-based nav ★
└── MainActivity.kt
```

---

## 🔌 API Coverage

The app consumes **65+ endpoints** from the A-MoVeR API:

| Module | Endpoints | Description |
|--------|:---------:|-----------|
| **Auth** | 2 | JWT login + profile |
| **Orders** | 9 | CRUD + start + finish + summary + units |
| **Units** | 10 | CRUD + VIN + serialized parts + summary + state |
| **Checklists** | 4 | Per order, individual toggle by type |
| **Services** | 14 | CRUD + states + changed parts + history by unit/VIN/model + common issues + warranties |
| **Orders (customer)** | 4 | CRUD + filters |
| **Users** | 5 | CRUD + assigned units + status |
| **Models** | 2 | List + detail |
| **Customers** | 2 | List + detail |
| **Parts** | 1 | Catalog |

---

## 🚀 Setup

### Prerequisites

- Android Studio Hedgehog+ (2024.x)
- Kotlin 1.9+ / Compose BOM 2024.09
- A-MoVeR API running (port 5137)

### Configuration

1. **Clone the repository**
2. **Check the API URL** in `build.gradle.kts`:
   ```kotlin
   buildConfigField("String", "API_BASE_URL", "\"http://10.0.2.2:5137/\"")
   ```
3. **Build & Run**
4. **Log in** with the web platform's credentials (same Identity system)

---

## 🧩 Relationship with the Ecosystem

```
  ┌─────────────────────────┐
  │     WEB APP (Desktop)   │  ← Full management: orders,
  │     ASP.NET Core MVC    │     models, parts, documents,
  │     + Razor Views       │     purchasing, received goods
  └───────────┬─────────────┘
              │
  ┌───────────▼─────────────┐
  │      A-MoVeR API        │  ← Central data layer
  │      ASP.NET Core       │     JWT Auth · SQL Server
  │      Web API            │     65+ REST endpoints
  └───────────┬─────────────┘
              │
    ┌─────────┴──────────┐
    │                    │
    ▼                    ▼
  ┌────────────┐   ┌─────────────────┐
  │ MANAGEMENT │   │ ASSEMBLY LINE   │
  │    APP     │   │      APP         │
  │ (this app) │   │                 │
  │            │   │ Operators       │
  │ Managers   │   │ Shop floor      │
  │ Supervision│   │ Tablet/Scanner  │
  │ Quality    │   │                 │
  └────────────┘   └─────────────────┘
```

The **Management App** and the **Assembly Line App** are complementary:
- The management app gives the **macro view** — dashboard, metrics, decisions
- The line app gives the **micro control** — part by part, checklist by checklist
- Both read and write the same data via the API
- A change on the line shows up in the manager's dashboard in real time

---

## 🔮 Roadmap

- [ ] Push notifications for critical alerts (blocked orders, warranties)
- [ ] Production charts (units/week, average time per order)
- [ ] Offline mode with automatic sync
- [ ] PDF report export
- [ ] PHC integration (invoicing) to avoid duplicating data
- [ ] QR code scanning for quick access to an order/unit
- [ ] Android widget for KPIs on the home screen

---

<div align="center">

```
  The factory in the palm of your hand.

  AJP Motorcycles × Project A-MoVeR
  Penafiel, Portugal · 2025
```

</div>
