# DWBI Data Warehouse Project

## Project Overview
The DWBI Data Warehouse Project is designed to facilitate the extraction, transformation, and loading (ETL) of data from various sources into a structured data warehouse. This project aims to provide a comprehensive solution for managing and analyzing data efficiently.

## Architecture
The architecture of the project is based on a star schema model. It includes:
- **Data Sources:** Various raw data sources including databases, APIs, and flat files.
- **ETL Process:** A robust ETL pipeline that extracts data from sources, transforms it into the desired format, and loads it into the data warehouse.
- **Data Warehouse:** A centralized repository that stores processed data for analytical querying.
- **Reporting Tools:** Integration with BI tools for data visualization and reporting.

## Project Structure
```
DWBI-Data-Warehouse-Project/
├── DWBI_Assignment.sln          # Visual Studio solution file
├── DWBI_Assignment.dtproj       # SSIS project file
├── DWBI_Assignment.database     # Database schema and objects
├── Project.params               # Project parameters and configurations
├── ETL_Master.dtsx              # Master orchestration package
├── ETL_Load_Dim_Customer.dtsx   # Customer dimension loader
├── ETL_Load_Dim_Product.dtsx    # Product dimension loader
├── ETL_Load_Dim_Supplier.dtsx   # Supplier dimension loader
├── ETL_Load_Dim_Date.dtsx       # Date dimension loader
├── ETL_Load_Fact_Sales.dtsx     # Sales fact table loader
└── ETL_Update_Returns.dtsx      # Returns data processor
```

## ETL Pipeline Overview

### Dimension Tables (Slowly Changing Dimensions)
- **Dim_Customer:** Stores customer information with SCD Type 2 logic
- **Dim_Product:** Maintains product catalog and historical changes
- **Dim_Supplier:** Tracks supplier details and relationships
- **Dim_Date:** Provides calendar dimensions for time-based analysis

### Fact Table
- **Fact_Sales:** Central fact table containing sales transactions with foreign keys to all dimensions

### ETL Packages

#### ETL_Master.dtsx
- Orchestrates the entire ETL workflow
- Manages execution order and dependencies
- Handles error logging and notifications

#### Individual Load Packages
- **ETL_Load_Dim_Customer.dtsx:** Extracts customer data, applies business rules, and loads to Dim_Customer
- **ETL_Load_Dim_Product.dtsx:** Processes product data with categorization
- **ETL_Load_Dim_Supplier.dtsx:** Loads supplier master data
- **ETL_Load_Dim_Date.dtsx:** Generates date dimension records
- **ETL_Load_Fact_Sales.dtsx:** Aggregates and loads sales transactions
- **ETL_Update_Returns.dtsx:** Handles return transactions and updates

## Requirements

### Software
- **SQL Server 2016** or higher
- **SQL Server Integration Services (SSIS)** 2016 or higher
- **Visual Studio** 2015 or higher (with SQL Server Data Tools)
- **SQL Server Management Studio (SSMS)**

### Database
- SQL Server database with appropriate permissions for creating tables and stored procedures
- Sufficient disk space for data warehouse growth

## Installation & Setup

1. **Clone the Repository:**
   ```bash
   git clone https://github.com/Deeghau0816/DWBI-Data-Warehouse-Project.git
   cd DWBI-Data-Warehouse-Project
   ```

2. **Open the Solution:**
   - Open `DWBI_Assignment.sln` in Visual Studio
   - Ensure SQL Server Data Tools (SSDT) is installed

3. **Configure Database Connection:**
   - Update connection strings in `Project.params` with your SQL Server instance details
   - Specify source database connection for data extraction

4. **Deploy SSIS Project:**
   - Right-click on the project → Deploy
   - Select target SQL Server Integration Services Catalog
   - Configure environment variables if needed

5. **Execute ETL:**
   - Run `ETL_Master.dtsx` through SQL Agent or manually from SSMS

## Configuration

### Project Parameters (Project.params)
Define key configuration parameters:
- Source database connection strings
- Target data warehouse connection string
- Data extraction parameters
- Error handling thresholds

### Connection Managers
Update the following connections:
- **Source Connections:** Point to your source systems
- **Target Connection:** SQL Server instance hosting the data warehouse

## Data Model

The project follows a **Star Schema** design:

```
                    Dim_Date
                       |
Dim_Customer -- Fact_Sales -- Dim_Product
                       |
                  Dim_Supplier
```

This schema is optimized for:
- Fast query performance
- Simplified joins
- Easy aggregations for BI tools

## Usage

### Running the ETL Pipeline

**Option 1: From SQL Server Agent**
1. Create a SQL Agent Job
2. Add a step to execute the SSIS package
3. Schedule as needed

**Option 2: Manual Execution**
1. Open SSMS
2. Connect to Integration Services
3. Right-click `ETL_Master.dtsx` → Execute
4. Monitor execution progress

### Monitoring and Troubleshooting

- **Check Execution Logs:** SSMS → Integration Services Catalog → Executions
- **Review Data Quality:** Query dimension and fact tables for completeness
- **Performance Tuning:** Analyze query execution plans and indexing strategy

## Best Practices

- Always test ETL packages in a development environment first
- Schedule incremental loads during off-peak hours
- Maintain audit logs for data lineage and compliance
- Regular backup of the data warehouse database
- Monitor disk space and ETL execution times

## Contributing

To contribute to this project:
1. Create a new branch for your feature
2. Make your changes
3. Submit a pull request with detailed descriptions

## License

This project is provided as-is for educational and business purposes.

## Support

For issues or questions, please reach out to the project maintainer or create an issue in the repository.