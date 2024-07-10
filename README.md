## Auto or Personal! Which Loan is the Game Changer?

Problem Statement:
 
You are a data analyst at HDFC Bank. The bank wants to analyze the interest rates on personal loans and auto loans to identify trends, optimize rates for competitive advantage, and improve customer satisfaction. The bank is particularly interested in understanding which loan type personal loans or auto loans is more critical for their business. Your tasks are.....................

1.Identify the average interest rate for personal loans and auto loans over the past year

2.Calculate the monthly trend of interest rates for both personal loans and auto loans.
 
3.Analyze loan volumes to determine which loan type is more critical.

4.Create a Power BI report to visualize the interest rate trends, compare them with competitor rates, and highlight the importance of each loan type.



SOLUTION:

1. Identify the average interest rate for personal loans and auto loans over the past year.

SELECT LoanProductID, AVG(InterestRate) AS AvgInterestRate

FROM InterestRates

WHERE RateDate <= DATE_SUB( '2024-12-30',INTERVAL 1 YEAR)

AND LoanProductID IN (2, 3) -- Assuming 2 is Auto Loan and 3 is Personal Loan

GROUP BY LoanProductID;

2. Calculate the monthly trend of interest rates for both personal loans and auto loans

select LoanProductID,

   YEAR(RateDate) as year,
       
   MONTH(RateDate) as month,
       
   AVG(InterestRate) as average_monthly_rate
       
from InterestRates

where RateDate <= date_sub('2024-12-30',INTERVAL 1 YEAR) 

group by LoanProductID,

   YEAR(RateDate),
       
   MONTH(RateDate)
       
order by LoanProductID,year,month;

3. Analyze loan volumes to determine which loan type is more critical

select LoanProductID,count(LoanProductID) as count,sum(LoanAmount) as total_sum

from loans

group by LoanProductID

4. Create a Power BI report to visualize the interest rate trends, compare them with competitor rates, and highlight the importance of each loan type.

   
![Screenshot 2024-07-10 174454](https://github.com/ErnestaRoschelle/Analyzing-Bank-Loan-Using-SQL-and-Power-BI/assets/145251891/2878c64a-41c9-473c-9d98-7d65a530b4a6)
