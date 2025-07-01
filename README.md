# Hotel Booking Data Analysis Project Report

##Table of Contents

  [Project overview](#project_overview)

## 1. Project overview

The objective of this project is to analyze hotel booking data to uncover patterns, trends, and actionable insights that can help improve booking rates, reduce cancellations, and enhance revenue management. The analysis leverages historical booking data from kaggle and employs various data analysis and visualization techniques.

---

## 2. Data Overview

- **Data Source:** [Kaggle]
- **Main Features:**
  - Booking ID
  - Arrival Date
  - Number of Adults/Children
  - Country of Origin
  - Booking Channel
  - Room Type
  - Special Requests
  - Lead Time
  - Deposit Type
  - Customer Type
  - Cancellation Status
  - Other relevant features

---

## 3. Data Cleaning & Preprocessing:

 Data cleanig is neccessary step before analysing data
 
  -Removed duplicate records and handled missing values.
  
  -Dropped irrelevant columns (email, phone-number, credit_card, name, agent, company).
  
  -Converted reservation_status_date to datetime for temporal analysis.
  
  -Encoded categorical variables and explored their unique values.
  
  -Filtered out outliers in ADR (e.g., removed values above 5000).
  
  -Created new features such as month and month_name for time-based grouping.

---

## 4. Exploratory Data Analysis (EDA)

  #4.1 Booking Trends
 -Visualized bookings by month using count plot
       
            ----# Extract month number and name
            df['month'] = df['reservation_status_date'].dt.month
            df['month_name'] = df['reservation_status_date'].dt.strftime('%B')
            
            # Order the months correctly
            month_order = ['January', 'February', 'March', 'April', 'May', 'June',
                           'July', 'August', 'September', 'October', 'November', 'December']
            df['month_name'] = pd.Categorical(df['month_name'], categories=month_order, ordered=True)
            
            # Plot with cancellation hue
            plt.figure(figsize=(12, 6))
            sns.countplot(data=df, x='month_name', hue='is_canceled')
            plt.title('Bookings and Cancellations by Reservation Status Month')
            plt.xlabel('Month')
            plt.ylabel('Number of Bookings')
            plt.legend(title='Canceled', labels=['Not cancelled', 'Cancelled'])
            plt.xticks(rotation=45)
            plt.tight_layout()
            plt.show()
    -----
            
  -Identified peak seasons: July and August, showing significantly higher booking volumes.

    ----month_adr=df[df['is_canceled']==1].groupby('month')[['adr']].sum().reset_index()
        plt.figure(figsize=(5,4))
        plt.title('Adr per month')
        sns.barplot(x='month',y='adr',data=month_adr)
        plt.show()
    ----
  ##4.2 Cancellation Analysis
  
  -Overall cancellation rate: 37% (approx.)
  -Higher cancellation rates observed with:
        
  -Longer lead times
  -Bookings without deposits
  -Transient customer type
     
  -City Hotels experienced higher cancellation rates than Resort Hotels.

##4.3 Customer Segmentation

-Top countries by bookings: Portugal, United Kingdom, France, Spain, and Germany.

-Most common booking channels: Online Travel Agents (OTAs) like Expedia and Booking.com.

-Cancellations were more frequent among OTA bookings.

##4.4 Revenue Insights

-ADR (Average Daily Rate):

-Higher for Resort Hotels compared to City Hotels.

-Clear seasonal spike in ADRs during summer months (especially July and August).

-Revenue was higher for non-canceled bookings and dropped significantly for canceled bookings..

---

## 5. Key Findings

-High Cancellation Rates: Notable among bookings without deposits, transient guests, and OTA channels.

-Seasonality: Peaks in bookings and revenue during summer (July–August).

-Channel Performance: OTAs contribute most bookings but also have the highest cancellation rates.

-Customer Origin: Most frequent guests from Portugal, UK, and France.


## 6. Recommendations

- Encourage or require deposits to reduce cancellations.
- 
-Focus marketing campaigns on off-peak seasons like November–March.

-Segment and prioritize high-value, low-cancellation customer types for retention.

-Evaluate cancellation policies for OTA bookings and explore direct booking incentives.


## 7. Future Work

- Build predictive models to estimate cancellation likelihood based on booking features.
- 
-Perform sentiment analysis on guest reviews to enhance service and reduce negative feedback.

-Integrate external data like holidays, events, and weather for more accurate demand forecasting.


## 8. Conclusion

The hotel booking data analysis uncovered actionable insights regarding customer behavior, seasonality, and revenue drivers. Implementing the recommendations can help optimize bookings and reduce cancellations, ultimately increasing profitability.

---

## 9. Appendix

- [Link to code/notebook]
- [Key visualizations/charts]
- [Data dictionary]
