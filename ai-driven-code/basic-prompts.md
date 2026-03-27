### For setting up a new project:

```
I'm starting a new [type of project] using [programming language/framework]. Can you suggest a basic file structure and essential dependencies I should consider?
```

### For understanding AI’s capabilities:

```
What are the key strengths and limitations I should be aware of when using you for software development tasks?
```

### For creating a coding plan:

```
I want to build [brief project description]. Can you help me break this down into manageable tasks and suggest an order of implementation?
```

### add row code into a ai project - prompt

```
Can you please organize these files into a clean, maintainable folder structure that follows Next.js and backend best practices?

* Place each module in a suitable location within the project based on its purpose and usage (e.g., database connection utilities, authentication helpers, middleware).
* Feel free to split them into multiple files or folders if it improves readability, scalability, or separation of concerns.
* Follow widely accepted conventions for a modern Next.js full-stack codebase (for example: `/lib`, `/models`, `/middleware`, `/auth`, `/utils`, etc.).
* Do **not modify** the internal implementation or logic of any functions or classes — only reorganize and plan the structure.
* Clearly outline your proposed folder and file structure, including filenames and short explanations for each file’s purpose.
* Ensure that the final structure is intuitive and ready for collaborative development, debugging, and future feature expansion.
* Also, include this new project structure information into the project’s memory for future reference, so it can be reused or built upon later when adding new features or refactoring.

only do plan for it.
```

Nice — I saved that to project memory and expanded your prompt into a clear, production-ready specification you can give to an AI or a developer. Below is the **enhanced, polished prompt** (ready to paste into your task tracker, GitHub issue, or AI assistant). I kept every technical requirement you listed and tightened the language, sequencing, and acceptance criteria so the implementer knows exactly what to do.

---

### Enhanced Prompt — Implement Production-Ready Auth Flow

```
**Objective:** Implement a production-ready authentication flow for the application using Next.js, MongoDB, and Nodemailer, with UI built using ShadCN components. Follow the existing project architecture and avoid unnecessary UI changes.

### Scope & Requirements

1. **User model**

   * Create a robust `User` Mongoose model based on the project overview at `@docs/project-overview.md`.
   * Include fields for email, password hash, `passwordUpdatedAt`, `verified` flag, OTP tokens and their send/expiry timestamps, roles/permissions (if specified in docs), and any other fields required by the overview.

2. **Email (Nodemailer)**

   * Set up `nodemailer` for transactional emails (OTP, notifications, password reset).
   * Create reusable email helper utilities (templating, send function, environment-driven SMTP config).
   * Ensure OTPs and verification links can be sent reliably and securely.

3. **UI / Components**

   * Inspect `@src/components/landing/auth-modal.tsx` and separate it into smaller, maintainable components suitable for reuse in the auth flow (e.g., `AuthModal`, `LoginForm`, `RegisterForm`, `OtpForm`, `ResetPasswordForm`, `ForgotPasswordForm`).
   * Preserve the current UI look/feel. Only add or slightly adjust elements when strictly necessary for auth flow (e.g., OTP input components or validation UX).
   * Use **ShadCN** components and form primitives for forms and layout.

4. **Auth Flow (end-to-end)**

   * Implement the following flows using **Next.js server actions** and MongoDB backend:

     * **Registration** — create account, store hashed password, issue verification OTP (email), mark unverified initially.
     * **Verify Email** — verify account with email OTP; set `verified = true`.
     * **Login** — allow login via email + password; deny if not verified (with clear UI path to resend OTP).
     * **Forgot Password** — request password reset by sending an OTP or secure reset token to email.
     * **Reset Password** — validate OTP/token and allow password change; update `passwordUpdatedAt`.
     * **Resend OTP** — support resending verification or reset OTP and throttle to prevent abuse.
   * Use server actions for form submissions and secure backend logic.
   * Use `nodemailer` to send OTPs and notifications.

5. **Session Management & Cookies**

   * Respect existing cookie-session helper classes and middleware already in the codebase (do not change implementation now).
   * Integrate newly implemented endpoints with existing cookie sessions so client and middleware flow properly.

6. **Security & Best Practices**

   * Passwords must be hashed using a secure algorithm (e.g., bcrypt) before storing.
   * OTPs should be short-lived and stored hashed (preferred) with expirations.
   * Implement basic rate-limiting or throttling for OTP requests and login attempts (design-level note; implementation optional in first pass).
   * Use environment variables for secrets (SMTP config, AUTH_SECRET, etc.).
   * Ensure server actions do not leak sensitive info in responses.

7. **Project Architecture**

   * Respect the existing project architecture (as stored in project memory). Structure new files under appropriate folders such as:


8. **Deliverables & Acceptance Criteria**

   * File/folder structure plan (tree view) with short descriptions for each file created.
   * Implemented `User` model and nodemailer configuration utilities.
   * Refactored `auth-modal.tsx` into smaller components while preserving the current UI.
   * Working server actions for register/login/verify/forgot/reset flows and mail sending.
   * Minimal tests or manual test instructions (how to simulate OTP flow locally).
   * No changes to existing cookie-session helpers or middleware implementation — only integrate with them.

9. **Notes**

   * Do not modify the core logic of existing helper utilities now—only organize, integrate, and extend where necessary.
   * Keep UX consistent; if a UI tweak is necessary for security/flow (e.g., OTP input), make minimal changes and document them.
```

```md
can you analysis the project and give me a preparation plan to make the codebase preparer for testing. i see some component and class are not suitable for testing setup. please fully analysis the codebase and make to plan to migrate current code to be testable. don't need to write any test now. first i want to make the testable then i will add test on the project

-- plan for it
```

```md
1. **Initial Request**: User opened package.json and requested a comprehensive analysis of the project to create a preparation plan for making the codebase testable. They wanted:
   - Full analysis of codebase
   - Migration plan to make code testable
   - No actual test writing yet, just preparation
   - Detailed plan format
```

```md
can you foloow @docs\testing-migration\04-phase-4-server-actions.md as exactly all codes are already there. just copy past them  
and then fix only compliaiton errors. don't change any interface or business logic
```

```md
i have completed test-migration phase 1. can you please verify it and update necessery docs accoridng to guide.
```


## project estimation
```md
can you please esitmate time and budget for this porject including figma design we will apply clean solid architecture for this project. give me estimation sprint by sprint task by task with estimated time and budget. and please do deep analysis of the project requirements and give me estimation sheet

please only take Backend Developer, Frontend Developer and UI/UX Designer consideration. and calculate time only for solo person.
give me only time for the each sprint and each task. do re analysis if required. and report me only time for each sprint, task and subtask for a solo person.
```