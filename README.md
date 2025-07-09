Dynamic Pricing for Urban Parking Lots

🔹 Overview

This project implements a real-time dynamic pricing engine for 14 urban parking lots. The pricing adjusts based on real-time data such as occupancy, traffic, queue length, vehicle type, and special events. The primary goal is to simulate smart urban pricing that maximizes parking lot utilization while minimizing congestion.

The project is built as part of the Summer Analytics 2025 Capstone hosted by the Consulting & Analytics Club × Pathway.

📊 Tech Stack

Python 3.11

Pandas & NumPy: Data preprocessing and analysis

Pathway: Real-time data streaming, windowing, and transformations

Bokeh + Panel: Real-time interactive visualizations

Google Colab: Development and experimentation environment

Mermaid: For architecture diagramming

🛠️ Architecture Diagram (Model 1 & Model 2)

![Untitled diagram _ Mermaid Chart-2025-07-09-181525](https://github.com/user-attachments/assets/e633c833-2369-454d-95bd-8683f3359034)


📚 Project Architecture & Workflow

✅ Step 1: Data Ingestion & Parsing

Input CSV contains 18,000+ rows of real-time parking logs.

LastUpdatedDate and LastUpdatedTime are merged and parsed to form Timestamp.

Latitude, Longitude, QueueLength, IsSpecialDay, and other context features are retained.

✅ Step 2: Pathway Stream Setup

Data is loaded into Pathway's replay_csv with schema definition.

Streaming rate is defined to simulate real-time ingestion.

A tumbling window of 1 day per parking lot is used for aggregation.

✅ Step 3: Model 1 (Baseline Linear Model)

Features: Occupancy Max, Occupancy Min, Capacity

Pricing Formula:

price = 10 + (occ_max - occ_min)/capacity

Purpose: Acts as a simple baseline reference.

✅ Step 4: Model 2 (Demand-Based Pricing)

Features: Average Occupancy, QueueLength, Traffic, Vehicle Type, Special Day

Demand Function:

demand = (occ_avg / cap) + 0.3 * queue_avg - 0.4 * traffic_weight + 0.6 * is_special + 0.3 * vehicle_weight

Price Function:

demand = clipped to [0, 2.5]
price = 10 + 0.2 * demand

✅ Step 5: Real-Time Visualization

Bokeh & Panel used for live multi-line plots

One line per parking lot with price vs. time (daily)



