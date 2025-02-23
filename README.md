# Detecting Stale Petrol Stations Using Probe Data

## Overview
This project aims to detect stale (non-operational) petrol stations using probe data. We employ Explainable AI (XAI), and anomaly detection to identify stations that are no longer in use. Our approach eliminates the need for traditional geospatial tools like QGIS and enables automated identification of stale petrol pumps.

## Solution Approach
### 1. **Rule-Based Spatial Outlier Detection & Adaptive Buffering**
   - This method detects stale petrol stations based on defined spatial rules and adaptive buffering techniques.
   - In this approach, stale stations are identified based on:
1. Low probe count (less than a defined threshold, e.g., 5 probes).
2. Road type: Petrol stations located on for e.g., "residential" or "tertiary" roads are flagged as stale.
3. Tunnel status: If the station is near a tunnel (i.e., tunnel column is not NaN), it may indicate a difficult-to-access location, which could also be flagged.
4. Outlier Detection (IQR Method): Probe data near stations is analyzed using an adaptive buffer calculation based on probe density. The Interquartile Range (IQR) method is used to detect outliers in probe counts. Petrol stations with probe counts significantly above or below the normal range are flagged as stale.
- The rule-based stale stations and outlier stations are combined and stored in a new GeoDataFrame. Petrol stations that fall outside defined spatial norms are flagged as stale.

### 2. **Anomaly Detection with Explainable AI (XAI)**
   - We employ an **Isolation Forest Model** to detect anomalies in petrol station activity.
   - The model is trained on normalized probe data to identify stations with significantly different characteristics.
   - Benefits:
     - **Scalability**: Can be applied to different locations with varying rules.
     - **Trainable Model**: The model can adapt to new data patterns over time.
     - **Frequent Updates**: The model can be continuously improved with new data inputs.

## Workflow
1. **Data Cleaning**: Remove inconsistencies and prepare the dataset for analysis.
2. **Data Normalization**: Ensure uniform scaling for better anomaly detection.
3. **Fine-Tuned Isolation Forest Model Development**: Train the model on petrol station probe data.

## Results
### **Rule-Based Approach Results**
- Petrol stations that violated predefined spatial norms were flagged as stale.
- Example non-stale petrol pumps: Place ID 337, Place ID 343.
![image](https://github.com/user-attachments/assets/e82cc31b-4793-4a2c-9ddd-5f288203c48c)


### **Anomaly-Based Approach Results**
- The Isolation Forest model successfully identified stale petrol stations based on probe data anomalies.
- Anomaly detection provided an automated, scalable solution compared to static rule-based methods.

  ![image](https://github.com/user-attachments/assets/773611f6-5023-40a9-9458-2e853bf04d46)


## Why Our Solution is Better
✅ **Automation**: Eliminates manual detection and reduces reliance on tools like QGIS.  
✅ **Adaptability**: Model can be trained and updated for different locations.  
✅ **Scalability**: Works across various datasets without predefined spatial rules.  


## Installation & Setup
1. Clone the repository:
   ```sh
   git clone https://github.com/SEJALHANMANTE/StalePetrolStationDetectionUsingProbeData.git
   ```
2. Navigate to the project folder:
   ```sh
   cd StalePetrolStationDetectionUsingProbeData
   ```






