# Anypoint Exchange Publication Guide

## Prerequisites for Publishing

To publish the Energy Asset 360 Experience API to Anypoint Exchange, you need:

1. **Organization ID**: A valid UUID format organization ID from your Anypoint Platform account
2. **Authentication**: Valid credentials for Anypoint Platform
3. **Exchange Access**: Permissions to publish assets to your organization's Exchange

## Manual Publication Steps

### Option 1: Using Anypoint Platform UI
1. Login to [Anypoint Platform](https://anypoint.mulesoft.com)
2. Navigate to **Exchange** in the left navigation
3. Click **Publish new asset**
4. Select **API Specification** as asset type
5. Fill in the details:
   - **Name**: Energy Asset 360 Experience API
   - **Asset ID**: asset-360-experience-api
   - **Version**: 1.1.0
   - **API Version**: v1.1
   - **Group ID**: Use your organization's group ID
   - **Description**: Experience API for Houston Oil & Gas meetup. Orchestrates discovery and health details for high-value field assets.
6. Upload the `openapi.yaml` file
7. Add tags: `oil-gas`, `energy`, `assets`, `houston-meetup`, `experience-api`
8. Click **Publish**

### Option 2: Using MuleSoft CLI
Once you have your organization ID, use this command:

```bash
anypoint-cli-v4 exchange asset upload \
  --organizationId YOUR_ORG_ID_HERE \
  --groupId com.energy.experience \
  --assetId asset-360-experience-api \
  --version 1.1.0 \
  --name "Energy Asset 360 Experience API" \
  --classifier oas \
  --apiVersion v1.1 \
  --main openapi.yaml \
  --files openapi.yaml
```

## Getting Your Organization ID

1. Login to Anypoint Platform
2. Navigate to **Access Management** > **Organization**
3. Your Organization ID will be displayed (UUID format: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx)

## Asset Details for Publication

- **Asset Name**: Energy Asset 360 Experience API
- **Asset ID**: asset-360-experience-api
- **Version**: 1.1.0
- **Group ID**: com.energy.experience (or your organization's group)
- **Classifier**: oas (OpenAPI Specification)
- **API Version**: v1.1
- **Main File**: openapi.yaml

## Keywords & Tags
- oil-gas
- energy
- assets
- scada
- maximo
- salesforce
- field-service
- houston-meetup
- experience-api
- mulesoft
- production-ready
- cloudhub
- industrial-iot
- anomaly-detection

## Publication Benefits

Once published to Exchange, your API will be:
- **Discoverable** by other developers in your organization
- **Reusable** across multiple projects
- **Governable** with proper versioning and lifecycle management
- **Mockable** with automatic mock service generation
- **Documentable** with interactive API console

## Next Steps After Publication

1. **Share the Exchange URL** with your Houston Oil & Gas meetup audience
2. **Generate mock services** for demonstration purposes
3. **Create implementation templates** using the specification
4. **Set up API governance policies** for production deployment
