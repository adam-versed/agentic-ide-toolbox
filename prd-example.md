# Project Requirements Document (PRD)

## 1. Project Overview

This project is about building a data pipeline that automatically retrieves information about street food vendors from Instagram and X.com (formerly Twitter) by leveraging an Apify feed. The main goal is to detect posts by street food vendors within a specific geographic area – starting with Greater Bristol, UK – and extract key details such as serving times, locations, food images, menus (which might be in text or image form), and customer reviews. The collected data will then be categorized and stored with rich metadata against each social media profile handle, ensuring that duplicate records are minimized while allowing updates to existing vendor profiles.

The pipeline is being built primarily as a prototype that runs on macOS for proof-of-concept purposes. However, the design is intended to be scalable so that it can easily transition into a production system with minimal refactoring. Success will be measured by whether the pipeline effectively retrieves organized and searchable street food vendor data from the Apify feed on schedule, making it useful for street food enthusiasts, vendors, food bloggers, and tech-savvy locals.

## 2. MoSCoW prioritised features

### Must Have

- Yarn package management setup with TypeScript configuration
- Apify API client initialization and configuration management
- Environment variable handling for Apify credentials
- Basic request/response types for Actor calls
- Error handling middleware for Apify service calls
- Health check endpoint
- Request validation middleware
- TypeScript types for Actor input/output

### Should Have

- Request rate limiting
- Request logging
- Actor call timeout handling
- Retry mechanism for failed Actor calls
- Documentation for common Actor call patterns
- Example Actor call implementation

### Could Have

- Actor call status monitoring
- Response caching mechanism
- Batch Actor call handling
- Actor call statistics
- OpenAPI/Swagger documentation

### Won't Have

- Database integration
- MCP specific implementations
- Complex authentication (beyond API key)
- Specific Actor business logic
- Data transformation logic

## 3. Target users and their motivations

- Street Food Enthusiasts:

  - Individuals who enjoy discovering and trying new street food but lack a reliable way to find vendors and reviews.

- Street Food Vendors:

  - Small food businesses looking to increase visibility, attract more customers, and share updates about their offerings.

- Food Bloggers and Influencers:

  - People who enjoy sharing food experiences online and rely on tools to discover unique and popular food vendors.

- Tech-Savvy Locals:

  - Individuals who enjoy using apps and digital platforms to explore food options and prefer convenience.

## 4. Non-Functional Requirements

- **Performance:**

  - The data pipeline should reliably execute its process every 6 hours without failure.
  - Although processing is offline, the system should handle data extraction and storage efficiently, even as data volume grows.

- **Security:**

  - All stored data must be protected with encryption protocols where necessary.
  - The system must comply with data protection and privacy regulations concerning personal information.

- **Scalability:**

  - The architecture must allow for easy scaling from a prototype to a production-level system with minimal changes.
  - The selected database solution should handle increased data load and more expansive geographic coverage.

- **Usability:**

  - Data should be stored in a well-indexed, searchable format to facilitate integration with future tools like NLP sentiment analysis systems.

## 5. Constraints & Assumptions

- The prototype will run on macOS, but the design should ensure easy transition to a production environment.
- The project does not involve real-time user interaction; it is a backend data pipeline that operates on a 6-hour schedule.
- It is assumed that the relevant Apify feed provides consistent and reliable data from both Instagram and X.com.
- The system should be prepared for future integration with tools like sentiment analysis, but that integration will not be part of the current build.
- Data privacy regulation compliance may require encryption for any potentially sensitive information (e.g., email, telephone numbers, names).

## 6. Known Issues & Potential Pitfalls

- **API and Feed Rate Limits:**

  - Social media platforms or the Apify service may have API rate limits that could affect data retrieval.
  - Mitigation: Monitor API usage and incorporate back-off strategies in the event of hitting rate limits.

- **Data Format Variability:**

  - Social media posts may have inconsistent formats or embedded data (e.g., text vs. image information for menus), which can complicate the extraction process.
  - Mitigation: Build flexible parsers and design rigorous data validation checks.

- **Duplicate Data Handling:**

  - Duplicate posts or vendor updates must be accurately recognized to avoid redundancy.
  - Mitigation: Design a robust deduplication mechanism that uses social media profile handles and timestamps as unique identifiers.

- **Scaling Challenges:**

  - Moving the pipeline from a local macOS prototype to a renowned production environment may surface unforeseen scalability and performance issues.
  - Mitigation: Choose a database and cloud storage solution that are known for scalability and test early with larger data sets.

- **Legal and Compliance Risks:**

  - Handling personal data, even if publicly available, may pose compliance challenges.
  - Mitigation: Incorporate secure encryption methods for sensitive data and perform regular reviews of data privacy practices.

This document serves as the primary guide for building the data pipeline and will be the foundation for all subsequent technical documents. Every detail, from data extraction to storage and security, has been outlined to ensure that the final system is robust, scalable, and compliant, while meeting all the project’s core objectives.
