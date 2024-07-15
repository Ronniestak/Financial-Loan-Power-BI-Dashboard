# SQL QUERIES USED TO DETERMINE THE KPI's AND VARIOUD OTHER MATRICES:- 


# BANK LOAN REPORT QUERY DOCUMENT

# A.	BANK LOAN REPORT | SUMMARY

## KPI’s:

Total Loan Applications
SELECT COUNT(id) AS Total_Loan_Applications
FROM bank_loan_data;
 
MTD Loan Applications
SELECT COUNT(id) AS MTD_Total_Loan_Applications
FROM bank_loan_data
WHERE MONTH(issue_date) = 12 AND YEAR(issue_date) = 2021;

PMTD Loan Applications
SELECT COUNT(id) AS PMTD_Total_Loan_Applications
FROM bank_loan_data
WHERE MONTH(issue_date) = 11 AND YEAR(issue_date) = 2021;

Total Fundcd Amount
SELECT SUM(loan_amount) AS Total_Funded_Amount
FROM bank_loan_data;
 
MTD Fundcd Amount
SELECT SUM(loan_amount) AS MTD_Total_Funded_Amount
FROM bank_loan_data
WHERE MONTH(issue_date) = 12 AND YEAR(issue_date) = 2021;

PMTD Fundcd Amount
SELECT SUM(loan_amount) AS PMTD_Total_Funded_Amount
FROM bank_loan_data
WHERE MONTH(issue_date) = 11 AND YEAR(issue_date) = 2021;

Total Amount Received
SELECT SUM(total_payment) AS Total_Amount_Received
FROM bank_loan_data;
 

MTD Amount Received
SELECT SUM(total_payment) AS MTD_Total_Amount_Received
FROM bank_loan_data
WHERE MONTH(issue_date) = 12 AND YEAR(issue_date) = 2021;

PMTD Amount Received
SELECT SUM(total_payment) AS PMTD_Total_Amount_Received
FROM bank_loan_data
WHERE MONTH(issue_date) = 11 AND YEAR(issue_date) = 2021;

Average Interest Rate
SELECT round(AVG(int_rate), 4) AS Average_Interest_Rate
FROM bank_loan_data;
 
MTD Average Interest Rate
SELECT round(AVG(int_rate), 4) AS MTD_Average_Interest_Rate
FROM bank_loan_data;
WHERE MONTH(issue_date) = 12 AND YEAR(issue_date) = 2021;

PMTD Average Interest Rate
SELECT round(AVG(int_rate), 4) AS PMTD_Average_Interest_Rate
FROM bank_loan_data;
WHERE MONTH(issue_date) = 11 AND YEAR(issue_date) = 2021;

Average DTI
SELECT ROUND(AVG(dti), 4) * 100 AS Average_DTI
FROM bank_loan_data;.
 
MTD Average DTI
SELECT ROUND(AVG(dti), 4) * 100 AS MTD_Average_DTI
FROM bank_loan_data 
WHERE MONTH(issue_date) = 12 AND YEAR(issue_date) = 2021;

PMTD Average DTI
SELECT ROUND(AVG(dti), 4) * 100 AS PMTD_Average_DTI
FROM bank_loan_data 
WHERE MONTH(issue_date) = 11 AND YEAR(issue_date) = 2021;

Good Loan Percentage
SELECT ROUND((COUNT(CASE WHEN loan_status = 'Fully Paid' OR loan_status = 'Current' THEN id END) * 100 
/ COUNT(id)), 2) AS Good_Loan_Percentage
FROM bank_loan_data;
 
Good Loan Applications
SELECT COUNT(id) AS Good_Loan_Application
FROM bank_loan_data
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current';
 
Good Loan Funded Amount
SELECT sum(loan_amount) AS Good_Loan_Funded_Amount
FROM bank_loan_data
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current';
 
Good Loan Total Received Amount
SELECT sum(total_payment) AS Good_Loan_Total_Received_Amount
FROM bank_loan_data
WHERE loan_status = 'Fully Paid' OR loan_status = 'Current';
 
Bad Loan Percentage
SELECT ROUND((COUNT(CASE WHEN loan_status = 'Charged Off' THEN id END) * 100 
/ COUNT(id)), 2) AS Badd_Loan_Percentage
FROM bank_loan_data;

Bad Loan Applications
SELECT COUNT(id) AS Bad_Loan_Application
FROM bank_loan_data
WHERE loan_status = 'Charged Off';
 
Bad Loan Funded Amount
SELECT sum(loan_amount) AS Bad_Loan_Funded_Amount
FROM bank_loan_data
WHERE loan_status = 'Charged Off';
 
Bad Loan Total Received Amount
SELECT sum(total_payment) AS Bad_Loan_Total_Received_Amount
FROM bank_loan_data
WHERE loan_status = 'Charged Off';
 

Loan Grid View
SELECT 
    loan_status,
    COUNT(id) AS Total_Loan_Applications,
    SUM(loan_amount) AS Total_Funded_Amount,
    SUM(total_payment) AS Total_Received_Amount,
    AVG(int_rate * 100) AS Average_Interest_Rate,
    AVG(dti * 100) AS Average_DTI
FROM bank_loan_data
GROUP BY loan_status;
 

SELECT 
    loan_status,
    SUM(loan_amount) AS MTD_Total_Funded_Amount,
    SUM(total_payment) AS MTD_Total_Amount_Received
FROM
    bank_loan_data
WHERE
    MONTH(issue_date) = 12
        AND YEAR(issue_date) = 2021
GROUP BY loan_status;


# B.	BANK LOAN REPORT | OVERVIEW

Monthly Trends by Issue Date 
SELECT 
    DATE_FORMAT('issue_date', '%M'),
    COUNT(id) AS Total_Loan_Applications,
    SUM(loan_amount) AS Total_Funded_Amount,
    SUM(total_payment) AS Total_Received_Amount
FROM
    bank_loan_data
GROUP BY DATE_FORMAT('issue_date', '%M')
ORDER BY DATE_FORMAT('issue_date', '%M');

Regional Analysis by State 
SELECT 
    address_state,
    COUNT(id) AS Total_Loan_Applications,
    SUM(loan_amount) AS Total_Funded_Amount,
    SUM(total_payment) AS Total_Received_Amount
FROM
    bank_loan_data
GROUP BY address_state
ORDER BY address_state;
 

Loan Term Analysis 
SELECT 
    term,
    COUNT(id) AS Total_Loan_Applications,
    SUM(loan_amount) AS Total_Funded_Amount,
    SUM(total_payment) AS Total_Received_Amount
FROM
    bank_loan_data
GROUP BY term
ORDER BY term;
 

Employee Length Analysis 
SELECT 
    emp_length,
    COUNT(id) AS Total_Loan_Applications,
    SUM(loan_amount) AS Total_Funded_Amount,
    SUM(total_payment) AS Total_Received_Amount
FROM
    bank_loan_data
GROUP BY emp_length
ORDER BY emp_length;
 
Loan Purpose Breakdown
SELECT 
    purpose,
    COUNT(id) AS Total_Loan_Applications,
    SUM(loan_amount) AS Total_Funded_Amount,
    SUM(total_payment) AS Total_Received_Amount
FROM
    bank_loan_data
GROUP BY purpose
ORDER BY Total_Loan_Applications desc;
 
Home Ownership Analysis 
SELECT 
    home_ownership,
    COUNT(id) AS Total_Loan_Applications,
    SUM(loan_amount) AS Total_Funded_Amount,
    SUM(total_payment) AS Total_Received_Amount
FROM
    bank_loan_data
GROUP BY home_ownership
ORDER BY Total_Loan_Applications desc;
 

FOR STATE = CA AND GRADE = A
SELECT 
    home_ownership,
    COUNT(id) AS Total_Loan_Applications,
    SUM(loan_amount) AS Total_Funded_Amount,
    SUM(total_payment) AS Total_Received_Amount
FROM
    bank_loan_data
WHERE
    grade = 'A' AND address_state = 'CA'
GROUP BY home_ownership
ORDER BY Total_Loan_Applications DESC;
 




















