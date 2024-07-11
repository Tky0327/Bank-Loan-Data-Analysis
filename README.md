# Data-Analyst-Project-Bank-Loan

### Project Overview

This data analysis project aims to gain insights into the set of bank loan data. By analyzing various aspects of data, we seek to identify trends, make data-driven recommendations, and gain a deeper understanding of the data set.


### Data Sources

Bank Loan Data: The primary data set used for this data is the 'financial_loan.csv' file. 


### Tools

Excel: Data cleaning
SQL: Data analysis
Power BI: Creating dashboard

### Exploratory Data Analysis (EDA)

1. 


### Data Cleaning

The data cleaning process involved several steps to ensure the dataset was accurate and ready for analysis:

1. Removing Duplicates: Identified and removed duplicate records to avoid skewing the analysis.

```excel
Remove Duplicates
```

2. Handling Missing Values: Checked for missing values and applied appropriate strategies such as imputation or removal of incomplete records.

``` excel
IF(ISBLANK(Cell), "Missing", Cell)
```

3. Correcting Data Types: Ensured that all columns had appropriate data types for accurate analysis (e.g., dates formatted correctly, numerical values).

``` excel
DATEVALUE(Cell)
```

4. Standardizing Text: Standardized text fields to maintain consistency, such as converting all text to lowercase or removing leading/trailing spaces.

``` excel
LOWER(TRIM(Cell))
```

5. Validating Data: Cross-verified data entries to ensure consistency and accuracy, such as checking for logical errors or outliers.

``` excel
IF(Cell < 0, "Error", Cell)
```


### SQL Queries

#### Total Loan Applications
```SQL
SELECT COUNT(id) AS Total_Applications FROM bank_loan_data
```

#### MTD Loan Applications
```SQL
SELECT COUNT(id) AS Total_Applications FROM bank_loan_data
WHERE MONTH(issue_date) = 12
```

#### PMTD Loan Applications
```SQL
SELECT COUNT(id) AS Total_Applications FROM bank_loan_data
WHERE MONTH(issue_date) = 11
```

#### Total Funded Amount
```SQL
SELECT SUM(loan_amount) AS Total_Funded_Amount FROM bank_loan_data
```

#### MTD Total Funded Amount
```sql
SELECT SUM(loan_amount) AS Total_Funded_Amount FROM bank_loan_data
WHERE MONTH(issue_date) = 12
```
#### PMTD Total Funded Amount
```sql
SELECT SUM(loan_amount) AS Total_Funded_Amount FROM bank_loan_data
WHERE MONTH(issue_date) = 11
```

#### Total Amount Received
```sql
SELECT SUM(total_payment) AS Total_Amount_Collected FROM bank_loan_data
```

#### MTD Total Amount Received
```sql
SELECT SUM(total_payment) AS Total_Amount_Collected FROM bank_loan_data
WHERE MONTH(issue_date) = 12
```

#### PMTD Total Amount Received
```sql
SELECT SUM(total_payment) AS Total_Amount_Collected FROM bank_loan_data
WHERE MONTH(issue_date) = 11
```

#### Average Interest Rate
```sql
SELECT AVG(int_rate)*100 AS Avg_Int_Rate FROM bank_loan_data
```

#### MTD Average Interest
```sql
SELECT AVG(int_rate)*100 AS MTD_Avg_Int_Rate FROM bank_loan_data
WHERE MONTH(issue_date) = 12
```

#### PMTD Average Interest
```sql
SELECT AVG(int_rate)*100 AS PMTD_Avg_Int_Rate FROM bank_loan_data
WHERE MONTH(issue_date) = 11
```

#### Avg DTI
```sql
SELECT AVG(dti)*100 AS Avg_DTI FROM bank_loan_data
```

#### MTD Avg DTI
```sql
SELECT AVG(dti)*100 AS MTD_Avg_DTI FROM bank_loan_data
WHERE MONTH(issue_date) = 12
```

#### PMTD Avg DTI
```sql
SELECT AVG(dti)*100 AS PMTD_Avg_DTI FROM bank_loan_data
WHERE MONTH(issue_date) = 11
```

#### Good Loan Percentage
```sql
SELECT
    (COUNT(CASE WHEN loan_status = 'Fully Paid' OR loan_status = 'Current' THEN id END) * 100.0) / 
	COUNT(id) AS Good_Loan_Percentage
FROM bank_loan_data
```

#### Good Loan Applications
```sql
SELECT COUNT(id) AS Good_Loan_Applications FROM bank_loan_data
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current'
```

#### Good Loan Funded Amount
```sql
SELECT SUM(loan_amount) AS Good_Loan_Funded_amount FROM bank_loan_data
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current'
```

#### Good Loan Amount Received
```sql
SELECT SUM(total_payment) AS Good_Loan_amount_received FROM bank_loan_data
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current'
```

#### Bad Loan Percentage
```sql
SELECT
    (COUNT(CASE WHEN loan_status = 'Charged Off' THEN id END) * 100.0) / 
	COUNT(id) AS Bad_Loan_Percentage
FROM bank_loan_data
```

#### Bad Loan Applications
```sql
SELECT COUNT(id) AS Bad_Loan_Applications FROM bank_loan_data
WHERE loan_status = 'Charged Off'
```

#### Bad Loan Funded Amount
```sql
SELECT SUM(loan_amount) AS Bad_Loan_Funded_amount FROM bank_loan_data
WHERE loan_status = 'Charged Off'
```

#### Bad Loan Amount Received
```sql
SELECT SUM(total_payment) AS Bad_Loan_amount_received FROM bank_loan_data
WHERE loan_status = 'Charged Off'
LOAN STATUS
	SELECT
        loan_status,
        COUNT(id) AS LoanCount,
        SUM(total_payment) AS Total_Amount_Received,
        SUM(loan_amount) AS Total_Funded_Amount,
        AVG(int_rate * 100) AS Interest_Rate,
        AVG(dti * 100) AS DTI
    FROM
        bank_loan_data
    GROUP BY
        loan_status
```
```sql
SELECT 
	loan_status, 
	SUM(total_payment) AS MTD_Total_Amount_Received, 
	SUM(loan_amount) AS MTD_Total_Funded_Amount 
FROM bank_loan_data
WHERE MONTH(issue_date) = 12 
GROUP BY loan_status
```

#### MONTH
```sql
SELECT 
	MONTH(issue_date) AS Month_Munber, 
	DATENAME(MONTH, issue_date) AS Month_name, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY MONTH(issue_date), DATENAME(MONTH, issue_date)
ORDER BY MONTH(issue_date)
```

#### STATE
```sql
SELECT 
	address_state AS State, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY address_state
ORDER BY address_state
```

#### TERM
```sql
SELECT 
	term AS Term, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY term
ORDER BY term
```

#### EMPLOYEE LENGTH
```sql
SELECT 
	emp_length AS Employee_Length, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY emp_length
ORDER BY emp_length
```

#### PURPOSE
```sql
SELECT 
	purpose AS PURPOSE, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY purpose
ORDER BY purpose
```

#### HOME OWNERSHIP
```sql
SELECT 
	home_ownership AS Home_Ownership, 
	COUNT(id) AS Total_Loan_Applications,
	SUM(loan_amount) AS Total_Funded_Amount,
	SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data
GROUP BY home_ownership
ORDER BY home_ownership
````














