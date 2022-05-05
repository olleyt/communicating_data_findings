# Prosper Loan Data Exploration

## Dataset


The data consists of information regarding 113,937 loans with 81 variables on each loan, including loan amount, borrower rate (or interest rate), current loan status, borrower income, loan rating, own Prosper Score and Prosper Rating and many others. 


However, the data set will be wrangled and cleaned for this project to select only loans where Prosper Score and other variables of interest are available.
It was my choice not to compute missing values but rather filter out records with missing values for ProsperScore, BankcardUtilization, DebtToIncomeRatio, , and DelinquenciesLast7Years columns. Leaving missing values was not a good option either as it could skew the analysis.

There is significant amount of loans originated before July 2009 that does not have Prosper Score and Prosper Rating. This is the reason of reduction the initial dataset as the analysis below will investigate reliance of Prosper Score and Prosper Rating on the loan outcome.

In addition, the canceled loan after all data tidying was removed because it was the only 1 loan in this status and it caused facet grid plotting issues.
The data wrangling will result in 77557 loans in the final data set for exploration.

The data wrangling efforts summary is provided below.

### Data Wrangling Summary
Data wrangling was performed on the original data set and included the following steps:
1. filling in missing values for the following variables as in the dictionary: {'Occupation':'Other', 
           'EmploymentStatus':'Not available',
           'BorrowerState':'Not Available'}
2. loan category was remapped to human readable strings as specified in the Prosper loan feature spreadsheet mentioned above.
3. loan status was simplified for alls statuses with past due payments: any of those were mapped to 'Past Due' value
4. new categorical variable 'TermYears' was created to categorize loan term in years (for simplicity)
5. new variable 'log_loan_amt' was created for plotting purposes for heat maps and facet grids on a log scale for loan amount
6. dataset was filtered where these variables were empty in order not to skew the analysis : DebtToIncomeRatio, DelinquenciesLast7Years, BankcardUtilization, BorrowerRate, ProsperScore
7. dataset dimensions were reduced to these columns: {'log_loan_amt', 'TermYears',
'LoanStatusSimplified','BorrowerRate',
'ProsperRating (numeric)', 'ProsperScore', 'ProsperRating (Alpha)',
'LoanCategory','BorrowerState','Occupation',
'EmploymentStatus','IsBorrowerHomeowner', 
'IncomeVerifiable','StatedMonthlyIncome', 'LoanOriginalAmount',
'DelinquenciesLast7Years', 'BankcardUtilization',
'DebtToIncomeRatio', 'IncomeRange'}
8. These column types were converted to categorical: {'TermYears', 'LoanStatusSimplified', 'ProsperRating (Alpha)', 'BorrowerState', 'Occupation','EmploymentStatus', 'IncomeRange'}
9. as it was only 1 cancelled loan in the dataset after previous filtering, this cancelled loan was also filtered out as it was causing errors for plotting heatmaps and facet grids. On the greater scale of things, it shall not impact the analysis and conclusions.

## Summary of Findings
In the exploration, I found that there was a strong relationship between Prosper Score and Prosper ratings with the loan outcome (loan status).
I also found that loan amount and borrower rate may contribute to the loan outcome and can strenghen the relationship of loan outcome with the Prosper score and Prosper ratings.
In addition, it was noted that debt-to-income ratio, delinquences for past 7 years are also strenghening relationship of loan outcome with Prosper Score and Prosper Rating.
Moreover, the exploration confirmed that loan category and employment staus can also play a role how differen loans perform.

Outside of main variables of interest, I verified that:
1. majority of Prosper borrowers had their income verifiable
2. some states seems to outperform others
3. Prosper rating is correlated with bank card utilization and therefore can indirectly influence loan outcome via Prosper Rating, as Prosper Rating and Prosper Score have more clear relationship with loan outcome

## Key Insights for Presentation

For the presentation, I focus on the influence of Prosper Score, Prosper Rating(both alpha and number) and the following loan features of interest:
* numerical variables:
    * stated monthly income
    * borrower rate
    * loan originating amount
    * debt-to-income ratio
* categorical variables:
    * loan category
    * employment status
    
I will also have a look at consistency among rating and scoring variables:
* `ProsperScore`
* `ProsperRating (Alpha)`
* `ProsperRating (numeric)`

Most of the intermediate derivations will be also included where appropriate such as:
* relationship between bank card utilization with loan outcome and Prosper Rating
* relationship between delinquences for past 7 years with loan outcome and Prosper Rating

I start by introducing the loan status variable, Prosper Score, and Prosper Rating and their distribution, followed by the distribution plots for other variables. Most of the distribution plots will use histograms or kde plots for numerical variables and box plots or violin plots for categorical variables.

Then I will explore bi-variate relationships between loan status, Prosper Score, and Prosper Rating and other variables that may influence loan outcome (i.e. loan status).

Afterwards I will move to multi-variate exploration to illuminate loan features relationships influencing loan outcome.

I've made sure to use appropriate color palettes for loan status variable to make sure it
is clear that they're different on the plots.

