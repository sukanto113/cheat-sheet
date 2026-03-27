# Requirements to Project Overview Conversion Prompt

Please analyze the following raw project requirements document(s) and convert them into a structured, Claude Code-compatible project overview. The raw docs may contain multiple languages and varying formats.

## Raw Requirements Document(s):
[PASTE YOUR RAW TEXT DOCUMENTS HERE]

---

## Instructions for Conversion:

Please create a comprehensive project overview following this exact structure:

### 1. PROJECT SUMMARY
- Extract and summarize the main project purpose in 2-3 sentences
- Identify the primary business domain/industry
- List the target users/audience

### 2. TECHNICAL REQUIREMENTS
- **Frontend Framework**: [Specify if mentioned, otherwise recommend Next.js 14]
- **Backend Requirements**: [Extract API needs, database requirements]
- **Authentication**: [Extract auth requirements]
- **Third-party Integrations**: [List any mentioned APIs, services]
- **Performance Requirements**: [Extract any speed, scalability needs]
- **Security Requirements**: [Extract security, compliance needs]

### 3. FEATURE BREAKDOWN
Organize all features into these categories:

#### Core Features (MVP)
- [List essential features for launch]

#### Secondary Features  
- [List important but not critical features]

#### Future Features
- [List nice-to-have or phase 2 features]

### 4. USER ROLES & PERMISSIONS
- [Extract different user types and their access levels]

### 5. DATA MODELS & ENTITIES
- [Identify main data objects: User, Product, Order, etc.]
- [Note relationships between entities]

### 6. API REQUIREMENTS
- [List required endpoints and their purposes]
- [Note any external API integrations]

### 7. UI/UX REQUIREMENTS
- **Design System**: [Extract design preferences, branding]
- **Responsive Requirements**: [Mobile, tablet, desktop needs]
- **Accessibility**: [Extract accessibility requirements]
- **Internationalization**: [Note multi-language support if needed]

### 8. DEVELOPMENT CONSTRAINTS
- **Timeline**: [Extract any deadlines or phases]
- **Budget Constraints**: [Note if mentioned]
- **Technology Constraints**: [Must-use or cannot-use technologies]
- **Compliance**: [GDPR, HIPAA, industry standards]

### 9. INTEGRATION REQUIREMENTS
- [List systems that need to integrate with this project]
- [Note data migration needs]

### 10. DEVELOPMENT PRIORITIES
Rank features by:
1. **High Priority** (Must have for launch)
2. **Medium Priority** (Important for user experience)  
3. **Low Priority** (Future enhancements)

### 11. CLAUDE CODE DEVELOPMENT PLAN
Create a suggested development sequence:

#### Phase 1: Foundation
- Project setup and configuration
- Basic component library
- Authentication system

#### Phase 2: Core Features
- [List core features in development order]

#### Phase 3: Enhancement
- [List secondary features]

#### Phase 4: Optimization
- Performance optimization
- Testing implementation
- Documentation

### 12. TECHNICAL ARCHITECTURE SUGGESTIONS
Based on the requirements, recommend:
- **Database**: [Suggest based on data needs]
- **Hosting/Deployment**: [Suggest based on scale]
- **State Management**: [React Query, Zustand, etc.]
- **Styling**: [Tailwind, Styled Components, etc.]

### 13. POTENTIAL CHALLENGES & CONSIDERATIONS
- [Identify complex requirements that need special attention]
- [Note any ambiguous requirements that need clarification]
- [Suggest areas where technical decisions are needed]

---

## Additional Instructions:

1. **Multi-language Support**: If the raw docs contain multiple languages, translate and consolidate all content into English while preserving all technical details.

2. **Ambiguity Resolution**: When requirements are unclear or conflicting, note these as questions that need clarification and provide reasonable assumptions.

3. **Technical Recommendations**: When specific technologies aren't mentioned, suggest modern best practices suitable for the project scale.

4. **Claude Code Compatibility**: Structure everything so that Claude Code can easily understand the project scope and generate appropriate code.

5. **Missing Information**: If critical information is missing (like user authentication details), note what needs to be clarified and provide sensible defaults.

Please ensure the output is:
- ✅ Technically detailed enough for development
- ✅ Organized for easy reference by Claude Code
- ✅ Prioritized for incremental development
- ✅ Complete with all extracted requirements
- ✅ Ready to use as project documentation