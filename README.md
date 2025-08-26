# ML-powered customer analytics

## Project Overview

This project demonstrates the development of an **unsupervised ML algorithm** that segments customers based on **lifetime value (LTV)** and provides **actionable business insights**. The goal is to help e-commerce companies identify high-value customers, understand purchasing behavior, and inform personalized marketing strategies.

The platform uses the **Online Retail Dataset (UCI Machine Learning Repository)** and was developed and deployed as a **proof-of-concept in one day**.



## Dataset

* **Source:** [UCI Online Retail Dataset](https://archive.ics.uci.edu/ml/datasets/online+retail)
* **Features:**

| Column      | Description                |
| ----------- | -------------------------- |
| InvoiceNo   | Unique invoice number      |
| StockCode   | Unique product code        |
| Description | Product description        |
| Quantity    | Number of items purchased  |
| InvoiceDate | Date and time of invoice   |
| UnitPrice   | Price per unit             |
| CustomerID  | Unique customer identifier |
| Country     | Customer country           |

* **Data preprocessing steps:**

  * Removed rows without `CustomerID`
  * Removed negative `UnitPrice` rows
  * Aggregated at **customer-level** to compute RFM metrics: Recency, Frequency, Monetary (TotalRevenue)

---

## Methodology

1. **Customer Segmentation**

   * Calculated **RFM metrics**:

     * **Recency:** Days since last purchase
     * **Frequency:** Number of invoices/orders
     * **Monetary:** Total spend
   * Due to heavy skew in the Monetary and Frequency distributions, standard IQR-based outlier detection was ineffective. Instead, thresholds were set empirically, guided by Elbow and Silhouette analysis, to ensure well-separated, meaningful customer segments.
   * Applied **log transformation** and **standard scaling**
   * Used **KMeans clustering** to identify 3 segments:

     * **VIP** (Blue)
     * **Middle Class** (Turquoise)
     * **Inactive** (Brow)

  ![clusters](https://raw.githubusercontent.com/JavieraAlmendrasVilla/Customer-Segmentation/main/customer_segments_3d.png
)

2. **KPIs Computed per Segment**

   * **Total Revenue per Segment**
   * **Average Order Value (AOV)**
   * **Purchase Frequency**
   * **Recency**
   * **Segment Size**
   * **Revenue Contribution (%)**

See the Analytics Dashboard on [Tableau](https://public.tableau.com/views/CustomerSegmentationAnalysis_17562205666720/Dashboard1?:language=en-US&:sid=&:redirect=auth&:display_count=n&:origin=viz_share_link)

---

## Key Findings

| Segment      | % of Customers | % of Revenue | Notes                                                             |
| ------------ | -------------- | ------------ | ----------------------------------------------------------------- |
| VIP          | 21%            | 57%          | High frequency, high spend. Most profitable segment.              |
| Middle Class | 40%            | 35%          | Highest AOV, lower frequency than VIP. Opportunity for upselling. |
| Inactive     | 39%            | 8%           | Rarely purchase; low revenue contribution.                        |

**Insights:**

* 61% of customers (VIP + Middle Class) generate **92% of total revenue**
* Middle Class customers have **higher AOV** but **half the frequency** of VIPs
* Targeted campaigns should focus on **retention and upsell** for VIP and Middle Class customers
* Inactive segment can be targeted with **win-back campaigns** or cost-efficient marketing strategies


---

## How to Run

1. Clone the repository:

```bash
git clone https://github.com/JavieraAlmendrasVilla/Customer-Segmentation.git
```

2. Install dependencies:

```bash
pip install -r requirements.txt
```

3. Run the notebook:

```bash
jupyter notebook customer_segmentation.ipynb
```

---

## Technologies Used

* Python (pandas, numpy, matplotlib, seaborn, scikit-learn)
* Jupyter Notebook
* KMeans clustering for segmentation
* PCA for visualization

---

## Portfolio Takeaway

This project demonstrates the ability to:

* Preprocess and clean real-world e-commerce data
* Compute RFM metrics and detect outliers
* Segment customers with unsupervised learning
* Derive actionable business insights
* Visualize results clearly for stakeholders

---

If you want, I can **also add a compact “Key Results & Figures” section** in the README with **charts and KPIs embedded**, so your GitHub page looks visually appealing.

Do you want me to do that next?
