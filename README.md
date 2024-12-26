# Finance Management Application

## 1. Overview

### **Bird's Eye View**
The Finance Management Application is a comprehensive tool designed for tracking, analyzing, and visualizing financial data, including income, investments, and expenses. It bridges the gap between day-to-day data entry in Excel workbooks and powerful analysis via a modern web interface.

### **Day-to-Day Workflow**
- **Data Entry:** 
  - Users record financial data in separate Excel workbooks for each year.
  - Categories:
    - **Expenses:** Transactions, Category, and Sub Category.
    - **Income:** Income, Income streams
    - **Investments:** Investment, Asset Class.

  _Note: The yearly workbook format minimizes risks of data corruption from large datasets._

- **Data Migration:** The application supports:
  - **Weekly synchronization** for expenses.
  - **Monthly synchronization** for income and investments.
  - **On-demand synchronization** triggered by the user.

- **Analysis and Visualization:** The synchronized data is analyzed for trends, net worth tracking, and spending insights via the web interface.

---

## 2. Backend Architecture

The backend uses a **microservice architecture** to ensure scalability and maintainability. Each service is developed using **FastAPI** and utilizes **PostgreSQL** for storage.

### **Microservices**

#### **1. Data Extraction Service** 
- **Purpose:** Extracts and validates data from Excel files stored in a predefined folder hierarchy.
- **Endpoints:**
  - `GET /transactions` – Retrieve transactions (supports pagination).
  - `GET /transactions/all` – Retrieve all transactions.
  - `GET /categories` – Retrieve all categories.
  - `GET /subcategories` – Retrieve all subcategories.
  - `GET /products` – Extract products from the expense workbook.
  - `POST /validate` – Validate the structure and data of an uploaded Excel file.
- **Data Folder Hierarchy:**
  ```
  data/
    income/
      2024/
      2023/
    investment/
      2024/
      2023/
    expense/
      2024/
      2023/
  ```
- **Tech Stack:** 
  - **Openpyxl** for data extraction.
  - **Pydantic** for validation.
- _Future Enhancements:_ Automated schema evolution handling.

#### **2. Expense Management Service**
- Manages expenses, including transactions, categories, and subcategories.
- Provides APIs for advanced filtering and querying.

#### **3. Income Management Service**
- Tracks income sources, trends, and history.
- Offers APIs for querying and data retrieval.

#### **4. Investment Management Service**
- Handles portfolio tracking and performance metrics.
- Provides APIs for accessing historical and real-time data.

#### **5. Analytics and Visualization Service**
- Enables budget analysis, trend evaluation, and net worth tracking.
- Generates visualization data using **Chart.js** (initial) and **D3.js** (future).

#### **6. Authentication and User Management Service**
- Implements user authentication with role-based access control.
- Prepares for token-based authentication for mobile support.

#### **7. Notification Service**
- Sends alerts for synchronization events and anomalies in spending.
- Provides APIs to manage notification preferences.

#### **8. Audit and Logging Service**
- Tracks data changes and synchronization activities for auditing and debugging.

### **Database**
- **Database:** PostgreSQL.
- **ORM:** SQLAlchemy for schema management and interactions.

---

## 3. Frontend Architecture

The frontend is a **React-based** application, providing a user-friendly interface and robust data visualization.

### **Key Features**
- **Dashboard:** Overview of income, expenses, and investments.
- **Visualization:** Interactive charts using **Chart.js** and **D3.js**.
- **Filtering:** Granular filtering options by time, category, and subcategory.
- **Role-Based Access:** Custom views for main and guest users.

### **Component Structure**
1. **Dashboard:** Central hub for financial insights.
2. **Expense View:** Explore expenses by year, category, and subcategory.
3. **Income View:** Analyze income trends and sources.
4. **Investment View:** Track portfolio performance.
5. **Settings:** Manage preferences and synchronization schedules.

---

## 4. DevOps and Hosting

The application is deployed on **AWS** to ensure scalability, reliability, and security.

### **AWS Infrastructure**

#### **Backend**
- **Amazon ECS:** Hosts backend microservices using Docker containers.
- **AWS RDS:** PostgreSQL database for data persistence.
- **AWS Lambda:** Executes scheduled synchronization tasks.
- **API Gateway:** Facilitates secure access to backend services.

#### **Frontend**
- **Amazon S3:** Hosts static assets for the React application.
- **CloudFront:** Ensures fast content delivery via CDN.
- **SSL/TLS:** Secures communication.

#### **Monitoring and Logging**
- **AWS CloudWatch:** Tracks application logs and performance.
- **AWS X-Ray:** Provides distributed tracing across microservices.

#### **Authentication and Security**
- **AWS Cognito:** Manages user authentication and role-based access.
- **IAM Roles:** Ensures secure access to AWS resources.

#### **CI/CD Pipeline**
- **AWS CodePipeline:** Automates deployment pipelines.
- **AWS CodeBuild:** Compiles and builds the application.
- **AWS CodeDeploy:** Ensures seamless updates to the application.
