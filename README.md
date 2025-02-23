# Unit-Economics-with-Python

## 📜 Introduction


### Context

I have been hired for a new job as a Data Analyst.

The company is called "TechStream Solutions", and the product is a Software as a Service (SaaS) platform named "Streamline Pro". This platform provides comprehensive project management and collaboration tools for businesses of all sizes.

TechStream Solutions has been operating for several years and has gathered significant data on their costs and revenues. They are now looking to analyze their unit economics to understand the profitability of Streamline Pro on a per-customer basis.

**The datasets are in the shared folder on Google Drive:**

https://drive.google.com/drive/folders/1qhOW9Y2orRXuzbX-kXEmuJ7TMQiRs2Uv?usp=drive_link

My First Task: Calculating Unit Economics for Streamline Pro
Background: Streamline Pro is a comprehensive project management and collaboration tool designed to help businesses manage projects, track progress, and collaborate efficiently. Understanding the unit economics of Streamline Pro is crucial for evaluating its financial health and sustainability. This involves analysing key metrics such as Customer Acquisition Cost (CAC), Average Revenue Per User (ARPU), Cost of Goods Sold (COGS), Gross Margin, Customer Lifetime Value (LTV), and the LTV/CAC ratio.

## 🎯 Objective: 
My task is to calculate the unit economics for Streamline Pro for the month of **March 2023**. This will help us assess the profitability and efficiency of our customer acquisition strategies and operational expenses.

By performing these calculations, TechStream Solutions aims to:

Identify the profitability of acquiring and retaining customers.
Assess the efficiency of their marketing and sales strategies.
Make informed decisions on scaling their operations and optimizing their resource allocation.
This information will guide TechStream Solutions in refining their business strategies, ensuring sustainable growth, and maximizing profitability.

### What should we do?

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

### How did I do it?

I must first import the essential libraries for computation.

```
import pandas as pd
import numpy as np
```
**Step 1 : Load data**

To efficiently load data from multiple Google Sheet links without repeating code, I developed the following function:

```
def read_file_ggsheet(file_id, month_col=None):
    df_ggsheet = pd.read_excel('https://docs.google.com/spreadsheets/d/' + file_id + '/export?format=xlsx')
    
    if month_col is not None:
        df_202303 = df_ggsheet[
            (df_ggsheet[month_col].dt.month == 3) & (df_ggsheet[month_col].dt.year == 2023)
        ]
        return df_202303
    else:
        return df_ggsheet
```

Then, We just need to input the variants:

```
df_daily = read_file_ggsheet(file_id='1AZOIThOV4P-0eYDge53ZwumVkfkHoYPWxst3k3Bv87c',month_col="date")
df_customer = read_file_ggsheet(file_id='1by8tPHwOnq3uKYK2E7sA9VBUYoPM4p1Rnrm_Ss9cyHI')
df_receipt = read_file_ggsheet(file_id='1qayqML1zCKdmtzutkcy9LWvE6xFRm6TGBEVkHHJKIuE',month_col="date")
df_payroll = read_file_ggsheet(file_id='1c_WihqTZCQvNgxzmd-OwhR9i5diwtfxXVLyMn8R-Lp4',month_col="month")
df_expenses = read_file_ggsheet(file_id='10OGbaywwMIqKgnPGy8VDvpBVtjyqln47iYa2lFhI9Mw',month_col="month")
```

Check data :

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

*To calculate the above key metric, I need to calculate the number below:*

| **Line** | **Code**                                                                                           |
|---------|----------------------------------------------------------------------------------------------------|
| 1       | `online_spending = df_daily['spending'].sum()`                                                    |
| 2       | `sales_and_makerting_cost = df_payroll[df_payroll['department'].isin(["Sales", "Marketing"])]['paid'].sum()` |
| 3       | `mkt_software_cost = df_expenses[df_expenses['item'] == "Salesforce"]['amount'].sum()`             |
| 4       | `total_sales_mkt_cost = online_spending + sales_and_makerting_cost + mkt_software_cost`            |
| 5       | `total_new_customers = df_receipt['new_customer'].sum()`                                           |

```
CAC = total_sales_mkt_cost / total_new_customers
CAC = 1213.968253968254
```

**Average Revenue Per User (ARPU):**

$$
ARPU = \frac{TotalRevenue}{NumberofUsers}
$$

*To calculate the above key metric, I need to calculate the number below:*

| **Line** | **Code**                                                                                           |
|---------|----------------------------------------------------------------------------------------------------|
| 1       | `total_revenue = df_receipt['receipt_amount'].sum()`                                               |
| 2       | `number_cus=len(df_receipt['customer_id'].unique())`                                               |

```
ARPU = total_revenue / number_cus
ARPU = 284.3595890410959
```

**Cost of Goods Sold (COGS) :**

$$
COGS = BeginningInventory + PurchasesDuringthePeriod - EndingInventory
$$

**⚠️ Pay attention!** As a software service company, TechStream Solutions only calculates the values generated during the period, having no beginning or ending inventory.

*To calculate the above key metric, I need to calculate the number below:*

| **Line** | **Code**                                                                                           |
|---------|----------------------------------------------------------------------------------------------------|
| 1       | `server_and_software_licences_cost = df_expenses[df_expenses['item'].isin (["AWS Hosting","Google Cloud Storage","Atlassian Jira"])]['amount'].sum()` |
| 2       | `salary_of_direct_employees = df_payroll[df_payroll['department'] == "Engineering"]['paid'].sum()`                                               |

```
COGS = server_and_software_licences_cost + salary_of_direct_employees
COGS = 19400
```

**Gross Margin :**

$$
GrossMargin = \frac{(Revenue - COGS)}{Revenue} \times 100
$$

*I calculated the number below:*

```
Gross_Margin = ((total_revenue - COGS) / total_revenue)*100
Gross_Margin = 76.63579540664554
```
                                            |
**Customer Lifetime Value (LTV) :**

$$
LTV = ARPU \times CustomerLifespan \times GrossMargin
$$

*To calculate the above key metric, I need to calculate the number below:*
```
avg_lifespan_months = ((df_customer['churn_date']-df_customer['start_date']).dt.days / 30).mean()
```

```
LTV = ARPU*avg_lifespan_months*Gross_Margin
LTV = 214463.5493150685
```

**LTV/CAC**

$$
\frac{LTV}{CAC}
$$

*I calculated the number below:*

```
LTV_devided_by_CAC = LTV/CAC
LTV_devided_by_CAC = 176.66322707700465
```

## Conclusion & Recommendations ✍

### 🔹 Conclusion:

The business enjoys a high profit margin and a reasonable customer acquisition cost (CAC) relative to customer lifetime value (LTV). The high LTV/CAC ratio indicates a strong capacity for quick capital recovery and sustainable growth.

### 🔹 Recommendations:

✅ Maintain customer attraction effectiveness
CAC remains low compared to customer value, allowing for continued expansion of marketing campaigns.

✅ Optimize CAC by increasing conversion rates
Improving the conversion efficiency of potential customers will lower CAC and boost profits.

✅ Implement a customer retention program
Given the high LTV, focus on retaining customers through excellent service, upselling, and loyalty programs.

✅ Reduce CAC dependence by increasing ARPU
Raising product/service prices or expanding service packages can enhance ARPU and further optimize profits.

💡 In summary: All current indicators are positive, indicating strong expansion potential. Further optimization of CAC and a focus on customer retention are essential for sustainable growth. 🚀

**✅ 🙂 👉 Note : You can see details my work at the link below.**

🔗 : https://colab.research.google.com/drive/17GU2XANBmjmv_40srrK8uQC6EA2VlEvm?usp=sharing
 








