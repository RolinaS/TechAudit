# TechAudit – Security & Technology Lifecycle Monitoring Platform

## 📌 Overview

TechAudit is a centralized security and technology lifecycle monitoring platform designed to provide continuous visibility over infrastructure environments.

It enables organizations to:

- Monitor installed software versions across machines
- Detect outdated or unsupported technologies (EOL)
- Identify known vulnerabilities (CVE)
- Track security posture evolution over time
- Receive upgrade recommendations
- Maintain a continuous security overview dashboard

This project is built with a modern, enterprise-ready stack using:

- **Next.js** (Frontend)
- **Spring Boot** (Backend API)
- **PostgreSQL** (Database)
- **Keycloak** (Authentication & Authorization)
- **Docker Compose** (Containerized deployment)

---

## 🎯 Objectives

The goal of TechAudit is to:

- Provide centralized security visibility
- Detect obsolete technologies before they become a risk
- Assist IT governance and upgrade planning
- Support DevOps and security best practices
- Offer a structured audit history for compliance needs

---

## 🏗 Architecture

### Frontend
- Next.js (App Router)
- Dashboard & visualization components
- Role-based UI
- Secure authentication via Keycloak (OIDC)

### Backend
- Spring Boot 3 (Java 21)
- REST API
- JPA / Hibernate
- Scheduled jobs for periodic checks
- Security via JWT Resource Server
- Role-based access control

### Database
- PostgreSQL
- Structured schema for machines, software, vulnerabilities and audit history

### Authentication
- Keycloak (OIDC)
- Roles:
  - `ROLE_ADMIN`
  - `ROLE_SECURITY`
  - `ROLE_VIEWER`

### Deployment
- Docker Compose
- One service per container:
  - `frontend`
  - `api`
  - `db`
  - `keycloak`
  - `keycloak-db`

---

## 🧠 Core Features

### 🖥 Machine Monitoring
- Register machines (prod/dev/test)
- Track installed software versions
- Record last audit timestamp

### 📦 Technology Tracking
- Detect version differences
- Identify EOL dates
- Highlight upgrade recommendations

### 🔐 Vulnerability Detection
- Associate software with CVE references
- Risk classification (Low / Medium / High / Critical)
- Centralized vulnerability dashboard

### 📊 Security Dashboard
- Global risk score
- Number of outdated technologies
- Critical vulnerabilities overview
- Per-machine security view

### 🕒 Audit History
- Historical tracking of version changes
- Change timeline
- Security evolution monitoring

---

## 🗄 Database Model (Simplified)

### machines
- id
- hostname
- ip_address
- environment
- last_audit

### installed_software
- id
- machine_id
- name
- version
- support_end_date
- status

### vulnerabilities
- id
- software_id
- cve_id
- severity
- description

### audit_history
- id
- machine_id
- action
- timestamp

---

## 🔍 Technology Obsolescence Detection

TechAudit integrates external lifecycle references such as:

- Public End-of-Life databases
- CVE databases (e.g. NVD)
- Vendor release notes

The platform calculates:

- Security risk score
- Upgrade priority
- Compliance status

---

## 🚀 Getting Started

### Requirements

- Docker
- Docker Compose
- Java 21 (for development)
- Node 20+ (for development)

---

### Run with Docker

```bash
docker compose up -d --build
```

### Services :

* Frontend → http://localhost:3000
* API → http://localhost:8080
* Keycloak → http://localhost:8081

## 🔐 Security Model

Authentication is handled by Keycloak using OpenID Connect.

The backend validates JWT tokens as a resource server.

Authorization is role-based and enforced at:

* API level (Spring Security)
* UI level (Next.js)