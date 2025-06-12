# Changelog

All notable changes to LibertyHub will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [2.0.2] - 2025-06-11

### Fixed
- 🔗 Fixed corrupted README header image link that was broken during emoji corrections
- 🎨 Restored proper clickable image button for creating new import requests
- 📝 Cleaned up alt text for header image link

## [2.0.1] - 2025-06-11

### Fixed
- 📝 Removed non-implemented "Retrocompatibility & Update System" section from README
- 📚 Removed references to `docker_hub_mappings.json` file (not implemented)
- 📋 Removed fallback strategies documentation that doesn't match actual implementation
- 🎨 Fixed broken emoji characters in feature list
- 📖 Improved documentation accuracy to match actual functionality

### Removed
- ❌ Misleading documentation about global mapping file system
- ❌ Complex fallback strategies that don't exist in implementation
- ❌ Detailed update-latest process documentation that was incorrect

## [2.0.0] - 2025-06-11

### Added
- 🤖 Enhanced issue template with improved descriptions and validation warnings
- 📝 Comprehensive README documentation with naming conventions and examples
- 🔍 Advanced organization name validation with hyphen conflict detection
- 📊 Detailed audit trail generation with comprehensive logging
- 🚫 Smart duplicate prevention system to avoid redundant workflow runs
- 🏷️ Advanced label management system for better state tracking
- 🎨 Visual improvements with emojis and better formatting throughout
- 📋 Detailed error messages with actionable solutions
- 🗂️ Image mapping documentation with complex naming examples
- 🚀 Development credits section recognizing AI-assisted development

### Changed
- 🔧 Complete overhaul of workflow automation with enhanced error handling
- 📝 Issue template field "Repository Name" → "Repository/Organization Name"
- 🎯 Event triggers changed from `[opened, labeled]` to `[opened]` only
- 📊 Enhanced job summaries with improved hash parsing and verification
- 🔄 Improved image update strategy with better conflict resolution
- 📋 Comprehensive documentation restructuring with clear sections

### Fixed
- 🐛 Docker template parsing error: `{{.ImageID}}` → `{{.ID}}`
- 🔧 JavaScript syntax errors in shell script contexts
- 📝 Issue data extraction regex patterns to match updated field names
- 🔄 Duplicate workflow execution prevention
- ⚠️ Organization name validation for hyphen conflicts
- 📊 Audit file creation and verification processes
- 🏷️ Label management and state tracking improvements

### Security
- 🔐 Enhanced validation to prevent naming conflicts and security issues
- 🛡️ Improved error handling to prevent information disclosure
- 🔍 Better input sanitization for organization and image names

## [1.1.1] - 2025-05-22

### Fixed
- 🔧 Ensure correct tagging of images for GitHub Packages by defining image_name_push variable before usage
- 🔄 Correct image push command to include 'dockerhub-' prefix for GitHub Packages

## [1.1.0] - 2025-05-22

### Added
- 📋 Enhanced image listing with detailed package information from GitHub API
- 🔄 Scheduled workflow for automatic updates of latest Docker images
- 📝 Video tutorial documentation for new image import process
- 🎯 Improved image processing with array syntax for better readability

### Changed
- 🔧 Streamlined API communication for listing organization container packages
- 📊 Enhanced image listing output with comprehensive package details
- 🔄 Updated token usage and authentication for GitHub API access

### Fixed
- 🐛 Missing environment variable for GH_TOKEN in image update step
- 🔄 Image listing to capture only relevant container names from API response
- 📋 API request headers and endpoints for listing organization packages
- 🔧 Image processing loop implementation for better reliability

## [1.0.0] - 2025-03-17

### Added
- 🚀 Initial release of LibertyHub container image import system
- 📝 Comprehensive project documentation and README
- 🎯 Issue template for standardized image import requests
- 👥 CODEOWNERS file for repository governance
- 🔄 Scheduled workflow for updating latest Docker images
- 📦 Support for official Docker Hub images with validation
- 🎛️ Enhanced workflow to handle both official and repository images

### Features
- 🐳 Automated Docker Hub to GitHub Packages image import
- 📋 Issue-based workflow for requesting image imports
- 🏷️ Intelligent naming convention with conflict resolution
- ✅ Validation for repository input and image processing
- 🔄 Automatic updates for images marked as "latest"
- 📊 Basic audit trail and logging capabilities

---

**Development Note**: Version 2.0.0 was developed with significant assistance from Claude Sonnet 4, demonstrating the power of AI-assisted development in creating robust automation solutions.

## Version Comparison Links

- [2.0.2...HEAD](https://github.com/codaqui/libertyhub/compare/v2.0.2...HEAD) (Unreleased)
- [2.0.1...2.0.2](https://github.com/codaqui/libertyhub/compare/v2.0.1...v2.0.2) (Header link fix)
- [2.0.0...2.0.1](https://github.com/codaqui/libertyhub/compare/v2.0.0...v2.0.1) (Documentation fixes)
- [1.1.1...2.0.0](https://github.com/codaqui/libertyhub/compare/v1.1.1...v2.0.0) (Major overhaul)
- [1.1.0...1.1.1](https://github.com/codaqui/libertyhub/compare/v1.1.0...v1.1.1) (Bug fixes)
- [1.0.0...1.1.0](https://github.com/codaqui/libertyhub/compare/v1.0.0...v1.1.0) (Feature additions)

[Unreleased]: https://github.com/codaqui/libertyhub/compare/v2.0.2...HEAD
[2.0.2]: https://github.com/codaqui/libertyhub/compare/v2.0.1...v2.0.2
[2.0.1]: https://github.com/codaqui/libertyhub/compare/v2.0.0...v2.0.1
[2.0.0]: https://github.com/codaqui/libertyhub/compare/v1.1.1...v2.0.0
[1.1.1]: https://github.com/codaqui/libertyhub/compare/v1.1.0...v1.1.1
[1.1.0]: https://github.com/codaqui/libertyhub/compare/v1.0.0...v1.1.0
[1.0.0]: https://github.com/codaqui/libertyhub/releases/tag/v1.0.0
