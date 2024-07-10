## Auto or Personal! Which Loan is the Game Changer?

Problem Statement:
 
You are a data analyst at HDFC Bank. The bank wants to analyze the interest rates on personal loans and auto loans to identify trends, optimize rates for competitive advantage, and improve customer satisfaction. The bank is particularly interested in understanding which loan type personal loans or auto loans is more critical for their business. Your tasks are.....................

1.Identify the average interest rate for personal loans and auto loans over the past year

2.Calculate the monthly trend of interest rates for both personal loans and auto loans.
 
3.Analyze loan volumes to determine which loan type is more critical.

4.Create a Power BI report to visualize the interest rate trends, compare them with competitor rates, and highlight the importance of each loan type.

Dataset

CompetitorInterestRates Table:
CREATE TABLE CompetitorInterestRates (
 CompetitorRateID INT,
 CompetitorID INT,
 LoanProductID INT,
 InterestRate DECIMAL(5, 2),
  RateDate DATE);
 
INSERT INTO CompetitorInterestRates (CompetitorRateID, CompetitorID, LoanProductID, InterestRate, RateDate) VALUES
(1, 1, 2, 4.95, '2023-01-05'),
(2, 1, 3, 11.40, '2023-01-10'),
(3, 2, 2, 4.70, '2023-02-15'),
(4, 2, 3, 10.85, '2023-03-20'),
(5, 3, 2, 4.35, '2023-04-25'),
(6, 3, 3, 11.78, '2023-05-30'),
(7, 1, 3, 10.82, '2023-06-05'),
(8, 2, 2, 4.45, '2023-07-10'),
(9, 3, 3, 10.88, '2023-08-15'),
(10, 1, 2, 4.83, '2023-09-20');

INSERT INTO InterestRates (RateID, LoanProductID, InterestRate, RateDate) VALUES
(1, 2, 5.00, '2023-01-05'), -- Auto Loan
(2, 3, 11.50, '2023-01-10'), -- Personal Loan
(3, 2, 4.75, '2023-02-15'),
(4, 3, 10.90, '2023-03-20'),
(5, 2, 4.30, '2023-04-25'),
(6, 3, 11.80, '2023-05-30'),
(7, 2, 4.85, '2023-06-05'),
(8, 3, 10.40, '2023-07-10'),
(9, 2, 4.95, '2023-08-15'),
(10, 3, 11.00, '2023-09-20');
 
 LoanProducts  Table:
CREATE TABLE LoanProducts (
 LoanProductID INT,
 ProductName VARCHAR(255)
);
 
INSERT INTO LoanProducts (LoanProductID, ProductName) VALUES
(2, 'Auto Loan'),
(3, 'Personal Loan');
 
 Loans  Table:
CREATE TABLE Loans (
 LoanID INT,
 LoanProductID INT,
 LoanAmount DECIMAL(10, 2),
 LoanDate DATE
);
 
INSERT INTO Loans (LoanID, LoanProductID, LoanAmount, LoanDate) VALUES
(1, 2, 500000.00, '2023-01-05'),
(2, 3, 200000.00, '2023-01-10'),
(3, 2, 600000.00, '2023-02-15'),
(4, 3, 250000.00, '2023-03-20'),
(5, 2, 450000.00, '2023-04-25'),
(6, 3, 300000.00, '2023-05-30'),
(7, 2, 500000.00, '2023-06-05'),
(8, 3, 150000.00, '2023-07-10'),
(9, 2, 550000.00, '2023-08-15'),
(10, 3, 180000.00, '2023-09-20');

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
