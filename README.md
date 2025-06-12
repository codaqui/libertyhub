# 🚀 LibertyHub

[![Image Request](assets/image.png)](https://github.com/codaqui/libertyhub/issues/new/choose)

Repository to release images from Docker Hub and securely republish them within GitHub Packages in an auditable and reliable manner.

## 🎯 Purpose

LibertyHub is designed to provide a transparent and secure way to import container images from external sources (initially Docker Hub) into GitHub Packages. This enhances security, provides audit trails, and reduces dependency on external registries.

## 🔄 How It Works

1. **📋 Issue-Based Workflow**: Users create an issue using a standardized template
2. **🤖 Automated Processing**: GitHub Workflows process the request with intelligent naming
3. **✅ Verification & Publishing**: The system checks, imports and publishes with proper mapping
4. **📊 Audit Trail**: All actions are logged for complete transparency

## ✨ Features

- **🎛️ Source Selection**: Choose the image source (initially Docker Hub, with plans to expand)
- **📦 Support for Official Images**: Option to mark an image as an official Docker Hub image
- **📝 Simple Request Process**: Easy-to-use issue template with dropdown options
- **🔄 Latest Version Support**: Option to select the latest version of an image
- **🔄 Automatic Updates**: For images marked as "latest", duplicate requests will trigger an update
- **🏷️ Intelligent Naming**: Smart naming convention with conflict resolution
- **📋 Complete Audit Trail**: All actions are logged, including image hashes, versions, and workflow details
- **🚫 Duplicate Prevention**: System verifies if the requested image already exists before processing
- **� Execution Control**: Prevents duplicate workflow runs with smart event handling and state tracking
- **�🗂️ Image Mapping**: Advanced naming system to handle complex Docker Hub structures

## 🏷️ Naming Convention & Image Mapping

### Standard Naming Pattern
Images are republished following the pattern: 
- **Official images**: `ghcr.io/codaqui/dockerhub-<image>:<version>`
- **Organization images**: `ghcr.io/codaqui/dockerhub-<org>-<image>:<version>`

### Intelligent Image Name Extraction

The system uses intelligent extraction to handle various Docker Hub naming patterns:

#### 📦 Official Images
```
Docker Hub: nginx:latest
GHCR: ghcr.io/codaqui/dockerhub-nginx:latest
```

#### 🏢 Organization/Repository Images
```
Docker Hub: bitnami/nginx:latest
GHCR: ghcr.io/codaqui/dockerhub-bitnami-nginx:latest

Docker Hub: homeassistant/core:latest  
GHCR: ghcr.io/codaqui/dockerhub-homeassistant-core:latest

Docker Hub: confluentinc/cp-kafka:latest
GHCR: ghcr.io/codaqui/dockerhub-confluentinc-cp-kafka:latest
```

#### 🔧 Complex Naming Examples
```
Docker Hub: homeassistant/aarch64-homeassistant:latest
GHCR: ghcr.io/codaqui/dockerhub-homeassistant-aarch64-homeassistant:latest

Docker Hub: microsoft/mssql-server-linux:latest
GHCR: ghcr.io/codaqui/dockerhub-microsoft-mssql-server-linux:latest

Docker Hub: prom/prometheus:latest
GHCR: ghcr.io/codaqui/dockerhub-prom-prometheus:latest
```

### 🚨 Naming Conflict Resolution & Limitations

**Organization Names with Hyphens**: ❌ **Not Supported**

The system **rejects** organization names containing hyphens to avoid conflicts:

```
❌ REJECTED: docker-compose/nginx → Would create: dockerhub-docker-compose-nginx
❌ REJECTED: my-org/postgres → Would create: dockerhub-my-org-postgres
```

**Why?**: These create ambiguity in reverse mapping for automatic updates:
- `dockerhub-my-org-postgres` could be interpreted as:
  - `my-org/postgres` ✅ (intended)  
  - `my/org-postgres` ❌ (wrong interpretation)

**Workarounds**:
1. Use organizations without hyphens when possible
2. Request official image status from Docker Hub
3. Use alternative image sources (official variants)

### 📊 Mapping Information

Each import creates a mapping record:
```json
{
  "source_pattern": "homeassistant/core:latest",
  "target_pattern": "dockerhub-homeassistant-core", 
  "mapping_type": "org_image_combination",
  "original_repo": "homeassistant",
  "original_image": "core",
  "org_name": "homeassistant", 
  "image_name": "core",
  "created": "2025-06-11T20:30:45Z"
}
```

**Mapping Types:**
- `standard`: Direct mapping (official images)
- `org_image_combination`: Organization + image name combination 
- `sanitized_fallback`: Fallback for complex structures

## 🚀 Usage

### 📝 Creating an Import Request

1. **Create Issue**: Use the "Image Import Request" template
2. **Fill Information**:
   - **Image source**: Select "Docker Hub" from dropdown
   - **Official image**: Check if it's an official Docker Hub image
   - **Repository name**: 
     - ✅ Leave empty for official images (nginx, ubuntu, postgres)
     - ✅ Required for organization images (bitnami, homeassistant, microsoft)
   - **Image name**: The actual image name
   - **Version**: Specific version or check "Use latest"
3. **Submit**: The workflow processes automatically
4. **Track Progress**: Updates provided in issue comments
5. **Use Image**: Available in GitHub Packages with smart naming

### 📋 Request Examples

#### Official Image
```
✅ Source: Docker Hub
✅ Official: [x] This is an official Docker Hub image  
✅ Repository: [leave empty]
✅ Image: nginx
✅ Version: latest
Result: ghcr.io/codaqui/dockerhub-nginx:latest
```

#### Organization Image  
```
✅ Source: Docker Hub
❌ Official: [ ] This is an official Docker Hub image
✅ Repository: homeassistant
✅ Image: core 
✅ Version: latest
Result: ghcr.io/codaqui/dockerhub-homeassistant-core:latest
```

#### Complex Organization Image
```
✅ Source: Docker Hub
❌ Official: [ ] This is an official Docker Hub image
✅ Repository: homeassistant
✅ Image: aarch64-homeassistant  
✅ Version: latest
Result: ghcr.io/codaqui/dockerhub-homeassistant-aarch64-homeassistant:latest
```

#### Complex Organization
```
✅ Source: Docker Hub
❌ Official: [ ] This is an official Docker Hub image
✅ Repository: microsoft
✅ Image: mssql-server-linux
✅ Version: 2019-latest
Result: ghcr.io/codaqui/dockerhub-microsoft-mssql-server-linux:2019-latest
```

### 🔄 Updating Latest Images

To update an image tagged as "latest":
1. Create a new import request with same details
2. Check "Use latest" option  
3. System detects duplicate and updates automatically
4. Audit trail shows before/after hashes

### ⏰ Scheduled Updates

A scheduled workflow automatically updates all `latest` images daily:
- 🕛 **Runs**: Daily at midnight UTC
- 🚀 **Manual trigger**: Available via `workflow_dispatch`
- 📊 **Smart updates**: Only updates when source image changed
- 📋 **Full audit**: Complete logging and hash verification

## 📊 Audit & Transparency

### 📋 Import Audit Information
Each import includes:
- 🔍 **Source verification**: Original Docker Hub image details
- 🔐 **Hash tracking**: SHA256 hashes before/after import  
- 🕐 **Timestamps**: Complete temporal tracking
- 👤 **Attribution**: User who requested import
- 🔗 **Workflow logs**: Full GitHub Actions execution logs
- 🗂️ **Mapping details**: How naming was resolved

### 📈 Update Audit Information  
For updated images:
- 🔄 **Previous state**: Hash of existing image
- 🆕 **New state**: Hash of updated image
- 📊 **Comparison**: What changed between versions
- ⚡ **Update trigger**: Manual vs scheduled
- 🔍 **Pull method**: How the source was obtained

### 🗃️ Audit File Format
```json
{
  "timestamp": "2025-06-11T20:30:45Z",
  "workflow_run": "15594728920", 
  "request": {
    "source": "homeassistant/core:latest",
    "target": "ghcr.io/codaqui/dockerhub-homeassistant-core:latest",
    "status": "success",
    "source_hash": "sha256:abc123...",
    "target_hash": "sha256:abc123...",
    "pull_method": "direct",
    "image_exists": false,
    "update_needed": true,
    "mapping": {
      "source_pattern": "homeassistant/core:latest",
      "target_pattern": "dockerhub-homeassistant-core",
      "mapping_type": "org_image_combination",
      "original_repo": "homeassistant",
      "original_image": "core",
      "org_name": "homeassistant",
      "image_name": "core"
    }
  }
}
```

## 🛡️ Security & Best Practices

### 🔐 Security Features
- ✅ **Hash verification**: Every image verified with SHA256
- ✅ **Audit trails**: Complete transparency in all operations  
- ✅ **Access control**: GitHub permissions and authentication
- ✅ **Isolated builds**: Each import in isolated environment

### 📋 Best Practices
- 🎯 **Specific versions**: Use specific tags when possible vs `latest`
- 🔄 **Regular updates**: Keep `latest` images updated via scheduled workflow
- 📊 **Monitor logs**: Review audit information for any anomalies
- 🏷️ **Consistent naming**: Follow the established naming conventions

## 🤝 Contributing

Contributions to improve LibertyHub are welcome:

1. 🐛 **Bug reports**: Use GitHub issues
2. 💡 **Feature requests**: Use GitHub discussions  
3. 🔧 **Code contributions**: Follow our PR guidelines
4. 📚 **Documentation**: Help improve this README

## 🚀 Development & Credits

**Version 2.0.0** - Enhanced automation and improved user experience

This major version was developed with the assistance of **Claude Sonnet 4**, which significantly contributed to:
- 🔧 **Workflow Optimization**: Enhanced GitHub Actions workflows with better error handling
- 📝 **Documentation Improvements**: Comprehensive README updates and clearer user guidance  
- 🎨 **Issue Template Enhancement**: More intuitive and informative request templates
- 🐛 **Bug Fixes**: Resolution of Docker template parsing errors and naming conflicts
- ✨ **Feature Enhancements**: Improved audit trails and automatic update mechanisms

*Special thanks to Claude Sonnet 4 for the exceptional assistance in making LibertyHub more robust and user-friendly.*

## 📄 License

LibertyHub is licensed under the MIT License. Version 2.0.0 was developed with significant assistance from Claude Sonnet 4, demonstrating the power of AI-assisted development in creating robust automation solutions.
