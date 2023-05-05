## Solution Technical Overview

Time series forecasting could be a critical demand in real-life senarios, such as network loading prediction, server utilization prediction, traffic flow prediction and so on. While the developing process for an AI end-to-end could be error-prone and time-consuming, let alone meeting a strict accuracy or performance requirement.

BigDL Time Series Toolkit supports building end-to-end (data loading, processing, built-in model, training, tuning, inference) AI solution on single node or cluster.

- More than 10 built-in models for forecasting and anomaly detection
- Performance tuning for extreme latency/throughput on Intel hardware
- Data processing, model training and hyperparameter tunning on single node or cluster
## Validated Hardware Details
BigDL Time Series Toolkit and the workflow example shown below could be run widely on both Core™ and Xeon® series processers.

|| Recommended Hardware         | Precision |
|---| ---------------------------- | --------- |
|CPU| Intel® 4th Gen Xeon® Scalable Performance processors| BF16 |
|CPU| Intel® 1st, 2nd, 3rd, and 4th Gen Xeon® Scalable Performance processors| FP32/INT8 |
|Memory|>192G|
|Disk|>10G|

## How it Works
The example workflow takes history taxi traffic number in past 1 day and predict future 30 min's taxi traffic number.
