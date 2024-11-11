# Jupyter Notebook Pipeline Example

This project demonstrates how to create a production-ready data pipeline using multiple Jupyter notebooks, where one notebook orchestrates the execution of another. It simulates a common enterprise scenario where analytical procedures (typically in SAS, R, or specialized SQL procedures) need to be executed for multiple providers, with results aggregated into individual reports.

## Overview

The project consists of two main notebooks:
1. `py_example.ipynb` - The orchestrator notebook that manages the pipeline execution
2. `sql_example.ipynb` - The analytical notebook containing SQL procedures

This pattern can be useful when:
- Converting legacy SAS/SQL procedures to modern Python pipelines
- Maintaining separation between business logic and orchestration
- Running the same analysis for multiple clients/providers
- Generating individual reports from a standardized analytical process

## Components

### Python Orchestrator (`py_example.ipynb`)

This notebook manages the pipeline execution:
- Loads provider data from a predefined structure
- Injects parameters into the SQL notebook
- Executes the SQL notebook for each provider
- Generates Excel reports from the results

Key functions:
- `execute_sql_notebook()`: Executes the SQL notebook with provider-specific parameters
- `create_excel_report()`: Generates provider-specific Excel reports
- `process_providers()`: Main processing loop for all providers

### SQL Analysis (`sql_example.ipynb`)

This notebook contains the analytical procedures:
- Creates a temporary SQLite database
- Performs various payment analyses using SQL
- Returns structured results for report generation

Analysis includes:
- Payment summaries
- Monthly trends
- Payment distribution statistics

## Sample Data Structure

The pipeline expects provider data in the following format:
```python
provider_data = {
    'provider_id': [1001, 1002, 1003],
    'provider_name': ['Alpha Payments', 'Beta Financial', 'Gamma Processing'],
    'month_1_payments': [150000, 225000, 175000],
    'month_2_payments': [165000, 215000, 180000],
    'month_3_payments': [175000, 235000, 165000],
    'month_4_payments': [180000, 245000, 190000],
    'output_file': ['alpha_report.xlsx', 'beta_report.xlsx', 'gamma_report.xlsx']
}
```

## Setup and Requirements

### Dependencies
```
pandas>=2.0.0
notebook>=7.0.0
nbformat>=5.9.0
nbconvert>=7.8.0
openpyxl>=3.1.2
```

### Installation
1. Create a Python virtual environment
```bash
python -m venv .venv
source .venv/bin/activate  # On Windows: .venv\Scripts\activate
```

2. Install required packages
```bash
pip install -r requirements.txt
```

## Usage

1. Ensure both notebooks are in the same directory
2. Open and run `py_example.ipynb`
3. The notebook will:
   - Create sample provider data
   - Execute the SQL analysis for each provider
   - Generate individual Excel reports

## Output

For each provider, an Excel file is generated containing:
- Payment summary statistics
- Monthly payment trends
- Payment distribution analysis

## Extending the Project

This example can be extended by:
1. Adding more complex SQL analyses
2. Modifying the report format
3. Adding data validation
4. Implementing error recovery
5. Adding logging and monitoring
6. Integrating with scheduling systems

## Best Practices

1. Keep analytical logic (SQL) separate from orchestration (Python)
2. Use proper error handling and logging
3. Parameterize all provider-specific values
4. Maintain clear documentation
5. Include data validation steps
6. Consider performance optimization for large datasets

## Limitations

1. In-memory SQLite database (could be replaced with production database)
2. Basic error handling
3. Simple report format
4. No data validation
5. No performance optimization
