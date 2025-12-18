# Asset 360 Experience API - Deployment Guide

## Quick Deployment Checklist

### ✅ Pre-Deployment Verification
- [x] OpenAPI 3.0 specification validated
- [x] All required schemas defined
- [x] Response examples included
- [x] Contact and license information added
- [x] Documentation complete

### 🚀 Deployment Steps

#### Step 1: Authenticate with Anypoint Platform
You'll need valid credentials for your organization's Anypoint Platform instance.

#### Step 2: Choose Deployment Method

**Recommended: Anypoint CLI (Command Line)**
```bash
# 1. Install Anypoint CLI
npm install -g anypoint-cli

# 2. Configure authentication
anypoint-cli-v4 conf
# Follow prompts to enter your credentials

# 3. Deploy to Exchange
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

**Alternative: Exchange Web UI**
1. Navigate to Anypoint Platform → Exchange
2. Click "Publish new asset"
3. Select "REST API - OAS" 
4. Upload `openapi.yaml`
5. Complete the metadata form
6. Click "Publish"

### 📋 Deployment Configuration

| Parameter | Value |
|-----------|-------|
| Asset ID | `asset-360-experience-api` |
| Group ID | `com.company.experience` |
| Version | `1.0.0` |
| Classifier | `oas` |
| API Version | `v1` |
| Main File | `openapi.yaml` |

### 🔍 Post-Deployment Validation

1. **Verify in Exchange**: Check that the asset appears in your organization's Exchange
2. **Test Documentation**: Ensure the API documentation renders correctly
3. **Validate Examples**: Confirm response examples display properly
4. **Check Discoverability**: Verify the API can be found via search

### 🔧 Next Steps After Deployment

#### Create API Instance (Optional)
If you plan to implement this API:
```bash
# Create API instance in API Manager
anypoint-cli-v4 api-mgr api create \
  --name "Asset 360 Experience API Instance" \
  --assetId asset-360-experience-api \
  --assetVersion 1.0.0 \
  --environmentId YOUR_ENV_ID
```

#### Implementation Considerations
- **Backend Dependencies**: Ensure Maximo and SCADA System APIs are available
- **Security**: Apply appropriate security policies (OAuth, Basic Auth, etc.)
- **Rate Limiting**: Configure appropriate throttling policies
- **Monitoring**: Set up API analytics and alerting

### 🆘 Troubleshooting

**Common Issues:**
- **403 Forbidden**: Check organization permissions and credentials
- **400 Bad Request**: Verify all required parameters and UUID formats
- **File Upload Issues**: Ensure `openapi.yaml` is valid OpenAPI 3.0

**Need Help?**
Contact: API Support Team (api-support@company.com)

---

## Files Ready for Deployment
- ✅ `openapi.yaml` - Complete API specification
- ✅ `README.md` - Comprehensive documentation  
- ✅ `deployment-guide.md` - This deployment guide

The API specification is production-ready and can be deployed to Anypoint Exchange immediately once you have the proper authentication credentials and organization access.
