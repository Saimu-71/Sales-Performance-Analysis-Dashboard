# 📊 Sales Performance Analysis Dashboard  

This project features a **Power BI dashboard** that analyzes the sales performance of a retail company. It offers actionable insights through dynamic visualizations, helping businesses track growth in sales and profit across various dimensions, including product, category, subcategory, country, region, sales representative, and date intervals.

---

## 🛠️ **Project Purpose**  
The purpose of this dashboard is to provide a one-page visual representation of sales insights to:  
- Monitor sales trends and performance metrics.  
- Identify profitable products, categories, and regions.  
- Enable data-driven decisions for improving sales strategies.  

---

## 📋 **Key Features**  

### 🔹 **Data Sources**  
- **Sales Data**: Folder containing yearly sales files (CSV format).  
- **Categories**: Excel file.  
- **Geography**: Excel file.  
- **Products**: Database/CSV.  
- **Sales Representatives**: Excel file.  
- **Subcategories**: Excel file.  

### 🔹 **Data Loading and Transformation**  
- A **resilient mechanism** to load all yearly sales files into a single fact table:  
  - Automatically incorporates new yearly files upon refresh.  
  - Handles missing files without errors.  
- Transformed the **Location** column by splitting **Country** and **City** to enable Geo maps.  
- Updated and formatted date fields to ensure proper usage in visuals.  
- Created a unique **GeoKey** by hashing and combining **Country** and **City** to connect Sales and Geography tables.  

### 🔹 **Data Model**  
- Established relationships between tables (Sales, Geography, Product, Subcategories, Categories, Sales Representatives) using a calendar table for time-based analysis.  

### 🔹 **DAX Calculations**  
1. **Total Revenue**: Calculates total revenue by multiplying units sold by the product's retail price.  
    ```DAX  
    Total Revenue = Sales[Units] * Product[Retail Price]
    ```  

2. **Total Cost**: Calculates total cost by multiplying units sold by the product's standard cost.  
    ```DAX  
    Total Cost = Sales[Units] * Product[Standard Cost]
    ```  

3. **Gross Profit**: Finds the gross profit as the difference between total revenue and total cost.  
    ```DAX  
    Gross Profit = [Total Revenue] - [Total Cost]
    ```  

4. **GeoKey**: Creates a unique key for connecting the Sales and Geography tables by combining country and city.  
    ```DAX  
    GeoKey = CONCATENATE(Sales[Country], Sales[City])
    ```  

5. **AverageRFMScore**: Calculates the weighted average of normalized Recency, Frequency, and Monetary values.  
    ```DAX  
    AverageRFMScore =  
    ( 'OnlineRetail'[NormalizedRecency]  
      + 2 * 'OnlineRetail'[NormalizedFrequency]  
      + 3 * 'OnlineRetail'[NormalizedMonetary]  
    ) / 5
    ```  

6. **Customer Category**: Categorizes customers into Silver, Gold, and Diamond tiers based on the RFM score.  
    ```DAX  
    CustomerCategory =  
    SWITCH(  
        TRUE(),  
        'OnlineRetail'[AverageRFMScore] >= 0.6, "Diamond",  
        'OnlineRetail'[AverageRFMScore] >= 0.3 && 'OnlineRetail'[AverageRFMScore] < 0.6, "Gold",  
        'OnlineRetail'[AverageRFMScore] < 0.3, "Silver"  
    )
    ```  

---

## 📊 **Dashboard Highlights**  
1. **Sales Performance Overview**:  
   - Key metrics like total revenue, gross profit, and total sales at a glance.  
2. **Monthly Trends**:  
   - Dynamic column charts showcasing monthly performance, sorted from January to December.  
3. **Regional Insights**:  
   - Geo maps and pie charts display performance by country and region.  
4. **Category and Product Analysis**:  
   - Detailed comparison of sales across categories, subcategories, and individual products.  
5. **Profitability Analysis**:  
   - Waterfall charts highlighting the breakdown of gross profit.  

---

## 🔢 **Types of Visualizations**  
- **Cards**: Total Sales, Gross Profit, Total Revenue.  
- **Column Charts**: Monthly Sales Trends.  
- **Clustered Column Charts**: Revenue and Profit by Product Categories.  
- **Slicers**: Filter by Product, Category, Region, Sales Rep, Date.  
- **Pie Charts**: Sales distribution by Region or Category.  
- **Waterfall Charts**: Gross Profit breakdown.  
- **Gauge Charts**: Progress toward sales targets.  

---

## ⚡ **Technologies Used**  
- **Power BI**: Data modeling, DAX, and visualization.  
- **Power Query**: Data cleaning and transformation.  
- **DAX Functions**: For calculated columns and measures.  
- **Data Sources**: SQL databases, Excel sheets, CSV files.  

---

## 📚 **Key Learnings**  
- **Efficient Data Preprocessing**: Learned that **80% of analysis time** is spent on cleaning and preparing data.  
- **Advanced DAX Calculations**: Developed a deeper understanding of creating complex measures.  
- **Resilient Data Loading**: Implemented dynamic file handling for scalable data ingestion.  
- **Data Visualization**: Designed an intuitive dashboard that translates raw data into actionable insights.  

---

## 🚀 **Future Enhancements**  
- Incorporate machine learning models for **sales forecasting**.  
- Add KPIs to measure **customer acquisition and retention rates**.  
- Automate report distribution using Power BI Service.  

---

## 💬 **Let’s Connect!**  
Have feedback or suggestions for improving this dashboard? Let’s discuss and share ideas!  

**GitHub Repository**: https://github.com/Saimu-71/Sales-Performance-Analysis-Dashboard/
**LinkedIn**: https://www.linkedin.com/in/tanshen-mahamud-saimu-066a471a6/
