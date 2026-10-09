# ABB EasyOrder — System Architecture Reference

> Purpose: System context knowledge for agents performing incident analysis, troubleshooting, and operational tasks on the ABB EasyOrder platform.

---

## 1. System Overview

ABB EasyOrder is an e-commerce platform for ABB's Electrification business, serving customers globally with product search, availability checks, order placement, and order management. It evolved from a monolithic application called **CBOL** (ASP.NET Web Forms → MVC) into a **microservices-based architecture** built on Azure.

EasyOrder is a React SPA backed by a C# ASP.NET  Core BFF. 

**Key distinction — CBOL vs EasyOrder (EO):**
- URLs containing `/cBOL_Application/` are CBOL pages (managed by the CBOL/One4 team)
- URLs containing `/ebusiness/` are EasyOrder pages (managed by the EPAM support team)

---

## 2. Geographies & Environments

The platform operates across **two Azure regions**: West Europe and China.

- Subject to the **Great Firewall of China (GFW)** — strict cross-border traffic controls
- DR via **Azure Availability Zones** (zone-redundant deployments, no separate DR region)
- Cosmos DB configured with Availability Zone support for automatic failover

---

## 3. Tech Stack

| Layer | Technology |
|-------|------------|
| Frontend | React with TypeScript |
| Backend | .NET 8 with C# |
| Container Orchestration | Azure Kubernetes Service (AKS) |
| Database | Azure Cosmos DB |
| Messaging | Azure Service Bus |
| Storage | Azure Storage |
| Secrets | Azure Key Vault |
| Service Mesh | Istio |
| Monitoring | Azure App Insights, Dynatrace, Splunk |
| Security Scanning | WIZ |

---

## 4. Network Architecture

### Inbound Traffic
- **West Europe:** Requests enter via **F5 Load Balancer** (managed by ABB Network team)
- **China:** Requests routed through **Wangsu Firewall** (replaced Akamai for compliance; managed by Wipro). Uses **Application Gateway** for traffic routing.

### Outbound Traffic
- All outbound connections to public internet go through **Zscaler** network proxy (secure, policy-compliant access)

### Private Network Communication
- Communication with private networks (e.g., SAP, internal systems) secured by **Checkpoint Firewall** (traffic inspection and access control)

### Network Ownership
- Cloud network changes: TCS team
- Zscaler: ABB and Wipro teams

---

## 5. Application Components (Microservices)

| Service | Purpose (Inferred) |
|---------|---------------------|
| `abb-mvp-fe-app` | Main frontend application |
| `abb-fe-punchout` | Punchout frontend (procurement integration) |
| `abb-bff` | Backend-for-Frontend gateway |
| `abb-auth-entrypoint-service` | Authentication and entry point |
| `abb-customer-service` | Customer data management |
| `abb-product-service` | Product catalog and search |
| `abb-availability-service` | Product availability checks |
| `abb-cart-service` | Shopping cart |
| `abb-order-service` | Order creation and management |
| `abb-order-processing-service` | Order processing pipeline |
| `abb-order-asyncprocessing-service` | Async order processing |
| `abb-order-attachments-service` | Order document attachments |
| `abb-commerce-service` | Core commerce logic |
| `abb-configuration-service` | Application configuration |
| `abb-email-service` | Email notifications |
| `abb-sap-services` | SAP integration layer |
| `abb-reports-service` | Reporting |
| `abb-contentful-worker` | CMS content sync (Contentful) |
| `abb-localization-exporter-worker` | Localization/translation export |
| `abb-training-exporter-worker` | Training data export |
| `abb-easyorder-newsmanagement-service` | News/announcements management |
... (Note: this is not an exhausted list)

---

## 6. External Dependencies - Important

| System | Role |
|--------|------|
| **SAP** | Order creation, order data, fulfillment (SI2001 team) |
| **PIS (Product Information Service) TnB** | Product information source |
| **CBOL** | Legacy system, still active for some pages and China order management |
| **E Configure** | Product configuration |
| **Contentful** | Content management (inferred from contentful-worker) |

### 6.1 Dependency Criticality and Failure Impact

| Dependency | Integration Type | Core EO Modules Affected | Typical User Impact |
|------------|------------------|--------------------------|---------------------|
| **SAP** | Synchronous API + async processing | `abb-order-service`, `abb-order-processing-service`, `abb-order-asyncprocessing-service`, `abb-sap-services` | Order submission fails, delayed confirmations, missing order history updates |
| **PIS TnB** | API/data service | `abb-product-service`, `abb-availability-service`, `abb-commerce-service` | Product search incomplete, missing SKU details, incorrect availability |
| **CBOL** | Redirect/session handoff | `abb-mvp-fe-app`, `abb-bff`, routing/config services | Users routed to wrong experience, China order management disruption |
| **E Configure** | Product configuration API | `abb-product-service`, `abb-cart-service`, `abb-commerce-service` | Configurable products cannot be configured or added to cart |
| **Contentful** | Content fetch/sync worker | `abb-contentful-worker`, FE content rendering paths | CMS-driven content stale or unavailable (banners/help/news text) |

### 6.2 External Dependency Boundaries (for Incident Isolation)

1. **In-platform responsibility (EO/EPAM):**
	- Frontend rendering, BFF orchestration, internal microservice routing, retries/circuit breakers, local validation, queue processing in AKS.
2. **Shared boundary responsibility:**
	- Network path via F5/Wangsu/App Gateway/Zscaler/Checkpoint, DNS, certificates, firewall rules, and identity/token trust chains.
3. **External-system responsibility:**
	- SAP business APIs and downstream processing, PIS source quality/availability, CBOL runtime behavior, E Configure responses, Contentful tenant/API health.

This split should be used during first-touch triage to avoid treating external outages as internal code defects.

### 6.3 Module-to-External-System Root Cause Matrix

| Symptom Reported | Primary EO Module(s) to Check First | Likely External System | Fast Validation Clues |
|------------------|-------------------------------------|------------------------|-----------------------|
| "Cannot place order" / HTTP 5xx at submit | `abb-order-service`, `abb-sap-services`, `abb-order-processing-service` | **SAP** | Spike in SAP connector failures, timeout patterns, no order ID returned |
| "Order placed but status not updating" | `abb-order-asyncprocessing-service`, `abb-reports-service` | **SAP** | Queue backlog grows while EO core is healthy; delayed SAP callbacks/data sync |
| "Products missing in search" | `abb-product-service`, `abb-commerce-service` | **PIS TnB** | FE and BFF healthy, but product payloads empty/partial from PIS |
| "Availability differs from expected" | `abb-availability-service` | **PIS TnB** (or SAP depending flow) | Availability endpoint latency/errors with normal cart/order service health |
| "Configurable item cannot be configured" | `abb-product-service`, `abb-cart-service` | **E Configure** | Config API call failures or malformed configuration response |
| "Redirect sends me to wrong app/page" | `abb-mvp-fe-app`, `abb-bff`, config service | **CBOL** (plus routing config) | Redirect rules/session handoff errors; path switches between `/ebusiness/` and `/cBOL_Application/` |
| "News/content block missing" | FE rendering path + `abb-contentful-worker` status | **Contentful** | Worker sync lag, fetch errors, content version mismatch |

### 6.4 External Dependency Triage Playbook (Initial Incident Analysis)

1. **Identify business capability impacted:**
	- Auth, product discovery, availability, cart, order submit, order history, content.
2. **Map capability to EO module set:**
	- Use Section 5 module list and the matrix above to pick 1-3 candidate services.
3. **Classify failure mode quickly:**
	- `Timeout` -> often network path or external latency.
	- `4xx functional error` -> contract/payload/config mismatch.
	- `5xx burst` -> dependency outage or integration component regression.
	- `Partial degradation` -> async backlog or region-specific dependency issues.
4. **Correlate internal vs external health signals:**
	- If EO pods are healthy but connector errors spike, suspect external dependency.
	- If only China/WE is affected, prioritize regional network boundary checks.
5. **Assign preliminary root-cause domain:**
	- `EO Internal`, `Network Boundary`, or `External System`.
6. **Escalate with dependency-specific evidence bundle:**
	- Timestamp (UTC), impacted region, endpoint/operation, correlation IDs, error rates, sample payload metadata (non-PII), and retry behavior.

### 6.5 Region-Specific Dependency Risk Notes

- **China region** has additional routing and integration constraints (GFW, Wangsu, local network controls), so dependency incidents may present as network timeouts even when external systems are healthy globally.
- **West Europe** has better observability coverage in Splunk/WIZ, which can make dependency attribution faster.
- For cross-region comparison, use "same operation, same time window" checks to distinguish global external outages from region-local network issues.

---

## 7. Application Flows

### Authentication Flow
1. User enters credentials → UI sends login request to API
2. API validates credentials against identity provider
3. Valid → Token issued → User redirected to dashboard
4. Invalid → Error message displayed

### End-to-End Order Flow
1. User authenticates → Dashboard loads
2. User searches for account → Redirected to EO or CBOL based on configuration
3. User performs actions: Search Products / Check Availability / Add to Cart / View Order History
4. Request sent to backend API → Business validation → Data processed
5. Order created in SAP → Order ID generated → Confirmation returned to UI

### Order Management
- **West Europe:** System loads last 15 orders; user can filter by Order No, Date, Status; data fetched from SAP backend
- **China:** Managed by CBOL team; similar to WE but includes Sales Office filter option

### Product Search
- User searches via menu search bar → Backend fetches data → Results in dropdown list → Click navigates to Product Detail page

---

## 9. Infrastructure Ownership

| Area | Owner |
|------|-------|
| Azure cloud infrastructure (AKS, storage, PaaS) | EPAM |
| CI/CD pipelines, releases, deployments | Deloitte |
| Network, Firewall, Proxy | TCS / ABB / Wipro |
| CBOL infrastructure (China) | CBOL team (One4) |
| L1 monitoring | Wipro |
| SAP | SI2001 team |
| Zscaler | ABB + Wipro |

> EPAM scope excludes: Network, Firewall, Proxy, and CBOL Infrastructure in China.

---
