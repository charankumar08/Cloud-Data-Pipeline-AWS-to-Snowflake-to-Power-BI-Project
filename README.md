

# ❄️ Cloud Data Pipeline: AWS to Snowflake to Power BI Project

## 📌 Project Overview
This project showcases a complete **Modern Data Stack** pipeline. I engineered a solution to move agricultural datasets from local environments to the cloud, specifically targeting crop yield analysis, seasonal price fluctuations, and environmental impacts.

By integrating **Amazon S3**, **Snowflake**, and **Power BI**, I built a scalable system that transforms raw CSV data into actionable business intelligence.

---

## 🏗️ Architecture Flow
1. **Source:** Raw Agricultural Data (Weather, Soil, Yields).
2. **Storage:** **Amazon S3** (Object Storage) used as a landing zone.
3. **Security:** **AWS IAM** Role-based access with specialized Trust Policies for secure Snowflake communication.
4. **Warehouse:** **Snowflake** (Cloud Data Platform) for data storage, schema management, and ingestion.
5. **BI Layer:** **Power BI** for interactive dashboards and data storytelling.

---

## 🛠️ Tech Stack & Skills
*   **Cloud Storage:** Amazon S3
*   **Data Warehouse:** Snowflake
*   **Cloud Security:** AWS IAM (Keyless Authentication via Storage Integrations)
*   **Data Viz:** Power BI (DirectQuery/Import)
*   **Language:** SQL (Snowflake Dialect)

---

## 🚀 Step-by-Step Implementation

### 1. Secure Cloud Handshake (AWS & Snowflake)
Instead of using risky access keys, I implemented a **Storage Integration** object. This creates a secure "handshake" between AWS and Snowflake using an IAM Role ARN and an External ID.

```sql
CREATE OR REPLACE STORAGE INTEGRATION PBI_Integration
  TYPE = EXTERNAL_STAGE
  STORAGE_PROVIDER = 'S3'
  ENABLED = TRUE
  STORAGE_AWS_ROLE_ARN = 'arn:aws:iam::825765422200:role/powerbi.role'
  STORAGE_ALLOWED_LOCATIONS = ('s3://powerbi.project/');
```

### 2. Data Infrastructure
I designed a structured schema in Snowflake to house the `PBI_Dataset`. The table captures 12 critical variables including:
*   **Environmental:** Rainfall, Temperature, Humidity.
*   **Agricultural:** Soil Type, Irrigation, Season.
*   **Economic:** Crop Prices and Yields.

#### 3. Data Transformation & Visualization
* Processed raw crop and weather data (Year, Location, Rainfall, Temperature, etc.).
* Connected Power BI to Snowflake using the **Snowflake Connector**.
* Built a dynamic dashboard to analyze crop yields and seasonal patterns.

### 🧠 What I Learned
* **Cloud Security:** Deep understanding of IAM Roles, Trust Relationships, and External IDs.
* **Scalability:** How to handle data in a way that works for 1,000 rows or 1 billion rows.
* **Integration:** Managing the "Handshake" between different cloud ecosystems.

### 4. Automated Ingestion
Using an **External Stage**, I created a pipeline to bulk-load data directly from S3:
```sql
COPY INTO PBI_Dataset 
FROM @pbi_stage
FILE_FORMAT = (TYPE=CSV FIELD_DELIMITER=',' SKIP_HEADER=1)
ON_ERROR = 'CONTINUE';
```

---

## 📈 Key Insights & Learning
*   **IAM Mastery:** Learned how to configure Trust Relationships and Permission Policies to ensure "Least Privilege" security.
*   **Data Lifecycle:** Managed the entire flow from raw CSV to a structured Snowflake table ready for BI consumption.
*   **Error Handling:** Implemented `ON_ERROR = 'CONTINUE'` to ensure pipeline resilience during bulk loads.
*   **Cloud Integration:** Successfully connected Power BI to Snowflake to visualize crop performance based on seasonal rainfall and soil types.

---

## 📂 Project Structure
*   `Scripts/`: Contains the full `snowflake_setup.sql` logic.
*   `Data/`: Schema definitions and sample agricultural data.
*   `Dashboard/`: Power BI `.pbix` files and visualization exports.

---

## 🔗 Connect with me
**Charan Kumar Donthula**
*   **LinkedIn:** [Charan Kumar Donthula](https://linkedin.com)
*   **GitHub:** [charankumar08](https://github.com)
