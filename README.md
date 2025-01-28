# Unit-Economics-with-Python

📜 Introduction

Context

I have been hired for a new job as a Data Analyst.

The company is called "TechStream Solutions", and the product is a Software as a Service (SaaS) platform named "Streamline Pro". This platform provides comprehensive project management and collaboration tools for businesses of all sizes.

TechStream Solutions has been operating for several years and has gathered significant data on their costs and revenues. They are now looking to analyze their unit economics to understand the profitability of Streamline Pro on a per-customer basis.

**The datasets are in the shared folder on Google Drive:**

https://drive.google.com/drive/folders/1qhOW9Y2orRXuzbX-kXEmuJ7TMQiRs2Uv?usp=drive_link

My First Task: Calculating Unit Economics for Streamline Pro
Background: Streamline Pro is a comprehensive project management and collaboration tool designed to help businesses manage projects, track progress, and collaborate efficiently. Understanding the unit economics of Streamline Pro is crucial for evaluating its financial health and sustainability. This involves analysing key metrics such as Customer Acquisition Cost (CAC), Average Revenue Per User (ARPU), Cost of Goods Sold (COGS), Gross Margin, Customer Lifetime Value (LTV), and the LTV/CAC ratio.

Objective: My task is to calculate the unit economics for Streamline Pro for the month of **March 2023**. This will help us assess the profitability and efficiency of our customer acquisition strategies and operational expenses.

By performing these calculations, TechStream Solutions aims to:

Identify the profitability of acquiring and retaining customers.
Assess the efficiency of their marketing and sales strategies.
Make informed decisions on scaling their operations and optimizing their resource allocation.
This information will guide TechStream Solutions in refining their business strategies, ensuring sustainable growth, and maximizing profitability.

**What should we do?**

Today I need to calculate Unit Economics for "TechStream Solutions" including:

    CAC
    ARPU
    COGS
    Gross Margin
    LTV
    LTV / CAC
For doing this I'll use Python + Pandas + Google Colab.

The calculations should be made based on the data from the shared Google Drive folder (the link is in the block above).

https://colab.research.google.com/drive/17GU2XANBmjmv_40srrK8uQC6EA2VlEvm?usp=sharing

**How did I do it?**

I must first import the essential libraries for computation.

![image](https://github.com/user-attachments/assets/ac5cce44-87ba-42b0-a263-19204d285523)

**Step 1 : Load data**

To efficiently load data from multiple Google Sheet links without repeating code, I developed the following function:

![image](https://github.com/user-attachments/assets/445eb046-13ac-476b-a82a-3bbddc097b8a)

Then, We just need to input the variants:

![image](https://github.com/user-attachments/assets/7780ce03-4856-45cd-857e-b243ee749576)

View data :

df_daily.head()

|index|date|channel|spending|
|---|---|---|---|
|236|2023-03-01 |Google Ads|449|
|237|2023-03-01 |Facebook Ads|229|
|238|2023-03-01 |LinkedIn Ads|835|
|239|2023-03-01 |Twitter Ads|986|
|240|2023-03-02 |Google Ads|912|

df_customer.head()

|index||start\_date|churn\_date|
|---|---|---|---|
|0|1000|2021-11-15 |2022-09-14 |
|1|1001|2022-04-15 |2023-02-16 |
|2|1002|2022-10-30 |2023-02-04 |
|3|1003|2021-08-22 |2023-02-07 |
|4|1004|2021-08-23 |2022-02-02 |

df_receipt.head()

|index|date|customer\_id|receipt\_amount|new\_customer|
|---|---|---|---|---|
|618|2023-03-01 |1062|103|0|
|619|2023-03-01 |2243|157|0|
|620|2023-03-01 |1166|372|0|
|621|2023-03-01 |2406|426|1|
|622|2023-03-01 |2761|41|1|

df_payroll.head()

|index|month|department|employee\_name|position|paid|
|---|---|---|---|---|---|
|34|2023-03-01 |Sales|John Doe|Sales Manager|1500|
|35|2023-03-01 |Sales|Jane Smith|Sales Associate|600|
|36|2023-03-01 |Sales|Jim Brown|Sales Associate|700|
|37|2023-03-01 |Sales|Laura Miller|Sales Associate|800|
|38|2023-03-01 |Marketing|Alice Johnson|Marketing Manager|1650|

df_expenses.head()

|index|\#|month|category|item|amount|
|---|---|---|---|---|---|
|18|19|2023-03-01 |Server Costs|AWS Hosting|8400|
|19|20|2023-03-01 |Server Costs|Google Cloud Storage|4400|
|20|21|2023-03-01 |Software Licenses|Atlassian Jira|1400|
|21|22|2023-03-01 |Software Licenses|Slack|900|
|22|23|2023-03-01 |Software Licenses|Salesforce|1700|

**Step 2 : Calculate**

We have the following formulas:

**Customer Acquisition Cost (CAC):**

$$
CAC = \frac{TotalSalesandMarketingExpenses}{NumberofNewCustomersAcquired}
$$

**Average Revenue Per User (ARPU):**

$$
ARPU = \frac{TotalRevenue}{NumberofUsers}
$$

**Cost of Goods Sold (COGS) :**

$$
COGS = BeginningInventory + PurchasesDuringthePeriod - EndingInventory
$$

**⚠️ Pay attention!** As a software service company, TechStream Solutions only calculates the values generated during the period, having no beginning or ending inventory.

**Gross Margin :**

$$
GrossMargin = \frac{(Revenue - COGS)}{Revenue} \times 100
$$

**Customer Lifetime Value (LTV) :**

$$
LTV = ARPU \times CustomerLifespan \times GrossMargin
$$

**LTV/CAC**

$$
\frac{LTV}{CAC}
$$

*To calculate the above key metrics, I need to calculate the number below:*










