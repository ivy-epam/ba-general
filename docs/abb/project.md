# EasyOrder China Project

**Last Updated:** 2026-10-09

## Overview

EasyOrder is an enterprise-grade digital platform designed to streamline ordering and operational processes across global markets. It represents a strategic initiative to enhance customer experience, operational efficiency, and business scalability.

- **Infrastructure:** Separate China and Global deployments as per regulatory requirements
- **Focus:** Primarily focused on China EO initiative
- **Timeline:** CBOL decommissioning target: end of 2026

## Strategic Context

### Legacy System (cBOL)

cBOL is a bespoke B2B Commerce solution built by ABB serving as the primary digital sales channel in 40+ markets. While it has a long development history and rich feature set, it faces significant challenges:

**Current State Issues:**
- 58% of cBOL users find the experience unfriendly
- Performance issues leading to user dissatisfaction
- Manual order placement preferred by some users due to platform friction
- Missing modern B2B Commerce features (product recommendations, returns management, personalized experiences)

### Migration Strategy

The platform is being migrated from cBOL to a new modernized system module-by-module, with cBOL decommissioned by year-end 2026.

## Migration Scope

The scope focuses on rebuilding three critical cBOL journeys:

1. **Cart & Ordering** — core transactional workflow
2. **Price & Availability Check** — product information and fulfillment capabilities
3. **Order Management** — order lifecycle and post-purchase operations

## One High-Value Initiatives

### 1. Platform 2.0
Revamped e-commerce experience featuring:
- Modern visual design
- Brand-new cloud-native architecture

## Primary Challenges Addressed

### Architecture & Performance
- cBOL architecture no longer fit for purpose
- Extremely slow performance
- Challenges in maintenance and scaling

### User Experience
- Inconsistent, confusing user experience
- Missed opportunities and cart abandonment
- Performance frustration driving users to non-digital channels

### Organizational Capability
- cBOL team structure unable to meet growing business requirements
- Silos creating duplicate effort and missed opportunities
- Lack of knowledge sharing across markets

### Market Positioning
- Growing customer expectations unmet across platforms
- Increased support burden on ABB teams
- Competitive pressure as customers consider alternatives

## Proposed Solution Architecture

The new solution is built on the following architectural principles:

### Microservices
- Small, independently deployable and maintainable applications
- Enables modular development and scaling

### API-First Integration
- Omnichannel, reusable, scalable, versioned APIs
- Centrally managed for consistency

### Event-Driven Communication
- Event broker as primary data exchange mechanism between microservices
- Ensures loose coupling and flexibility

### Microfrontends
- Small, cohesive UIs deployed and maintained independently
- Completely decoupled from the backend

### Expected Benefits

By adhering to these principles, the solution enables:

- **Increased speed of innovation** — modular approach reduces time-to-market
- **Native cloud readiness** — cloud-native architecture supports scalability
- **High performance, availability, scalability, and cost efficiency** — optimized for modern cloud operations

## Project Goals

Build a solid UX scoped to the mentioned new journeys while establishing a technical foundation for a best-in-class e-commerce experience that supports future expansion beyond.
