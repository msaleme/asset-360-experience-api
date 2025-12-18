# Asset 360 Experience API

## Overview
The Asset 360 Experience API provides a comprehensive, consolidated view of industrial assets by orchestrating data from multiple backend systems including Maximo and SCADA. This Experience API layer is specifically designed to support Salesforce Field Service operations by delivering a unified data model that combines asset summaries, operational status, and real-time sensor readings in a single, streamlined interface.

## API Specification
- **Version**: v1 (1.0.0)
- **Format**: OpenAPI 3.0
- **Base Path**: `/api/v1`

## Features
- **Asset Details**: Comprehensive asset information including operational status and metadata
- **Sensor Data**: Real-time sensor readings with anomaly detection
- **Unified Interface**: Single endpoint for consolidated asset view
- **Salesforce Integration**: Optimized for Field Service Mobile applications

## Endpoints

### GET /assets/{assetId}/detail
Retrieves comprehensive asset details with associated sensor data.

**Parameters:**
- `assetId` (path, required): Unique identifier for the asset

**Response:**
Returns a JSON object containing:
- Asset summary with operational details
- Array of recent sensor readings
- Anomaly flags and alerts

## Data Models

### AssetSummary
Core asset information including:
- Asset identification and naming
- Current operational status
- Runtime metrics (hours, pressure)
- Location and alert information

### SensorReading
Individual sensor data points including:
- Timestamp and reading ID
- Pressure, temperature, and vibration measurements
- Anomaly detection flags

### AssetDetailResponse
Root response object combining asset summary and sensor readings array.

## Architecture
This API serves as an Experience API layer in the three-layer API architecture:
- **Experience Layer**: This API - consumer-focused, business-specific
- **Process Layer**: Orchestration and business logic
- **System Layer**: Backend system integration (Maximo, SCADA)

## Deployment Instructions

### Prerequisites
1. Anypoint Platform account with Exchange access
2. Proper organization permissions
3. Valid authentication credentials

### Deploy to Anypoint Exchange

#### Option 1: Using Anypoint CLI
```bash
# Install Anypoint CLI
npm install -g anypoint-cli

# Login to Anypoint Platform
anypoint-cli-v4 conf

# Deploy to Exchange
anypoint-cli-v4 exchange asset upload \
  --organizationId YOUR_ORG_ID \
  --groupId com.company.experience \
  --assetId asset-360-experience-api \
  --version 1.0.0 \
  --name "Asset 360 Experience API" \
  --classifier oas \
  --apiVersion v1 \
  --main openapi.yaml \
  ./openapi.yaml
```

#### Option 2: Using Exchange Web Interface
1. Login to Anypoint Platform
2. Navigate to Exchange
3. Click "Publish new asset"
4. Select "REST API - OAS"
5. Upload the `openapi.yaml` file
6. Fill in metadata:
   - Name: Asset 360 Experience API
   - Asset ID: asset-360-experience-api
   - Version: 1.0.0
   - API Version: v1
7. Publish the asset

#### Option 3: Using Maven (if part of Mule project)
Add to `pom.xml`:
```xml
<plugin>
  <groupId>org.mule.tools.maven</groupId>
  <artifactId>exchange-mule-maven-plugin</artifactId>
  <version>0.0.21</version>
  <executions>
    <execution>
      <id>upload-asset</id>
      <phase>deploy</phase>
      <goals>
        <goal>exchange-deploy</goal>
      </goals>
    </execution>
  </executions>
</plugin>
```

### Post-Deployment
1. Verify the API appears in Exchange
2. Test the API documentation rendering
3. Set up proper access controls
4. Configure API instance in API Manager (if implementing)

## Implementation Notes
- Ensure backend System APIs (Maximo, SCADA) are available
- Configure appropriate error handling and timeout values
- Implement proper logging and monitoring
- Consider rate limiting and security policies

## Support
Contact: API Support Team (api-support@company.com)
License: MIT
