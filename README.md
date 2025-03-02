# dbt_practice

### **1. Set up my environment**
1. **Install dbt**:
   - Use pip to install dbt:
     ```bash
     pip install dbt-core dbt-snowflake
     ```
     ```bash
     pip install dbt-core dbt-postgres
     ```

2. **Set up database**:
   - Create access to a database to run and test dbt models (Snowflake).
   - Need database credentials (host, port, database name, user, password).

---

### **2. Initialize a dbt project**
1. **Create a New dbt Project**:
   - Run the following command to create a new dbt project:
     ```bash
     dbt init dbt_test_project
     ```
   - This will create a directory structure like:
     ```
     dbt_test_project/
     ├── dbt_project.yml
     ├── models/ (**handle the transformation of data (usually from sources / seeds) for downstream users)
     ├── snapshots/ (**used to track changes within datasets)
     ├── tests/ (**can validata 'sources', 'seeds', 'models', and even 'snapshots')
     ├── macros/
     └── seeds/ (**feed initial data to dbt)
     ```

2. **Navigate to the project directory**:
   ```bash
   cd dbt_test_project
   ```

3. **Set up the yet another mark-up language with `profiles.yml`**:
   - Create a `profiles.yml` file in `~/.dbt/` (home directory) or update the existing one with the database connection details:
     ```yaml
     dbt_test_project:
       outputs:
         dev:
           type: postgres
           host: localhost
           user: your_username
           password: your_password
           port: 5432
           dbname: your_database
           schema: public
       target: dev
     ```

---

### **3. Add models and tests**
1. **Create a basic model**:
   - Add a SQL file in the `models/` folder:
     `models/example_model.sql`
     ```sql
     SELECT 
         id,
         name,
         COUNT(*) AS total_orders
     FROM raw_data.orders
     GROUP BY id, name
     ```

2. **Define a schema file for testing**:
   - Add a `schema.yml` file in the `models/` folder:
     `models/schema.yml`
     ```yaml
     version: 2
     models:
       - name: example_model
         description: "A model summarizing order counts by customer."
         columns:
           - name: id
             description: "The customer ID."
             tests:
               - unique
               - not_null
           - name: total_orders
             description: "The total number of orders per customer."
     ```

3. **Run tests**:
   - Testing my model using:
     ```bash
     dbt test
     ```

---

### **4. Initialize a GitHub repository**
1. **Create a New Repository**:
   - Go to [GitHub](https://github.com) and create a new repository (`dbt_practice`).

2. **Initialize Git in the project directory**:
   ```bash
   git init
   git add .
   git commit -m "Initial commit: Add dbt test project"
   ```

3. **Connect to GitHub**:
   - Add the GitHub repository as a remote:
     ```bash
     git remote add origin https://github.com/your-username/dbt_test_project.git
     ```

4. **Push to GitHub**:
   ```bash
   git branch -M main
   git push -u origin main
   ```

---

### **5. Run and practice**
1. **Run the dbt project**:
   - Execute the models:
     ```bash
     dbt run
     ```

2. **Test Your Models**:
   - Run tests:
     ```bash
     dbt test
     ```

3. **Practice Enhancements**:
   - Add more models, tests, or macros.
   - Practice using `dbt seed` to load sample data from CSV files.
   - Try defining sources in a `sources.yml` file.

---

### **6. Share and Collaborate**
- Sharing the GitHub repository link with others allows for feedback or collaboration.  
- Adding a `README.md` file explains the purpose of my project and a high-level overview on how to use it.  
