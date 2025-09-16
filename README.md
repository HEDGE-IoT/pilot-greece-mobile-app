# Mobile App for Residential Users

## 1.1 General Information and Purpose
- **Service Name/Title:** Mobile App for Residential Users  
- **Description and purpose:**  
The mobile app enables residential users to actively participate in demand-side flexibility programs. It provides real-time visualizations of household electricity consumption, PV production (if available), and tailored flexibility opportunities. The app empowers users to understand and optimize their energy behaviour while receiving incentives for participating in grid services. It also delivers push notifications about events and offers, enhancing user engagement and system responsiveness.  
- **Owner/Contact Information:** ICCS

---

## 1.2 Functional Requirements
- Show historical consumption data and patterns  
- Display real-time electricity consumption  
- Provide electricity billing breakdown and comparison of alternative offers  
- Notify users about upcoming flexibility events  
- Present incentive offers personalized to the user’s profile  
- Authenticate and authorize users securely via Keycloak  
- Sync user data with the backend optimization and forecasting services  

---

## 1.3 Non-Functional Requirements

### Performance
- App should update energy data within 5 seconds of backend push (for real-time events).  
- Minimal load time (<2s) on modern smartphones.  
- Efficient handling of chart rendering with limited device memory.  

### Reliability and Availability
- 99.5% availability.  
- Automatic re-sync when reconnected.  

### Security
- **Authentication:** Keycloak-based OAuth 2.0 flow.  
- **Authorization:** Role-based access control (residential user).  
- **Data Encryption:** All network communication over HTTPS.  
- **Data Privacy:** User-controlled data sharing, aligned with GDPR principles.  

---

## 1.4 Service Interfaces

### 1.4.1 API Endpoints
- The app consumes backend APIs, with data primarily fed from **SUC-04 Data Capture** service.  
- Request/response schemas and error handling follow backend service definitions.  

### 1.4.2 UI Mockups
- Dashboard mockups are included in **Section 1.8**.  

---

## 1.5 Data Model

### Entities and Relationships
- **Users ↔ Houses:** Many-to-many. Users may access multiple houses; houses may have multiple users.  
- **Users ↔ Energy Communities:** Many-to-many. Supports shared energy programs.  
- **Houses ↔ Devices:** One-to-many. Houses can host multiple IoT devices.  
- **Devices ↔ Rooms:** Optional one-to-many. Contextualizes devices.  
- **Devices ↔ Device Types / Device Models / Device Use / Brands:** Rich metadata for categorization, expected usage, manufacturer data.  
- **Houses ↔ PVs:** One-to-many. A house may have one or more PV installations.  
- **Houses ↔ Billing Metadata / Billing History:** Stores billing and cost-related records for analysis.  

### Database Schema
- PostgreSQL/TimescaleDB backend ensures efficient time-series data management.  

---

## 1.6 Integration and Dependencies

### External Dependencies
- **Flexibility Optimization Service:** For incentive/event logic.  
- **Forecasting Modules:** For demand/production predictions.  

### System Dependencies
- **MQTT/Kafka:** For live data streams.  
- **PostgreSQL/TimescaleDB:** Backend data storage.  

### Third-Party Integrations
- **Keycloak:** Authentication and RBAC.  
- **Firebase/Apple Push Notification Services:** Real-time event/incentive notifications.  

### HEDGE-IoT Integration
- Receives IoT readings from edge devices via backend services.  

### App Store Integration
- Compliant with **Google Play Store** and **Apple App Store** policies.  

### Data Space Integration
- Not implemented at this stage.  

---

## 1.7 Security and Privacy

### Data Sensitivity
- Consumption, production, and incentive data is privacy-sensitive.  
- Data pseudonymized for analytics and compliance.  

### Access Control
- Enforced via Keycloak tokens.  
- Users can only access their own data.  

### Audit Logs
- Login/logout events.  
- Data access and action logs.  

---

## 1.8 Pre-Demo Phase (WP5 Related)

### Overview – Features
The mobile app provides a comprehensive overview of household electricity consumption across multiple screens:  

- **Dashboard:**  
  Displays real-time and cumulative energy usage (today, week, month), averages, line chart (last hour), bar charts (daily/weekly), billing details (total/average cost).  

- **Devices Screen:**  
  Monitors consumption per device (meters, boilers, heat pumps). Each device shows 24-hour trends and operational status (ON/OFF, temperature settings).  

- **Billing Section:**  
  Summarizes costs, usage trends, and cost history. Includes plan comparison and suggests cheaper providers based on consumption patterns.  

### Outcome
Combines real-time tracking, historical analytics, and cost-saving tools. Enables users to stay informed and make better energy decisions while actively participating in flexibility services.  

---
