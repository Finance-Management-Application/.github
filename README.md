# Finance Management Application

## 1. Overview

### **Bird's Eye View**
The Finance Management Application is a tool designed for tracking and analyzing your financial data, including income, investments, and expenses. This application bridges the gap between day-to-day data entry in Excel workbooks and powerful analysis and visualization capabilities through a modern web interface.

### **Day-to-Day Workflow**
- **Data Entry:** Users will continue recording their financial data in existing Excel workbooks.
  - **Expenses:** Separate workbooks for each year, with sheets for transactions, categories, and subcategories.
  - **Income:** Separate workbooks for each year, with sheets for income streams, categories, and subcategories. 
  - **Investments:** Separate workbooks for each year, dedicated to tracking investment portfolios.
  The reason to make separate workbooks is because excel might not be able to handle high volume of rows and might get corrupt which may lead to loss or inconsistent data.
- **Data Migration:** The application supports periodic and on-demand synchronization:
  - Weekly for expenses.
  - Monthly for income and investments.
  - On demand of user, data migration can happen.
- **Analysis and Visualization:** After synchronization, users can analyze trends, track net worth, and visualize spending habits via the web application.

---

## 2. Backend Architecture

The backend follows a **microservice architecture** for scalability and maintainability. Each service is built using **FastAPI** and integrates seamlessly with PostgreSQL for data storage.

### **Microservices**
1. **Data Migration Service:**
   - Imports data from Excel files to the database.
   - Supports scheduled synchronization tasks.
   - Automatic Handling of schema changes (future feature). I NEED TO GIVE MORE THOUGHTS TO THIS.

   Tech Stack: 
   Openpyxl will be used to extract data from excel sheet
   Pydantic models are used for validating the extracted data

   Input to this service is a command

2. **Expense Management Service:**
   - Manages expense data, including transactions, categories, and subcategories.
   - Offers APIs for filtering and querying expense data.

3. **Income Management Service:**
   - Handles income data and tracks trends.
   - Provides APIs for querying income sources and history.

4. **Investment Management Service:**
   - Manages investment portfolios and performance tracking.
   - Facilitates APIs for accessing historical and real-time metrics.

5. **Analytics and Visualization Service:**
   - Performs analysis such as budgeting, trend evaluation, and net worth tracking.
   - Generates data for visualization using Chart.js (initial) and D3.js (future).

6. **Authentication and User Management Service:**
   - Implements user authentication with role-based access for the main user and guest users.
   - Prepares for token-based authentication for future mobile compatibility.

7. **Notification Service:**
   - Sends notifications for synchronization events and spending anomalies.
   - Manages notification preferences through APIs.

8. **Audit and Logging Service:**
   - Tracks data changes and synchronization activities for debugging and auditing.

### **Database**
- **Database:** PostgreSQL
- **ORM:** SQLAlchemy for database interaction, ensuring flexibility in schema management.

---

## 3. Frontend Architecture

The frontend is a **React-based web application** designed for intuitive interaction and data visualization.

### **Key Features**
- **Dashboard:** Provides a summary of income, expenses, and investments.
- **Charts and Graphs:** Visualize financial data using Chart.js and later D3.js for advanced custom visualizations.
- **Filters:** Enable filtering by time period, categories, and other criteria for granular insights.
- **User Access:** Role-based features for main users and guest users.

### **Component Structure**
- **Dashboard:** Central hub for all financial insights.
- **Expense View:** Dedicated view for exploring expense data by year, category, and subcategory.
- **Income View:** Visualize income trends and sources.
- **Investment View:** Analyze portfolio performance.
- **Settings:** Manage user preferences and synchronization schedules.

---

## 4. DevOps and Hosting

The application will be hosted on **AWS** to ensure reliability, scalability, and high availability.

### **AWS Infrastructure**
1. **Backend:**
   - Services deployed using **Amazon ECS (Elastic Container Service)** with Docker containers.
   - **AWS RDS** for PostgreSQL as the database.
   - **AWS Lambda** for running scheduled synchronization tasks.
   - **API Gateway** for secure access to backend services.

2. **Frontend:**
   - Hosted using **Amazon S3** for static assets and **CloudFront** for CDN distribution.
   - SSL/TLS for secure communication.

3. **Monitoring and Logging:**
   - **AWS CloudWatch** for logging and monitoring.
   - **AWS X-Ray** for tracing requests across microservices.

4. **Authentication and Security:**
   - **AWS Cognito** for managing user authentication and roles.
   - **IAM Roles** for access control to AWS resources.

5. **CI/CD Pipeline:**
   - **AWS CodePipeline** integrated with GitHub for continuous integration.
   - **AWS CodeBuild** for automated builds.
   - **AWS CodeDeploy** for deploying updates seamlessly.
