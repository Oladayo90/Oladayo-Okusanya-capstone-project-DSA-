# Oladayo-Okusanya-capstone-project-DSA-

# Kultra Mega Stores Inventory

#### Kultra Mega Stores (KMS), headquartered in Lagos, 

#### specialises in office supplies and furniture. Its customer base includes individual consumers, small businesses (retail), and large corporate clients (wholesale) across Lagos, Nigeria.
---
#### I have been engaged as a Business Intelligence Analyst to support the Abuja division of KMS. The Business Manager has shared an Excel file containing order data from 2009 to 2012 and has requested that I analyze the data and present my key insights and findings. 
I am to apply my SQL skills from the DSA Data Analysis class and solve both case scenarios as shared in the document.
The following queries were used to cleanup the imported Excel data
``` SQL
alter table [KMS Sql Case Study] alter column profit decimal(18,2) 
alter table [KMS Sql Case Study] alter column unit_price decimal(18,2)
alter table [KMS Sql Case Study] alter column Discount decimal(18,2)
alter table [KMS Sql Case Study] alter column sales decimal(18,2)
alter table [KMS Sql Case Study] alter column Product_Base_Margin decimal(18,2)
alter table [KMS Sql Case Study] alter column Shipping_Cost decimal(18,2)

update [KMS Sql Case Study] set profit = 0 where profit is null
update [KMS Sql Case Study] set unit_price = 0  where unit_price is null
update [KMS Sql Case Study] set Product_Base_Margin = 0  where Product_Base_Margin is null

```
### Case Scenario I
**Q.1.** Which product category had the highest sales?  
**Ans:** _Technology_
```SQL
select top(1) sum(sales)'Total_sales', product_category from [KMS Sql Case Study] group by product_category order by sum(sales) desc
```
**Q.2.** What are the Top 3 and Bottom 3 regions in terms of sales?  
**Ans:**  
_TOP 3:_  
 - West (3,597,549.33)  
 - Ontario (3,063,212.55)  
 - Prarie (2837,304.59)

``` SQL
select top 3 sum(sales)'Total_sales', Region from [KMS Sql Case Study] group by Region order by sum(sales) desc
```
  _Bottom 3:_  
  - Nunavut (116,376.47)  
  - Northwest Territories (800,847.34)  
  - Yukon (975,867.39)      
``` SQL
select top 3 sum(sales)'Total_sales', Region from [KMS Sql Case Study] group by Region order by sum(sales)
```
**Q.3.** What were the total sales of appliances in Ontario?  
**Ans:** _736,991.54_  
``` SQL
select SUM(sales)'Total_sales', Product_Sub_Category from [KMS Sql Case Study] where Product_Sub_Category = 'Appliances'
group by Product_Sub_Category
```
**Q.4.** Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers  
**Ans:**
```SQL
select top(10) SUM(profit) profit, customer_Name into #Bottom from [KMS Sql Case Study] 
group by customer_Name
order by SUM(profit)

select * from [KMS Sql Case Study] where customer_Name in (select customer_Name from #Bottom)

select * from #Bottom
```
**Q.5.** KMS incurred the most shipping cost using which shipping method?  
**Ans:** _Delivery Truck_  
```SQL
select ship_Mode from [KMS Sql Case Study] where shipping_Cost = (select max(shipping_Cost) from [KMS Sql Case Study])
```
### Case Scenario II
**Q.6.** Who are the most valuable customers, and what products or services do they typically purchase?  
```SQL
select SUM(profit)Profit,Customer_Segment into #MVC 
from [KMS Sql Case Study] where order_id not in (select order_id from order_status)
group by Customer_Segment
order by SUM(profit) desc
```
**Ans:** _most valuable customers: Corporate_  
```SQL
select Top(1) Customer_Segment from #MVC
```
**Ans:** _products or services they typically purchase_  
```SQL
select distinct Product_Sub_Category from [KMS Sql Case Study] 
where Customer_Segment in (select Top(1) Customer_Segment from #MVC)
```
**Q.7.** Which small business customer had the highest sales?  
**Ans:** _Dennis Kane with 75,967.59_  
```SQL
select top(1) sum(sales) 'Total_Sales', Customer_Name from [KMS Sql Case Study]
where ltrim(rtrim((Customer_Segment))) = 'Small Business'
group by Customer_Name
order by sum(sales) desc
```
**Q.8.** Which Corporate Customer placed the most number of orders in 2009 – 2012?  
**Ans:** _Roy Skaria with 773_  
```SQL
select top(1) sum(Order_Quantity)Total_Order_Quantity,Customer_Name from [KMS Sql Case Study]
where Customer_Segment = 'Corporate' 
and year(order_date) between '2009' and '2012'
group by Customer_Name
order by sum(Order_Quantity) desc
```
**Q.9.** Which consumer customer was the most profitable one?  
**Ans:** _Emily Phan with 34,005.44_  
```SQL
select Top(1) SUM(profit)Total_Profit, Customer_Name from [KMS Sql Case Study]
where Customer_Segment = 'Consumer'
group by Customer_Name
order by SUM(profit) desc
```
**Q.10.** Which customer returned items, and what segment do they belong to?  
```SQL
select distinct a.Customer_Name,a.Customer_Segment from [KMS Sql Case Study] a 
join Order_Status b on a.Order_ID =b.Order_ID
```

# About the author
# OLADAYO OKUSANYA OLUWASEUN  
📞 09083268004 | 09053042440  
📧 okudayoo@gmail.com  
🌐 GitHub: github.com/Oladayo90  
🏠 4, Araromi Street, Oto Awori, Lagos, Nigeria  

---

## ✨ Professional Summary  
Dedicated business educator with over a decade of experience in teaching, mentoring, and academic planning. Specializing in financial literacy, data analysis, and personal development for students. Passionate about shaping learners to excel both academically and professionally using modern tools and inclusive teaching methods.

---

## 🧠 Core Teaching Competencies  
- **Subject Expertise**: Financial Accounting, Economics, Business Studies  
- **Instructional Design**: Curriculum development and delivery  
- **Learner Engagement**: Student mentorship and coaching  
- **Assessment & Evaluation**: Academic progress tracking  
- **Tech Integration**: Excel, Power BI, and SQL in classroom settings  
- **Leadership & Pastoral Care**: Classroom management and behavioral support  

---

## 👩‍🏫 Professional Experience  

**Jacobian Comprehensive College** — *Bookkeeping & JSS Teacher*  
*Sept 2021 – Present*  
- Delivered bookkeeping instruction using practical examples  
- Guided junior students across multiple subjects with structured lesson plans  
- Acted as student advisor, enhancing academic performance through mentorship  

**Adeniyi Goodwill Private Schools** — *Economics & Financial Accounting Teacher*  
*Jun 2013 – Dec 2019*  
- Developed engaging lesson content aligned with WAEC curriculum  
- Mentored students in business topics, resulting in academic excellence  
- Created classroom environments focused on discipline and collaboration  

**Ladies in Tech Africa** — *Data Analyst Intern*  
*Aug 2024 – Nov 2024*  
- Applied Excel and Power BI in educational data cleaning projects  
- Supported learning dashboards to track student trends and engagement  
- Communicated data insights to non-technical stakeholders  

**PRO Freelancer (Video Editing & EdTech)** — *Visual Educator & Editor*  
*Jun 2024 – Feb 2025*  
- Created instructional videos and e-learning content  
- Used visual storytelling to enhance student understanding of abstract concepts  

---

## 🎓 Education & Certifications

- **B.Ed. Business Education** — National Open University of Nigeria *(2024 – Present)*  
- **Diploma, Data Analytics & Science** — The IncubatorHub *(2024)*  
- **NCE Business Education** — Adeniran Ogunsanya College of Education *(2016 – 2020)*  
- **Institute of Chartered Accountants of Nigeria (ICAN)** — AAT Certification *(Awaiting)*  

---

## 📊 Projects & Innovations  

**Power BI Dashboards for Classroom Insights**  
- Built student progress trackers and financial education models  
- Leveraged data visualization to promote performance improvement

**Excel-Based Business Learning Modules**  
- Designed spreadsheets for classroom exercises in finance and budgeting  
- Integrated PMT, IRR, and VLOOKUP functions into practical activities  

---

## 👥 Interests & Impact  
- Mentorship and youth empowerment programs  
- Sport-based character education (Boxing Enthusiast 🥊)  
- Advocating lifelong learning and growth mindset  

---

## 🏆 Summary of Strengths  
- 10+ years in educational instruction  
- Culturally aware and emotionally intelligent educator  
- Strong foundation in finance, tech, and classroom leadership
