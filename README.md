# Asset 360 Experience API

**Industry Focus:** Energy / Oil & Gas (Upstream/Midstream Operations)  
**Target Platform:** MuleSoft Anypoint Platform (CloudHub 2.0) - Mule 4.10 Runtime  
**Primary Consumer:** Salesforce Field Service Lightning Web Components  

## Executive Overview

The Asset 360 Experience API delivers a unified, real-time view of critical energy infrastructure assets (wellhead pumps, pipeline compressors, drilling equipment) directly within Salesforce Field Service Mobile. By orchestrating data from SAP/Maximo (ERP), SCADA/IoT platforms, and operational systems, this API eliminates data silos and enables proactive maintenance strategies that reduce downtime by up to 40%.

### Business Impact
- **🛠️ Predictive Maintenance:** Real-time anomaly detection prevents catastrophic equipment failures
- **📊 Operational Efficiency:** Consolidated 360° asset view eliminates manual data gathering across systems
- **⚖️ Regulatory Compliance:** Centralized monitoring supports EPA and safety reporting requirements
- **💰 Cost Optimization:** Reduces emergency repair costs through predictive insights

## API Specification
- **Version**: v1 (1.0.0)
- **Format**: OpenAPI 3.0.3
- **Base URL**: `https://asset-360-exp-api.us-e2.cloudhub.io/api/v1`
- **Runtime**: Mule 4.10 on CloudHub 2.0
- **Authentication**: Client ID Enforcement + Salesforce Named Credentials

## Key Features
- **🏭 Industrial Asset Intelligence**: Deep integration with Maximo, SAP, and SCADA systems
- **📡 Real-time Telemetry**: Live sensor data with configurable anomaly thresholds
- **🎯 Field Service Optimized**: Purpose-built for mobile field technician workflows
- **🔒 Enterprise Security**: Client ID enforcement, OAuth 2.0, and audit-compliant logging
- **📈 Performance Engineered**: Sub-500ms response times with auto-scaling architecture

## Endpoints

### GET /assets/{assetId}/detail
Retrieves comprehensive asset details with real-time sensor telemetry, optimized for field technician dashboards.

**Parameters:**
- `assetId` (path, required): Salesforce Asset Record ID (e.g., `02i8W000000xxxxx`)

**Response Schema:**
Returns a structured JSON object containing:
- **Asset Summary**: Operational status, runtime metrics, location data, maintenance schedules
- **Real-time Telemetry**: Pressure, temperature, vibration, flow rate, power consumption
- **Anomaly Detection**: AI-powered threshold monitoring with configurable alerts
- **Metadata**: Response timing, data source lineage, cache status

**Example Response:**
```json
{
  "assetSummary": {
    "assetId": "02i8W000000xxxxx",
    "name": "ESP-Pump-01",
    "currentStatus": "Optimal",
    "lastRunHours": 1450.5,
    "currentPressurePsi": 850.2,
    "operationalRegion": "Permian Basin",
    "flaggedAlerts": 0,
    "location": {
      "latitude": 31.8457,
      "longitude": -102.3676,
      "wellSite": "Site-Alpha-7"
    }
  },
  "sensorReadings": [
    {
      "timestamp": "2025-12-17T14:30:22.000Z",
      "pressurePsi": 850.2,
      "temperatureC": 110.5,
      "vibrationRMS": 0.45,
      "flowRateGPM": 125.8,
      "isAnomaly": false
    }
  ]
}
```

## Architecture & Integration

### API-Led Connectivity Model
This API follows MuleSoft's three-layer architecture pattern:

```
Experience Layer (This API) → Process Layer → System Layer
     ↓                           ↓              ↓
Salesforce LWC            Orchestration    SAP/Maximo/SCADA
```

### Data Orchestration Flow
1. **Parallel Data Retrieval**: Scatter-Gather pattern queries multiple backend systems simultaneously
2. **DataWeave Transformation**: Real-time data mapping with anomaly detection logic
3. **Caching Strategy**: Optimized TTL policies (5min telemetry, 30min metadata)
4. **Response Optimization**: Compressed JSON tailored for mobile consumption

## Industry-Specific Data Models

### AssetSummary (Energy/O&G Enhanced)
```json
{
  "assetId": "Salesforce Record ID",
  "name": "Asset identifier (e.g., ESP-Pump-01)",
  "currentStatus": "Optimal|Warning|Critical",
  "lastRunHours": "Cumulative runtime hours",
  "currentPressurePsi": "Real-time pressure reading",
  "operationalRegion": "Geographic region (e.g., Permian Basin)",
  "flaggedAlerts": "Count of active alerts",
  "location": "GPS coordinates + well site identifier",
  "lastMaintenance": "ISO 8601 timestamp",
  "nextScheduledMaintenance": "ISO 8601 timestamp"
}
```

### SensorReading (Industrial IoT Enhanced)
```json
{
  "readingId": "Unique sensor reading identifier",
  "timestamp": "ISO 8601 timestamp",
  "pressurePsi": "Pressure (PSI)",
  "temperatureC": "Temperature (Celsius)",
  "vibrationRMS": "Vibration RMS value",
  "flowRateGPM": "Flow rate (Gallons per minute)",
  "powerConsumptionKW": "Power consumption (Kilowatts)",
  "isAnomaly": "AI-detected anomaly flag",
  "alertThreshold": "Configurable threshold values"
}
```

## Enterprise Architecture Integration

### MuleSoft Anypoint Platform Stack
- **Runtime**: Mule 4.10 with enhanced performance optimizations
- **Deployment**: CloudHub 2.0 with auto-scaling (1+ vCores, 2+ replicas for HA)
- **Security**: Client ID Enforcement, OAuth 2.0, TLS 1.2+
- **Monitoring**: Anypoint Monitoring with custom Energy sector dashboards
- **Governance**: API governance policies with 100 req/min rate limiting

### Backend System Integration
- **SAP/ERP Integration**: Master data management and asset hierarchies
- **Maximo Integration**: Work order history, maintenance schedules, asset lifecycle
- **SCADA/IoT Integration**: Real-time telemetry from field devices (OSI PI, Wonderware)
- **Salesforce Integration**: Seamless consumption via Named Credentials and Lightning Web Components

### Performance & Scalability
- **Response Time**: < 500ms (95th percentile)
- **Throughput**: 1000+ concurrent field technicians
- **Availability**: 99.9% uptime SLA
- **Scalability**: Auto-scaling based on demand patterns

## Quick Start Deployment

### 🚀 Deploy to Anypoint Exchange (Recommended)
```bash
# Using MuleSoft CLI (requires authentication)
anypoint-cli-v4 exchange asset upload \
  --organizationId YOUR_ORG_ID \
  --groupId com.energy.experience \
  --assetId asset-360-experience-api \
  --version 1.0.0 \
  --name "Asset 360 Experience API" \
  --classifier oas \
  --apiVersion v1 \
  --main openapi.yaml
```

### 🔧 Implementation Checklist
- [ ] **Backend APIs Ready**: Ensure Maximo, SAP, and SCADA System APIs are accessible
- [ ] **Security Configuration**: Set up Client ID Enforcement and Named Credentials
- [ ] **Performance Tuning**: Configure caching policies and connection pools
- [ ] **Monitoring Setup**: Deploy custom dashboards for Energy sector KPIs
- [ ] **Testing**: Validate with realistic field technician usage patterns

### 📋 Production Deployment Requirements
- **CloudHub 2.0**: Minimum 1 vCore, 2 replicas for high availability
- **Private Space**: Enhanced security for sensitive operational data
- **Rate Limiting**: 100 req/min to protect legacy SCADA systems
- **Audit Logging**: Comprehensive logging for regulatory compliance
- **Circuit Breakers**: Fault tolerance for downstream system failures

## Documentation & Resources

### 📖 Available Documentation
- **[Design Specification](DESIGN_SPECIFICATION.md)**: Comprehensive technical architecture and implementation guide
- **[Deployment Guide](deployment-guide.md)**: Step-by-step deployment instructions for multiple environments  
- **[Contributing Guidelines](CONTRIBUTING.md)**: How to contribute to this open-source API specification
- **[Changelog](CHANGELOG.md)**: Version history and release notes

### 🔗 External Resources
- [MuleSoft Anypoint Platform](https://www.mulesoft.com/platform/enterprise-integration)
- [Salesforce Field Service Documentation](https://developer.salesforce.com/docs/atlas.en-us.field_service_dev.meta/field_service_dev/)
- [OpenAPI 3.0 Specification](https://swagger.io/specification/)
- [Energy Sector API Best Practices](https://docs.mulesoft.com/general/api-led-overview)

## Support
Contact: API Support Team (api-support@company.com)
License: MIT
