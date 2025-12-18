# Energy Asset 360 Experience API

**Version:** v1.1  
**Industry:** Oil & Gas (Upstream/Midstream Operations)  
**Target Platform:** MuleSoft Anypoint Platform (CloudHub 2.0)  
**Primary Consumer:** Salesforce Field Service Lightning Web Components

---

## Overview

The Energy Asset 360 Experience API delivers a unified, real-time view of critical energy infrastructure assets directly within Salesforce Field Service Mobile. Designed specifically for the Houston Oil & Gas meetup, this API orchestrates data from multiple backend systems including SAP/Maximo (ERP) and SCADA/IoT platforms, eliminating data silos and enabling proactive maintenance strategies.

### Business Impact
- **🛠️ Predictive Maintenance:** Real-time anomaly detection prevents catastrophic equipment failures
- **📊 Operational Efficiency:** Consolidated 360° asset view eliminates manual data gathering
- **⚖️ Regulatory Compliance:** Centralized monitoring supports EPA and safety reporting
- **💰 Cost Optimization:** Reduces emergency repair costs through predictive insights

---

## API Endpoints

### 🔍 GET /assets
**Discover Available Assets**

Browse and search available energy infrastructure assets. Perfect for field technician workflows with Salesforce-style discovery interface.

**Response:**
```json
[
  {
    "assetId": "02i8W00000GvXYZ",
    "name": "Wellhead Pump Alpha-7",
    "serialNumber": "SN-PMP-9901",
    "status": "Installed",
    "currentStatus": "Warning",
    "operationalRegion": "Permian Basin"
  },
  {
    "assetId": "02i8W00000GvABC",
    "name": "Turbine Gamma-2", 
    "serialNumber": "SN-TRB-4412",
    "status": "Registered",
    "currentStatus": "Online",
    "operationalRegion": "Eagle Ford"
  }
]
```

**Use Cases:**
- Field technician asset discovery
- Mobile dashboard asset lists
- Search and filter operations
- Regional asset browsing

---

### 📊 GET /assets/{assetId}/detail
**Get Comprehensive 360-Degree Asset Status**

Retrieve detailed asset information with real-time sensor telemetry, maintenance history, and anomaly detection.

**Parameters:**
- `assetId` (path, required): Salesforce Asset Record ID (e.g., `02i8W00000GvXYZ`)

**Response:**
```json
{
  "assetSummary": {
    "assetId": "02i8W00000GvXYZ",
    "name": "Wellhead Pump Alpha-7",
    "serialNumber": "SN-PMP-9901",
    "status": "Installed",
    "currentStatus": "Warning",
    "lastRunHours": 168.5,
    "currentPressurePsi": 852.4,
    "operationalRegion": "Permian Basin",
    "flaggedAlerts": 2,
    "location": {
      "latitude": 31.8457,
      "longitude": -102.3676,
      "wellSite": "Site-Alpha-7"
    },
    "lastMaintenance": "2025-11-15T10:30:00Z",
    "nextScheduledMaintenance": "2025-12-20T08:00:00Z"
  },
  "sensorReadings": [
    {
      "readingId": "SR-5521",
      "timestamp": "2025-12-18T08:00:00Z",
      "pressurePsi": 852.4,
      "temperatureC": 110.5,
      "vibrationRMS": 2.1,
      "flowRateGPM": 125.8,
      "powerConsumptionKW": 45.2,
      "isAnomaly": true
    }
  ],
  "metadata": {
    "responseTime": "2025-12-18T08:00:25.123Z",
    "dataSourcesQueried": ["Maximo", "SCADA", "SAP"],
    "cacheStatus": "FRESH"
  }
}
```

**Use Cases:**
- Field service mobile dashboards
- Predictive maintenance workflows
- Real-time monitoring alerts
- Historical trend analysis

---

## Security

### Authentication
- **Client ID Enforcement:** API Key-based authentication
- **Header Required:** `client_id` with valid Exchange client credentials
- **Salesforce Integration:** Seamless via Named Credentials

### Rate Limiting
- **Limit:** 100 requests per minute per client
- **Protection:** Safeguards legacy SCADA system performance
- **Throttling:** Spike control for high-volume scenarios

---

## Data Models

### AssetSummary
Core asset information optimized for Oil & Gas operations.

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `assetId` | String | Salesforce Asset Record ID | `"02i8W00000GvXYZ"` |
| `name` | String | Asset display name | `"Wellhead Pump Alpha-7"` |
| `serialNumber` | String | Equipment serial number | `"SN-PMP-9901"` |
| `status` | Enum | Lifecycle status | `"Installed"` |
| `currentStatus` | Enum | Real-time operational status | `"Warning"` |
| `lastRunHours` | Number | Cumulative runtime hours | `168.5` |
| `currentPressurePsi` | Number | Current pressure reading | `852.4` |
| `operationalRegion` | String | Geographic region | `"Permian Basin"` |
| `flaggedAlerts` | Integer | Active alert count | `2` |
| `location` | Object | GPS coordinates + well site | See Location schema |

### Location
Geographic and site information for field operations.

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `latitude` | Number | GPS latitude | `31.8457` |
| `longitude` | Number | GPS longitude | `-102.3676` |
| `wellSite` | String | Well site identifier | `"Site-Alpha-7"` |

### SensorReading
Industrial IoT sensor data with anomaly detection.

| Field | Type | Description | Example |
|-------|------|-------------|---------|
| `readingId` | String | Unique reading identifier | `"SR-5521"` |
| `timestamp` | DateTime | ISO 8601 timestamp | `"2025-12-18T08:00:00Z"` |
| `pressurePsi` | Number | Pressure in PSI | `852.4` |
| `temperatureC` | Number | Temperature in Celsius | `110.5` |
| `vibrationRMS` | Number | Vibration RMS value | `2.1` |
| `flowRateGPM` | Number | Flow rate (gallons/min) | `125.8` |
| `powerConsumptionKW` | Number | Power consumption | `45.2` |
| `isAnomaly` | Boolean | AI anomaly detection flag | `true` |

---

## Error Handling

### HTTP Status Codes

| Code | Description | Response |
|------|-------------|----------|
| `200` | Success | Asset data returned |
| `401` | Unauthorized | Invalid client credentials |
| `404` | Not Found | Asset does not exist |
| `500` | Server Error | Internal system failure |

### Error Response Format
```json
{
  "error": "Asset not found",
  "code": "ASSET_NOT_FOUND", 
  "timestamp": "2025-12-18T08:00:00Z",
  "details": "Asset ID 02i8W00000GvXYZ does not exist in Maximo system"
}
```

---

## Architecture & Integration

### API-Led Connectivity
Follows MuleSoft's three-layer architecture:

```
Experience Layer (This API) → Process Layer → System Layer
     ↓                           ↓              ↓
Salesforce LWC            Orchestration    SAP/Maximo/SCADA
```

### Data Orchestration
1. **Scatter-Gather Pattern:** Parallel queries to multiple backend systems
2. **DataWeave Transformation:** Real-time data mapping with anomaly detection
3. **Caching Strategy:** 5-min telemetry TTL, 30-min metadata TTL
4. **Mobile Optimization:** Compressed JSON for field service apps

### Backend Systems
- **SAP/ERP:** Master data and asset hierarchies
- **Maximo:** Work orders, maintenance schedules, asset lifecycle
- **SCADA/IoT:** Real-time telemetry (OSI PI, Wonderware)
- **Salesforce:** Field Service Lightning integration

---

## Performance & Scalability

### Response Times
- **Target:** < 500ms (95th percentile)
- **Throughput:** 1000+ concurrent field technicians
- **Availability:** 99.9% uptime SLA

### CloudHub 2.0 Deployment
- **Runtime:** Mule 4.10 with performance optimizations
- **Scaling:** Auto-scaling (1+ vCores, 2+ replicas for HA)
- **Monitoring:** Custom Energy sector dashboards

---

## Getting Started

### 1. Obtain API Access
- Request client credentials from Exchange
- Configure Salesforce Named Credentials
- Set up proper security policies

### 2. Test Endpoints
```bash
# List assets
curl -X GET "https://energy-asset-360-exp.us-e2.cloudhub.io/api/v1/assets" \
  -H "client_id: YOUR_CLIENT_ID"

# Get asset details  
curl -X GET "https://energy-asset-360-exp.us-e2.cloudhub.io/api/v1/assets/02i8W00000GvXYZ/detail" \
  -H "client_id: YOUR_CLIENT_ID"
```

### 3. Integration Patterns
```javascript
// Salesforce Lightning Web Component
import { LightningElement, api, track } from 'lwc/core';
import getAssetDetail from '@salesforce/apex/AssetController.getAssetDetail';

export default class Asset360Dashboard extends LightningElement {
    @api recordId;
    @track assetData;
    @track loading = true;

    async connectedCallback() {
        try {
            this.assetData = await getAssetDetail({ assetId: this.recordId });
            this.loading = false;
        } catch (error) {
            console.error('Error loading asset data:', error);
        }
    }
}
```

---

## Use Cases

### Field Service Technicians
- **Mobile Asset Discovery:** Browse available equipment by region
- **Predictive Maintenance:** Receive anomaly alerts before failures occur
- **Work Order Context:** Access real-time asset status during service calls
- **GPS Navigation:** Use location data for efficient routing

### Operations Centers
- **Fleet Monitoring:** Track asset performance across multiple sites
- **Compliance Reporting:** Generate EPA and safety reports
- **Resource Planning:** Optimize maintenance schedules based on runtime data
- **Emergency Response:** Rapid identification of critical asset failures

### Management & Analytics
- **KPI Dashboards:** Monitor asset utilization and performance metrics
- **Cost Optimization:** Identify opportunities for predictive maintenance
- **Regional Analysis:** Compare performance across operational areas
- **Trend Analysis:** Historical data for long-term planning

---

## Houston Oil & Gas Meetup Demo

### Demo Scenarios
1. **Asset Discovery:** Browse wellhead pumps in Permian Basin
2. **Real-time Monitoring:** View live telemetry from SCADA systems
3. **Anomaly Detection:** Demonstrate AI-powered failure prediction
4. **Mobile Integration:** Show Salesforce Field Service mobile UI
5. **Regional Operations:** Compare Eagle Ford vs Permian Basin assets

### Sample Data
- **Wellhead Pump Alpha-7:** High-pressure warning scenario
- **Turbine Gamma-2:** Optimal performance example
- **Pipeline Compressor Delta-5:** Maintenance due scenario

---

## Support & Resources

### Documentation
- **Technical Specs:** Complete OpenAPI 3.0.3 specification
- **Implementation Guide:** Step-by-step integration instructions
- **Best Practices:** Oil & Gas industry optimization tips

### Community
- **Houston MuleSoft Meetup:** Monthly technical discussions
- **Energy Sector APIs:** Industry-specific integration patterns
- **Salesforce Field Service:** Mobile app development resources

### Contact
- **API Support Team:** Technical assistance and troubleshooting
- **Exchange Portal:** Latest versions and documentation updates
- **Community Forum:** Peer-to-peer developer support

---

*Last Updated: December 18, 2025*  
*API Version: v1.1*  
*Documentation Version: 1.0*
