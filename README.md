# NetSec_lab: DoS Attack Detection in an IoT Environment

## Overview

This project focuses on the detection of Denial-of-Service (DoS) and Distributed Denial-of-Service (DDoS) attacks in IoT (Internet of Things) networks using network traffic data. The classification is performed by analyzing both TCP and UDP traffic patterns based on various packet features. By applying statistical thresholds and machine learning techniques, the system classifies network traffic as either "DoS/DDoS" or "Other" (normal or other types of attacks).

The project also demonstrates how to validate the model using a test dataset and evaluate its accuracy in detecting suspicious network behavior.

## Key Features

### Data Preprocessing:

- The dataset consists of network traffic records collected from an IoT environment.
- **Key features used for analysis:**
  - Connection state (`conn_state`)
  - Number of destination/source packets (`dst_pkts`, `src_pkts`)
  - Number of destination/source bytes (`dst_ip_bytes`, `src_ip_bytes`)
- The attack types are grouped into two main categories:
  - **DoS or DDoS** attacks
  - **Other** (including normal traffic and other types of attacks such as backdoor, scanning, etc.)

### Data Splitting:

- The dataset is shuffled and split into training (80%) and testing (20%) sets.
- The training data is further divided into smaller subsets to calculate metrics on connection states and packet statistics.

### Connection State Classification:

- TCP traffic is classified into "Suspicious" or "Not Suspicious" categories based on connection states (`conn_state`). A mapping of connection states to these two categories is applied.
- The proportion of suspicious TCP connections in each subset is calculated, which helps in identifying DoS or DDoS traffic.

### Packet Feature Analysis for UDP:

- UDP traffic is analyzed based on the number of packets and bytes transferred.
- For each subset, the mean values of `dst_pkts`, `src_pkts`, `dst_bytes`, and `src_bytes` are calculated for both DoS/DDoS and non-DoS traffic. These mean values are used to set statistical thresholds.

### Classification Algorithm:

The detection model (Network Traffic Classifier, or NTC) works by:
- Analyzing TCP traffic for suspicious connection states.
- Analyzing UDP traffic to check if features (packets/bytes) exceed predefined thresholds.

A subset is classified as DoS/DDoS if any of the following conditions are met:
- The percentage of suspicious TCP connections exceeds the threshold.
- The percentage of UDP packets/features exceeding thresholds is significant.

### Model Validation:

- The classifier is validated using the test dataset.
- Users can select between "DoS/DDoS" or "Other" traffic types to evaluate the model.
- The accuracy of the classifier is calculated based on its performance in detecting the correct labels for each subset.

## Requirements

### Libraries:
- `pandas`: For data manipulation and analysis.
- `numpy`: For numerical calculations.
- `sklearn`: For splitting the dataset into training and testing sets.
- `matplotlib`: For plotting results.

### Environment:
- Google Colab or a local environment with access to Google Drive (for loading the dataset).

## Instructions

### Mount Google Drive:
- The dataset (`Train_Test_Network.csv`) should be stored in Google Drive. Mount Google Drive to access it.

### Data Preprocessing:
- The dataset is read, preprocessed, and split into training and testing sets.

## Conclusion

This project provides an efficient approach for detecting DoS and DDoS attacks in an IoT environment by analyzing network traffic patterns. By using both TCP connection states and UDP packet features, the system can accurately classify network flows and identify malicious activity.
