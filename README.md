Here’s the updated **README.md** based on your request:

---

# **Second Creator**

Welcome to **Second Creator**, a dynamic project creation tool that leverages data from Second Brain systems like ChatGPT JSON history, markdown notes, and other personal knowledge management tools. This project is built using **Nuxt.js**, **Nitro server**, **PostgreSQL** with **Drizzle ORM**, and is designed for incremental development, versioning, and audit tracking through a structured Request for Change (RFC) workflow.

## **Project Overview**

The goal of this project is to dynamically aggregate inputs from Second Brain instances, organize project versions, track changes using RFCs, and maintain a full audit history. The system supports collaboration with version control and a dashboard for monitoring project states.

## **Table of Contents**

1. [Tech Stack](#tech-stack)
2. [File Structure](#file-structure)
3. [Installation](#installation)
4. [Usage](#usage)
   - [Running the Project](#running-the-project)
   - [Working with Projects](#working-with-projects)
   - [Syncing with Second Brain Inputs](#syncing-with-second-brain-inputs)
   - [Request for Changes (RFCs)](#request-for-changes-rfcs)
   - [Audit Logs](#audit-logs)
5. [Collaboration](#collaboration)
   - [Code Contributions](#code-contributions)
   - [RFC Workflow](#rfc-workflow)
6. [Testing](#testing)

---

## **Tech Stack**

- **Frontend**: Nuxt.js (with Vercel hosting)
- **Backend**: Nitro Server (API and server-side logic)
- **Database**: PostgreSQL (with Drizzle ORM)
- **Testing**: Vitest for unit/integration tests, Cypress for E2E
- **Data Sources**: Second Brain systems (ChatGPT JSON exports, markdown files, etc.)

---

## **File Structure**

This project follows a **modular and scalable structure**. Here’s an overview of the key folders and files:

```bash
├── src
│   ├── client                      # Client-side code (Nuxt.js frontend)
│   │   ├── components              # Reusable UI components
│   │   ├── pages                   # Nuxt.js pages (automatically mapped to routes)
│   │   ├── stores                  # State management (Pinia stores)
│   │   ├── composables             # Reusable business logic (composable functions)
│   │   ├── assets                  # Static assets (images, fonts)
│   │   ├── middleware              # Client-side route protection, data loading
│   │   └── utils                   # Utility functions (validation, formatting)
│   ├── server                      # Server-side code (Nitro API and business logic)
│   │   ├── routes                  # API routes (RESTful API)
│   │   ├── services                # Core business logic (e.g., project and RFC management)
│   │   ├── repositories            # Database layer (Drizzle ORM + PostgreSQL)
│   │   └── middleware              # Server-side middleware (authentication, logging)
│   ├── db                          # Database migration and schema files
│   ├── tests                       # Automated tests
│   │   ├── unit                    # Unit tests (for services, repositories)
│   │   ├── integration             # Integration tests (API and database interaction)
│   │   └── e2e                     # End-to-end tests (for dashboards and user flows)
│   ├── config                      # Application configuration files (environment)
│   └── logs                        # Logs for error tracking and audit trails
├── public                          # Publicly accessible static files (favicon, robots.txt)
├── scripts                         # Scripts for build and deployment
├── nuxt.config.ts                  # Nuxt.js configuration
├── drizzle.config.ts               # Drizzle ORM configuration
└── README.md                       # Documentation (this file)
```

### **Key Folders:**

- **client/components/**: Contains reusable Vue components for the frontend, such as project listings, RFC forms, and dashboard visualizations.
  
- **server/services/**: Contains business logic services such as `ProjectService`, `RFCService`, and `SecondBrainService` for handling core functionality like creating projects, managing RFCs, and syncing data from Second Brain systems.
  
- **server/repositories/**: Contains the database interaction layer. Each repository corresponds to a specific domain (projects, versions, RFCs, etc.), ensuring separation of concerns.
  
- **db/**: Includes database migration scripts and schema definitions using Drizzle ORM to ensure proper versioning and evolution of the database schema.

- **tests/**: Organized into unit, integration, and end-to-end (E2E) tests to ensure robustness and correct behavior of all features.

---

## **Installation**

### **Prerequisites**

- Node.js v16+ and npm
- PostgreSQL (local or hosted, e.g., Supabase or ElephantSQL)
- Vercel account (optional for deployment)

### **Steps**

1. Clone the repository:
   ```bash
   git clone https://github.com/your-username/second-creator.git
   cd second-creator
   ```

2. Install dependencies:
   ```bash
   npm install
   ```

3. Set up the PostgreSQL database:
   - Create a PostgreSQL database.
   - Copy `.env.example` to `.env` and update the database connection details:
     ```bash
     cp .env.example .env
     ```

4. Run database migrations:
   ```bash
   npm run migrate
   ```

5. Run the project:
   ```bash
   npm run dev
   ```

6. Open the project in your browser at `http://localhost:3000`.

---

## **Usage**

### **Running the Project**

After following the installation steps, run the project using `npm run dev`. The main pages you will interact with:

- **Home/Dashboard** (`/`): A dashboard view displaying current projects, RFCs, and system logs.
- **Projects** (`/project/[id]`): Detailed view for individual projects, showing its versions, RFCs, and related inputs.
- **RFCs** (`/project/rfc`): Manage the request for changes to track and control project updates.
- **Audit Logs** (`/project/audit`): Full audit logs showing changes over time and who made them.

### **Working with Projects**

- **Create a Project**: Use the form on the homepage to add a new project. You can also upload related files (markdown, JSON outputs) to store as part of the project.
- **Versioning**: Each project tracks incremental versions. You can add new versions manually or trigger them through incoming RFCs or Second Brain inputs.

### **Syncing with Second Brain Inputs**

Second Brain inputs (such as ChatGPT JSON exports or markdown notes) can be synced to a project via the API or directly through the UI. Here's how it works:

1. **ChatGPT History**: Upload JSON output from ChatGPT sessions. The system will parse the data and associate it with a relevant project or RFC.
2. **Notes or Markdown Files**: Upload markdown or notes from other tools (e.g., Notion, Obsidian). These notes will be categorized and stored for future reference.

### **Request for Changes (RFCs)**

RFCs allow structured management of project changes:

1. **Create an RFC**: Propose a change, including detailed descriptions of what needs to be updated.
2. **Approval Workflow**: Each RFC goes through an approval process, which may involve multiple stakeholders.
3. **Linking to Versions**: Once approved, RFCs automatically generate a new project version and log all changes in the audit trail.

### **Audit Logs**

Audit logs track every change made to the system, including project updates, RFC approvals, and syncs with Second Brain inputs. This ensures transparency and traceability.

---

## **Collaboration**

### **Code Contributions**

We welcome contributions from the community! Please follow these steps:

1. **Fork the Repository**: Fork the repo and create your own branch:
   ```bash
   git checkout -b feature/new-feature
   ```

2. **Make Changes**: Develop your feature or bugfix, ensuring to write unit or integration tests where applicable.

3. **Run Tests**: Run all tests before pushing changes:
   ```bash
   npm run test
   ```

4. **Submit a Pull Request (PR)**: Open a PR on the main repository, detailing what you changed and how it was tested.

### **RFC Workflow**

For larger changes, we encourage contributors to follow an RFC process:

1. **Create an RFC**: Open an issue in GitHub with the **RFC** template, detailing the proposed changes and rationale.
2. **Discussion**: Team members and contributors will review the RFC and discuss potential impacts.
3. **Approval**: Once approved, the changes can be implemented, and the RFC will be logged into the project system for tracking.

---

## **Testing**

This project has full test coverage, including unit, integration, and E2E tests.

- **Run Unit Tests**:
  ```bash
  npm run test:unit
  ```

- **Run Integration Tests**:
  ```bash
  npm run test:integration
  ```

- **Run End-to-End Tests (E2E)**:
  ```bash
  npm run test:e2e
  ```

Tests ensure that the core features (project management, RFCs, syncing with Second Brain inputs, etc.) work as expected.

---

## **Environment Variables (Sample `.env` file

)**

To configure your environment, create a `.env` file at the root of the project and include the following environment variables:

```bash
DATABASE_URL=postgres://username:password@localhost:5432/second_creator_db
JWT_SECRET=your_jwt_secret_key
NODE_ENV=development
```

- **`DATABASE_URL`**: The connection string for your PostgreSQL database.
- **`JWT_SECRET`**: Secret key used for signing JWT tokens.
- **`NODE_ENV`**: The environment in which the application is running (`development`, `production`, etc.).

---

### **Dependencies**

All dependencies are managed in the `package.json` file. Here's a summary of the major dependencies:

```json
"dependencies": {
  "nuxt": "^3.0.0",
  "@nuxtjs/pinia": "^0.3.0",
  "drizzle-orm": "^0.10.0",
  "pg": "^8.7.1",
  "express": "^4.17.1",
  "shadcn": "^0.2.0",
  "axios": "^0.26.0",
  "jsonwebtoken": "^8.5.1",
  "bcryptjs": "^2.4.3",
  "dotenv": "^10.0.0",
  "chalk": "^4.1.0",
  "dayjs": "^1.10.6",
  "uuid": "^8.3.2"
},
"devDependencies": {
  "@types/node": "^16.11.7",
  "@types/pg": "^8.6.0",
  "@types/jest": "^26.0.24",
  "typescript": "^4.5.4",
  "eslint": "^7.32.0",
  "eslint-plugin-vue": "^7.17.0",
  "vitest": "^0.0.117",
  "cypress": "^9.5.0",
  "nodemon": "^2.0.15",
  "ts-node": "^10.4.0",
  "jest": "^27.4.7",
  "husky": "^7.0.4",
  "lint-staged": "^12.1.3",
  "drizzle-kit": "^0.10.0"
}
```

---

## **Contact**

For any questions or help, please reach out to the project maintainers via GitHub issues or pull requests. We look forward to your contributions!

---
