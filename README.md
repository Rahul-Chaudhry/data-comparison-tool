# Data Comparison Tool

Compare the results of a SQL Server query and an Amazon Redshift query. The
project checks column names, row counts, duplicate records, records found in
only one source, and individual values for matching records. It writes an
Excel workbook with a separate worksheet for each result.

## Start in JupyterLab

Clone the repository, create a virtual environment, and install JupyterLab:

    git clone https://github.com/YOUR-USERNAME/data-comparison-tool.git
    cd data-comparison-tool
    python3 -m venv .venv
    source .venv/bin/activate
    python3 -m pip install jupyterlab
    jupyter lab

On Windows PowerShell, activate the environment with:

    .venv\Scripts\Activate.ps1

## Configure credentials

Copy .env.example to .env and replace every placeholder with your real
connection details. The .env file is ignored by Git, so credentials are not
committed.

    cp .env.example .env

The SQL Server machine needs an appropriate Microsoft ODBC driver. The
notebook uses standard Redshift username/password authentication; use a
read-only database account wherever possible.

## Run the comparison

1. Open notebooks/compare_sql_server_redshift.ipynb.
2. Uncomment and run the individual package-install lines if needed.
3. Edit SQL_SERVER_QUERY, REDSHIFT_QUERY, and KEY_COLUMNS.
4. Select Run All Cells.

The workbook is saved in outputs/comparison_report.xlsx. It contains a
summary, column comparison, source-only records, duplicate rows, and
value-level differences.

## Project layout

    notebooks/      All executable project code
    data/           Optional non-sensitive sample data
    outputs/        Generated comparison workbooks, ignored by Git
    documentation/  Connection and query notes
    .env.example    Credential template; copy it to .env locally

## Important comparison rule

KEY_COLUMNS must identify one logical row. The notebook reports duplicate keys
before comparing values. If the two systems use different column names or
different business keys, adapt the SQL queries so they return the same
comparison columns and key names.
