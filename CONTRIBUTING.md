# Contributing to Asset 360 Experience API

Thank you for your interest in contributing to the Asset 360 Experience API! This document provides guidelines and information for contributors.

## Table of Contents
- [Getting Started](#getting-started)
- [Development Process](#development-process)
- [API Specification Guidelines](#api-specification-guidelines)
- [Submission Guidelines](#submission-guidelines)
- [Code of Conduct](#code-of-conduct)

## Getting Started

### Prerequisites
- Basic understanding of OpenAPI 3.0 specification
- Knowledge of REST API design principles
- Familiarity with MuleSoft Anypoint Platform (helpful but not required)
- Understanding of industrial asset management systems (Maximo, SCADA)

### Local Development Setup
1. Fork this repository
2. Clone your fork locally:
   ```bash
   git clone https://github.com/YOUR_USERNAME/asset-360-experience-api.git
   cd asset-360-experience-api
   ```
3. Create a feature branch:
   ```bash
   git checkout -b feature/your-feature-name
   ```

## Development Process

### Making Changes
1. **Review the API specification**: Understand the current `openapi.yaml` structure
2. **Follow REST API best practices**: Ensure your changes align with REST principles
3. **Maintain consistency**: Keep naming conventions and response formats consistent
4. **Update documentation**: Modify README.md and deployment guides as needed

### Testing Changes
- Validate OpenAPI specification using online validators
- Test API documentation rendering
- Ensure examples are accurate and helpful

## API Specification Guidelines

### Naming Conventions
- Use kebab-case for endpoint paths: `/assets/{assetId}/sensor-data`
- Use camelCase for JSON property names: `operationalStatus`
- Use clear, descriptive names for parameters and responses

### Response Format Standards
- Always include appropriate HTTP status codes
- Provide meaningful error responses with error codes
- Include comprehensive examples for all responses
- Use consistent data types across endpoints

### Documentation Requirements
- All endpoints must have clear descriptions
- Parameters must include type, format, and validation rules
- Response schemas must be well-defined
- Include realistic examples for requests and responses

## Submission Guidelines

### Pull Request Process
1. **Create descriptive commits**: Use clear, concise commit messages
2. **Update documentation**: Ensure all changes are reflected in documentation
3. **Test thoroughly**: Validate your OpenAPI specification
4. **Submit pull request**: Include a detailed description of changes

### Pull Request Template
```markdown
## Description
Brief description of the changes

## Type of Change
- [ ] Bug fix
- [ ] New feature
- [ ] Breaking change
- [ ] Documentation update

## Changes Made
- List specific changes
- Include any new endpoints or modifications
- Note any breaking changes

## Testing
- [ ] OpenAPI specification validates
- [ ] Documentation renders correctly
- [ ] Examples are accurate

## Checklist
- [ ] Code follows project conventions
- [ ] Documentation updated
- [ ] Changes tested
- [ ] No sensitive information included
```

### Review Process
1. Automated validation checks must pass
2. At least one maintainer review required
3. All feedback must be addressed
4. Final approval from project maintainer

## API Design Principles

### RESTful Design
- Use HTTP methods appropriately (GET, POST, PUT, DELETE)
- Design resource-oriented URLs
- Return appropriate HTTP status codes
- Follow stateless communication principles

### Data Models
- Keep response models consistent
- Use appropriate data types (string, integer, boolean, array)
- Include validation rules where applicable
- Provide clear property descriptions

### Error Handling
- Use standard HTTP status codes
- Provide informative error messages
- Include error codes for programmatic handling
- Maintain consistent error response format

## Deployment Considerations

### Anypoint Exchange Compatibility
- Ensure OpenAPI 3.0 compliance
- Include all required metadata
- Test deployment to sandbox environment
- Validate documentation rendering in Exchange

### Version Management
- Follow semantic versioning (semver)
- Document breaking changes clearly
- Provide migration guides when necessary
- Maintain backward compatibility when possible

## Code of Conduct

### Our Standards
- Be respectful and inclusive
- Provide constructive feedback
- Focus on what is best for the community
- Show empathy towards other community members

### Unacceptable Behavior
- Harassment or discriminatory language
- Personal attacks or trolling
- Publishing private information without permission
- Unprofessional conduct

## Getting Help

### Resources
- [OpenAPI 3.0 Specification](https://swagger.io/specification/)
- [MuleSoft API Design Best Practices](https://docs.mulesoft.com/)
- [REST API Design Guidelines](https://restfulapi.net/)

### Support Channels
- Create an issue for bugs or feature requests
- Start a discussion for questions or ideas
- Contact maintainers for security issues

## Recognition

Contributors will be recognized in our README.md file and release notes. We appreciate all contributions, whether they're code changes, documentation improvements, or community support.

Thank you for contributing to the Asset 360 Experience API project!
