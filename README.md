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

**Step 2 : Calculate**

We have the following formulas:

**Customer Acquisition Cost (CAC):**

![image](https://github.com/user-attachments/assets/bce016be-4dfb-4448-bc5d-03d9f6dc75b5)

**Average Revenue Per User (ARPU):**

![image](https://github.com/user-attachments/assets/cbcb2a20-673a-4622-b051-6190fa1e02b5)

**Cost of Goods Sold (COGS) :**

![image](https://github.com/user-attachments/assets/202f4d98-d25f-4e1a-a8a8-be093ae1d49e)

**⚠️ Pay attention!** As a software service company, TechStream Solutions only calculates the values generated during the period, having no beginning or ending inventory.

**Gross Margin :**

![image](https://github.com/user-attachments/assets/98c60433-fad0-4c88-a144-fbd0fb711cd1)

**Customer Lifetime Value (LTV) :**

![image](https://github.com/user-attachments/assets/4092434d-0c73-4cc1-b305-f23721d94144)

**LTV/CAC**

LTV/CAC

*To calculate the above key metrics, I need to calculate the number below:*








