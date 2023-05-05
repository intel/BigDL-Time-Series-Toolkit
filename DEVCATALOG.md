# Time Series Analysis with BigDL Time Series Toolkit

## Introduction
Use BigDL Time Series Toolkit (previous known as BigDL-Chronos or Chronos) to build time series analysis (including forecasting and anomaly detection) applications.  This workflow provides instructions on how to train and inference a Temporal Convolution Neural Network on BigDL Time Series Toolkit using time series dataset to carry out forecasting task as an example.

Check out more workflow examples and reference implementations in the Developer Catalog.

## Solution Technical Overview

Time series forecasting could be a critical demand in real-life senarios, such as network loading prediction, server utilization prediction, traffic flow prediction and so on. While the developing process for an AI end-to-end could be error-prone and time-consuming, let alone meeting a strict accuracy or performance requirement.

BigDL Time Series Toolkit supports building end-to-end (data loading, processing, built-in model, training, tuning, inference) AI solution on single node or cluster.

- More than 10 built-in models for forecasting and anomaly detection
- Performance tuning for extreme latency/throughput on Intel hardware
- Data processing, model training and hyperparameter tunning on single node or cluster

## Solution Technical Details
Following is a block chart for BigDL Time Series Toolkit.

![Toolkit](https://user-images.githubusercontent.com/35031544/231412648-e7ae8d16-b513-428d-8332-6aecdd8b415d.png)

More specifically, users could load their data to `TSDataset` for preprocessing and feature engineering. The processed data could be fed into `Forecaster` or `Detector` for training and prediction. Easy tuning work (performance and accuracy) could be done within `Forecaster`, while for large scale tunning users may train their model through `AutoTSEstimator`.


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

## Get Started

### Download the Workflow Repository

**There is no need to download the workflow repo if you only want to try the workflow on docker container.**

Create a working directory for the workflow and clone the [Main
Repository](https://github.com/intel-analytics/BigDL.git) repository into your working directory.

```
# For example...
mkdir ~/work && cd ~/work
git clone https://github.com/intel-analytics/BigDL.git
```

### Download the Datasets
The dataset we will use in our workflow example is a subset of [Numenta Anomaly Benchmark](https://github.com/numenta/NAB/tree/v1.0), which is not contained in our docker image or workflow directory.

Users **do not need to download it manually** since the workflow script will download the dataset automatically.

---

## Run Using Docker
Follow these instructions to set up and run our provided Docker image.
For running on bare metal, see the [bare metal instructions](#run-using-bare-metal)
instructions.

### Set Up Docker Engine
You'll need to install Docker Engine on your development system.
Note that while **Docker Engine** is free to use, **Docker Desktop** may require
you to purchase a license.  See the [Docker Engine Server installation
instructions](https://docs.docker.com/engine/install/#server) for details.

### Set Up Docker Image
Pull the provided docker image.
```bash
docker pull intelanalytics/bigdl-chronos:latest
```

This docker image already contains a basic BigDL Time Series Toolkit conda environment with minimal dependencies and the workflow example notebook. Some additional dependencies will be installed later in section **Run Docker Image**.

### Run Docker Image
Run the workflow using the ``docker run`` command, as shown:
```bash
sudo docker run -it --rm --net=host intelanalytics/bigdl-chronos:latest bash
```
If your environment requires a proxy to access the internet, export your
development system's proxy settings to the docker environment when you run the docker:

```bash
-e ftp_proxy=${ftp_proxy} \
-e FTP_PROXY=${FTP_PROXY}\
-e http_proxy=${http_proxy} \
-e HTTP_PROXY=${HTTP_PROXY} \
-e https_proxy=${https_proxy} \
-e HTTPS_PROXY=${HTTPS_PROXY} \
-e no_proxy=${no_proxy} \
-e NO_PROXY=${NO_PROXY} \
-e socks_proxy=${socks_proxy} \
-e SOCKS_PROXY=${SOCKS_PROXY}
```

Inside the docker, we could run the workflow example
```bash
# install some additional dependencies
pip install --pre --upgrade bigdl-chronos[pytorch] matplotlib notebook==6.4.12

# transform the notebook to a runnable python script
cd colab-notebook
jupyter nbconvert --to python chronos_nyc_taxi_tsdataset_forecaster.ipynb
sed '26,40d' chronos_nyc_taxi_tsdataset_forecaster.py > chronos_nyc_taxi_forecaster.py

# start the script
python chronos_nyc_taxi_forecaster.py
```

---

## Run Using Bare Metal
Follow these instructions to set up and run this workflow on your own development system. For running a provided Docker image with Docker, see the [Docker instructions](#run-using-docker).

### Set Up System Software
Our examples use the ``conda`` package and enviroment on your local computer.
If you don't already have ``conda`` installed, see the [Conda Linux installation
instructions](https://docs.conda.io/projects/conda/en/stable/user-guide/install/linux.html).

### Set Up Workflow
Run these commands to set up the workflow's conda environment and install required software:
```bash
# If you have done this in section Workflow Repository
# please skip next 2 commands
mkdir ~/work && cd ~/work
git clone https://github.com/intel-analytics/BigDL.git

# setup a conda environemnt for BigDL Time Series Toolkit
cd ~/work/BigDL
conda create -n my_env python=3.7 setuptools=58.0.4
conda activate my_env
pip install --pre --upgrade bigdl-chronos[pytorch] matplotlib notebook==6.4.12

# transform the workflow example to python script
cd python/chronos/colab-notebook
jupyter nbconvert --to python chronos_nyc_taxi_tsdataset_forecaster.ipynb
sed '26,40d' chronos_nyc_taxi_tsdataset_forecaster.py > chronos_nyc_taxi_forecaster.py
```

### Run Workflow
Use these commands to run the workflow:
```bash
python chronos_nyc_taxi_forecaster.py
```

## Expected Output
This workflow provides instructions on how to train and inference a Temporal Convolution Neural Network on BigDL Time Series Toolkit using time series dataset to carry out forecasting task as an example.

The main part will be the model training progress bar, you may expect the whole workflow example be completed in 1 minute.

```bash
# ...
Epoch 2: 100%|█████████████████████████████████████████████████████████████████████████████████████████████████████████████████████| 274/274 [00:21<00:00, 12.93it/s, loss=0.0253]
# ...
```
## Summary and Next Steps
The workflow example only shows a very small portion of what BigDL Time Series Toolkit can do. Users may refer to our document to see detailed information.

## Learn More
- [Document First page](https://bigdl.readthedocs.io/en/latest/doc/Chronos/index.html) (you may start from here and navigate to other pages)
- [How to Guides](https://bigdl.readthedocs.io/en/latest/doc/Chronos/Howto/index.html) (If you are meeting with some specific problems during the usage, how-to guides are good place to be checked.)
- [Example & Use-case library](https://bigdl.readthedocs.io/en/latest/doc/Chronos/QuickStart/index.html) (Examples provides short, high quality use case that users can emulated in their own works.)


## Troubleshooting
Nothing for now

## Support

The BigDL Time Series Toolkit team tracks both bugs and
enhancement requests using [GitHub
issues](https://github.com/intel-analytics/BigDL/issues).