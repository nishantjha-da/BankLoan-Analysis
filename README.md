---------------------------------------------------SQL_QUERY---------------------------------------------------------------

--Total Loan Application--

select count(*) as Total_Loan_Application from bank_loan_data

--MTD Loan Application--

select count(*) as MTD_Total_Loan_Application from bank_loan_data
where MONTH(issue_date)=12 and year(issue_date)=2021

--MOM Loan Application--

select count(*) as PMTD_Total_Loan_Application from bank_loan_data
where MONTH(issue_date)=11 and year(issue_date)=2021

--Total Funded Amount-- 

select sum(loan_amount) as Total_funded_amount from bank_loan_data

--MTD Total Funded Amount--

select sum(loan_amount) as MTD_Total_funded_amount from bank_loan_data
where MONTH(issue_date)=12 and year(issue_date)=2021

--PMTD Total Loan Application--

select sum(loan_amount) as PMTD_Total_funded_amount from bank_loan_data
where MONTH(issue_date)=11 and year(issue_date)=2021

--Total Received Amount--

select sum(total_payment) as Total_Amount_Received from bank_loan_data 

--MTD Total Received Amount--

select sum(total_payment) as MTD_Total_Amount_Received from bank_loan_data
where month(issue_date)=12 and year(issue_date) = 2021

--PMTD Total Received Amount--

select sum(total_payment) as PMTD_Total_Amount_Received from bank_loan_data
where month(issue_date)=11 and year(issue_date) = 2021

--Average Intrest Rate--

select round(AVG(int_rate)*100,2) as Average_Intrest_Rate from bank_loan_data

--MTD Average Intrest Rate--

select round(AVG(int_rate)*100,2) as MTD_Average_Intrest_Rate from bank_loan_data
where MONTH(issue_date)=12 and YEAR(issue_date)=2021

--PMTD Average Intrest Rate--

select round(AVG(int_rate)*100,2) as PMTD_Average_Intrest_Rate from bank_loan_data
where MONTH(issue_date)=11 and YEAR(issue_date)=2021

--Debt Income Ratio--

select round(AVG(dti)*100,2) as Avg_dti from bank_loan_data

--MTD Debt Income Ratio--

select round(AVG(dti)*100,2) as MTD_Avg_dti from bank_loan_data
where MONTH(issue_date)=12 and YEAR(issue_date)=2021

--PMTD Debt Income Ratio--

select round(AVG(dti)*100,2) as PMTD_Avg_dti from bank_loan_data
where MONTH(issue_date)=11 and YEAR(issue_date)=2021

--Total Number Of Good Loan Applications Percentage--

select 
(count(case when loan_status = 'Fully Paid' or loan_status ='Current' then id end)*100)
/
count(id) as Good_loan_Percentage
from bank_loan_data

--Good Loan Applicaton--

select count(id) as Good_Loan_Applicatons from bank_loan_data
where loan_status='Fully Paid' or Loan_status='Current'

--Good Loan Funded Amount--

select sum(loan_amount) as Good_Loan_Funded_Amount from bank_loan_data
where loan_status='Fully Paid' or Loan_status='Current'

--Good Loan Total Received Amount--

select sum(total_payment) as Good_Loan_Received_Amount from bank_loan_data
where loan_status='Fully Paid' or Loan_status='Current'

--Total Number Of Bad Loan Applications Percentage--

select 
(count(case when loan_status = 'Charged Off' then id end)*100)
/
count(id) as Bad_loan_Percentage
from bank_loan_data

--Bad Loan Applicaton--

select count(id) as Bad_Loan_Applicatons from bank_loan_data
where loan_status='Charged Off'

--Bad Loan Funded Amount--

select sum(loan_amount) as Bad_Loan_Funded_Amount from bank_loan_data
where loan_status='Charged Off'

--Bad Loan Total Received Amount--

select sum(total_payment) as Bad_Loan_Received_Amount from bank_loan_data
where loan_status='Charged Off'

--LOAN STATUS--

select
loan_status,
count(id) as Total_loan_application,
sum(total_payment) as Total_Amount_Received,
sum(loan_amount) as Total_Funded_Amount,
avg(int_rate *100) as Intrest_Rate,
avg(dti*100) as DTI
from 
bank_loan_data
group by 
loan_status

--MTD Amount Received Loan Status--

select 
loan_status,
sum(total_payment) as MTD_Total_Amount_Received,
sum(loan_amount) as MTD_Total_Funded_Amount
from bank_loan_data
where month(issue_date) = 12
group by loan_status

--Monthly Trends by Issue Date--

select
month(issue_date) as Month_Number,
DATENAME(month,issue_date) as Month_Name,
count(id) as Total_Loan_Applications,
sum(loan_amount) as Total_Funded_Amount,
sum(total_payment) as Total_Received_Amount
from bank_loan_data
group by  month(issue_date) ,DATENAME(month,issue_date)
order by month(issue_date)

--Regional Analysis by State--

select
address_state,
count(id) as Total_Loan_Applications,
sum(loan_amount) as Total_Funded_Amount,
sum(total_payment) as Total_Received_Amount
from bank_loan_data
group by  address_state
order by count(id) desc 

--Loan Term Analysis--

select
term,
count(id) as Total_Loan_Applications,
sum(loan_amount) as Total_Funded_Amount,
sum(total_payment) as Total_Received_Amount
from bank_loan_data
group by term
order by term

--Employee Length Analysis--

select
emp_length,
count(id) as Total_Loan_Applications,
sum(loan_amount) as Total_Funded_Amount,
sum(total_payment) as Total_Received_Amount
from bank_loan_data
group by emp_length
order by emp_length

--Loan Purpose Breakdown--

select
purpose,
count(id) as Total_Loan_Applications,
sum(loan_amount) as Total_Funded_Amount,
sum(total_payment) as Total_Received_Amount
from bank_loan_data
group by purpose
order by purpose 

--Home Ownership Analysis--

select
home_ownership,
count(id) as Total_Loan_Applications,
sum(loan_amount) as Total_Funded_Amount,
sum(total_payment) as Total_Received_Amount
from bank_loan_data
group by home_ownership
order by home_ownership

