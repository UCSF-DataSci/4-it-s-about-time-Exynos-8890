[![Open in Codespaces](https://classroom.github.com/assets/launch-codespace-2972f46106e565e64193e422d61a12cf1da4916b45550586e14ef0a7c637dd04.svg)](https://classroom.github.com/open-in-codespaces?assignment_repo_id=19340903)

# 时间序列分析作业 / Time Series Analysis Assignment

## 概述 / Overview

在本次作业中，您将应用时间序列分析技术来分析来自"诱导压力和运动会话的可穿戴设备数据集"的真实健康数据。该数据集包含使用Empatica E4可穿戴设备，从健康志愿者在结构化急性压力诱导和有氧/无氧运动会话期间收集的生理信号（皮电活动、血容量脉搏、心率、温度）。

In this assignment, you will apply time series analysis techniques to analyze real health data from the "Wearable Exam Stress Dataset". This dataset contains physiological signals (electrodermal activity, blood volume pulse, heart rate, temperature) collected from healthy volunteers using Empatica E4 wearable devices during structured acute stress induction and aerobic/anaerobic exercise sessions.

数据集链接 / Dataset link：https://physionet.org/content/wearable-exam-stress/1.0.0/

### 方法 / Methodology

受试者需要在参加期中考试（考试1和2）和期末考试时佩戴FDA批准的Empatica E4腕带。E4记录了皮肤电导率、心率、体温和运动（加速度计）。

Subjects were required to wear FDA-approved Empatica E4 wristbands during midterm exams (Exams 1 and 2) and the final exam. The E4 recorded skin conductance, heart rate, body temperature, and movement (accelerometer).

每个E4设备都有一个标签号。在参加考试时，每位参与者领取一个E4设备，并在与所选E4设备相对应的文档上写下他们的名字。数据收集后，参与者将他们的E4腕带归还给研究团队。最后，课程讲师向研究团队的其他成员提供了与设备编号相对应的成绩。

Each E4 device has a tag number. When attending exams, each participant received an E4 device and wrote their name on documentation corresponding to the selected E4 device. After data collection, participants returned their E4 wristbands to the research team. Finally, the course instructor provided corresponding grades to other members of the research team.

### 数据说明 / Data Description

数据包含在**三次考试会话**（期中考试1、期中考试2和期末考试）期间记录的**皮电活动**、**心率**、**血容量脉搏**、**皮肤表面温度**、**心跳间隔**和**加速度计数据**，以及相应的成绩。所有数据均为Empatica E4设备的直接输出，已进行了处理。期中考试时长为1.5小时，期末考试时长为3小时。以下是关于数据集的一些有用说明：

The data contains **electrodermal activity**, **heart rate**, **blood volume pulse**, **skin surface temperature**, **inter-beat intervals**, and **accelerometer data** recorded during **three exam sessions** (Midterm 1, Midterm 2, and Final), as well as corresponding grades. All data is direct output from the Empatica E4 device and has been processed. Midterm exams lasted 1.5 hours, and the final exam lasted 3 hours. Here are some useful notes about the dataset:

-   StudentGrades.txt包含每位学生的成绩

-   Data.zip文件包含每位参与者的文件夹，命名为S1、S2等

-   在每位参与者对应的文件夹下，有三个文件夹'Final'、'Midterm 1'和'Midterm 2'，对应三次考试

-   每个文件夹包含csv文件：'ACC.csv'、'BVP.csv'、'EDA.csv'、'HR.csv'、'IBI.csv'、'tags.csv'、'TEMP.csv'和'info.txt'

-   'info.txt'包含每个文件的详细信息

-   所有Unix时间戳都进行了日期偏移以进行匿名处理，但没有进行时间偏移。日期偏移的方式不会改变日光节约时间设置（CT/CDT）

-   所有考试都在上午9:00开始（CT或CDT，取决于与Unix时间戳对应的日期）。期中考试时长为1.5小时，期末考试时长为3小时

-   数组的采样频率在'info.txt'中提供

-   数据集包含两名女性和八名男性参与者，但出于匿名目的，未标明性别

-   StudentGrades.txt contains grades for each student

-   Data.zip file contains folders for each participant, labeled as S1, S2, etc.

-   Under each participant's folder, there are three folders 'Final', 'Midterm 1', and 'Midterm 2', corresponding to the three exams

-   Each folder contains csv files: 'ACC.csv', 'BVP.csv', 'EDA.csv', 'HR.csv', 'IBI.csv', 'tags.csv', 'TEMP.csv', and 'info.txt'

-   'info.txt' contains detailed information about each file

-   All Unix timestamps have been date-shifted for anonymization, but have not been time-shifted. The date shifting was done in a way that does not change daylight savings time settings (CT/CDT)

-   All exams start at 9:00 AM (CT or CDT, depending on the date corresponding to the Unix timestamp). Midterm exams last 1.5 hours, and the final exam lasts 3 hours

-   Sampling rates for the arrays are provided in 'info.txt'

-   The dataset includes two female and eight male participants, but gender is not indicated for anonymity purposes

## 数据集下载 / Dataset Download

1.  访问 https://physionet.org/

2.  导航到数据列表

3.  在"开放数据库"部分找到"A Wearable Exam Stress Dataset for Predicting Cognitive Performance in Real-World Settings"

4.  将下载的文件解压到本仓库中的`data`目录

5.  Visit https://physionet.org/

6.  Navigate to the data list

7.  Find "A Wearable Exam Stress Dataset for Predicting Cognitive Performance in Real-World Settings" in the "Open Databases" section

8.  Extract the downloaded files to the `data` directory in this repository

## 作业结构 / Assignment Structure

本作业分为三个部分：

This assignment is divided into three parts:

### 1: 数据探索和预处理 / Data Exploration and Preprocessing

在这部分，您将在`part1_exploration.ipynb`中实现以下函数：

In this part, you will implement the following functions in `part1_exploration.ipynb`:

1.  `load_data(data_dir='data/raw')`：
    -   从数据集加载所有生理数据

    -   返回一个pandas DataFrame，包含以下列：\['timestamp', 'heart_rate', 'eda', 'temperature', 'subject_id', 'session'\]

    -   时间戳可以是datetime对象或数值

    -   数据应按受试者和会话组织

    -   列名不区分大小写

    -   Load all physiological data from the dataset

    -   Return a pandas DataFrame with the following columns: \['timestamp', 'heart_rate', 'eda', 'temperature', 'subject_id', 'session'\]

    -   Timestamps can be datetime objects or numeric

    -   Data should be organized by subject and session

    -   Column names are case-insensitive
2.  `preprocess_data(data, output_dir='data/processed')`：
    -   使用适当的插补方法处理缺失值（允许最多1%的缺失值）

    -   将不规则时间序列重新采样为规则间隔

    -   使用z-score方法移除异常值（阈值=3.5）

    -   将处理后的数据保存到输出目录中的文件：

        -   每个受试者一个文件：'S1_processed.*'、'S2_processed.*'等
        -   支持的格式：.csv、.parquet或.feather
        -   每个文件应包含该受试者的所有会话

    -   返回处理后的DataFrame

    -   Handle missing values using appropriate imputation methods (allowing at most 1% missing values)

    -   Resample irregular time series to regular intervals

    -   Remove outliers using z-score method (threshold = 3.5)

    -   Save processed data to files in the output directory:

        -   One file per subject: 'S1_processed.*', 'S2_processed.*', etc.
        -   Supported formats: .csv, .parquet, or .feather
        -   Each file should contain all sessions for that subject

    -   Return the processed DataFrame
3.  `plot_physiological_signals(data, subject_id, session, output_dir='plots')`：
    -   为每个生理信号创建带有子图的图形

    -   添加适当的标签和标题

    -   将图形保存到输出目录，文件名为'S{subject_id}\_{session}\_signals.png'

    -   返回matplotlib图形对象

    -   Create a figure with subplots for each physiological signal

    -   Add appropriate labels and titles

    -   Save the figure to the output directory with the filename 'S{subject_id}\_{session}\_signals.png'

    -   Return the matplotlib figure object

### 2: 时间序列建模 / Time Series Modeling

在这部分，您将在`part2_modeling.ipynb`中实现以下函数：

In this part, you will implement the following functions in `part2_modeling.ipynb`:

1.  `extract_time_series_features(data, window_size=60)`：
    -   从时间序列中提取滚动窗口特征

    -   对于每个窗口，计算：均值、标准差、最小值、最大值和滞后1的自相关

    -   特征名称不区分大小写，可以包含额外文本

    -   返回包含提取特征的DataFrame

    -   Extract rolling window features from time series

    -   For each window, calculate: mean, standard deviation, minimum, maximum, and lag-1 autocorrelation

    -   Feature names are case-insensitive and can contain extra text

    -   Return a DataFrame containing the extracted atures
2.  `build_arima_model(series, order=(1,1,1), output_dir='plots')`：
    -   对输入的时间序列拟合ARIMA模型

    -   创建并保存至少2个诊断图到输出目录：

        -   图名应包含'arima'并以'.png'结尾
        -   示例：'S1_Midterm 1_heart_rate_arima_fit.png'、'S1_Midterm 1_heart_rate_arima_residuals.png'

    -   返回拟合的模型对象

    -   模型应具有predict和fit方法

    -   Fit an ARIMA model to the input time series

    -   Create and save at least 2 diagnostic plots to the output directory:

        -   Plot names should include 'arima' and end with '.png'
        -   Examples: 'S1_Midterm 1_heart_rate_arima_fit.png', 'S1_Midterm 1_heart_rate_arima_residuals.png'

    -   Return the fitted model object

    -   The model should have predict and fit methods

### 3: 高级分析 / Advanced Analysis

在这部分，您将在`part3_advanced.ipynb`中实现以下函数：

In this part, you will implement the following functions in `part3_advanced.ipynb`:

1.  `extract_time_domain_features(data, window_size=60)`：
    -   从生理信号中提取时域特征

    -   对于每个窗口，计算：

        -   基本统计量：均值、标准差、最小值、最大值
        -   心率统计量：平均心率、心率标准差
        -   心跳间隔变异性：RMSSD、SDNN、pNN50

    -   返回包含提取特征的DataFrame

    -   特征名称应具有描述性，并在适当的地方包括单位

    -   Extract time-domain features from physiological signals

    -   For each window, calculate:

        -   Basic statistics: mean, standard deviation, minimum, maximum
        -   Heart rate statistics: mean heart rate, heart rate standard deviation
        -   Heart rate variability: RMSSD, SDNN, pNN50

    -   Return a DataFrame containing the extracted features

    -   Feature names should be descriptive and include units where appropriate
2.  `analyze_frequency_components(data, sampling_rate, window_size=60)`：
    -   对信号进行频域分析
    -   对于每个窗口，计算：
        -   使用Welch方法的功率谱密度（PSD）
        -   生理相关频段中的功率：
            -   极低频（VLF）：0.003-0.04 Hz
            -   低频（LF）：0.04-0.15 Hz
            -   高频（HF）：0.15-0.4 Hz
        -   LF/HF比值作为自主神经平衡的度量
    -   返回包含以下内容的字典：
        -   'frequencies'：频率值数组
        -   'power'：功率谱值数组
        -   'bands'：不同频段功率的字典
    -   将频率分析结果保存到输出目录：
        -   文件名应包含'fft'
        -   支持的格式：.npz、.npy或.csv
    -   Perform frequency-domain analysis on signals
    -   For each window, calculate:
        -   Power spectral density (PSD) using the Welch method
        -   Power in physiologically relevant frequency bands:
            -   Very low frequency (VLF): 0.003-0.04 Hz
            -   Low frequency (LF): 0.04-0.15 Hz
            -   High frequency (HF): 0.15-0.4 Hz
        -   LF/HF ratio as a measure of autonomic balance
    -   Return a dictionary containing:
        -   'frequencies': array of frequency values
        -   'power': array of power spectral values
        -   'bands': dictionary of power in different frequency bands
    -   Save frequency analysis results to the output directory:
        -   Filenames should include 'fft'
        -   Supported formats: .npz, .npy, or .csv
3.  `analyze_time_frequency_features(data, sampling_rate, window_size=60)`：
    -   应用小波变换分析时频特征
    -   对于每个窗口，计算：
        -   连续小波变换系数
        -   时频能量分布
        -   随时间变化的主导频率成分
    -   返回包含以下内容的字典：
        -   'scales'：小波尺度数组
        -   'coefficients'：小波系数数组
        -   'time_frequency_energy'：能量分布的2D数组
    -   将时频分析结果保存到输出目录：
        -   文件名应包含'wavelet'
        -   支持的格式：.npz、.npy或.csv
    -   Apply wavelet transforms to analyze time-frequency features
    -   For each window, calculate:
        -   Continuous wavelet transform coefficients
        -   Time-frequency energy distribution
        -   Dominant frequency components over time
    -   Return a dictionary containing:
        -   'scales': array of wavelet scales
        -   'coefficients': array of wavelet coefficients
        -   'time_frequency_energy': 2D array of energy distribution
    -   Save time-frequency analysis results to the output directory:
        -   Filenames should include 'wavelet'
        -   Supported formats: .npz, .npy, or .csv

## 评分标准 / Grading Criteria

您的作业将根据以下标准进行评分：

Your assignment will be graded based on the following criteria:

1.  **数据探索和预处理（第1部分）/ Data Exploration and Preprocessing (Part 1)**
    -   数据加载函数的正确实现

    -   适当处理缺失值和异常值

    -   正确重采样时间序列

    -   生成可视化的质量

    -   适当的文件组织和输出

    -   Correct implementation of data loading functions

    -   Appropriate handling of missing values and outliers

    -   Correct resampling of time series

    -   Quality of generated visualizations

    -   Appropriate file organization and output
2.  **时间序列建模（第2部分）/ Time Series Modeling (Part 2)**
    -   特征提取的正确实现

    -   适当的ARIMA模型拟合

    -   适当的模型评估

    -   Correct implementation of feature extraction

    -   Appropriate ARIMA model fitting

    -   Appropriate model evaluation
3.  **高级分析（第3部分）/ Advanced Analysis (Part 3)**
    -   时域特征提取的正确实现

    -   适当的频域分析

    -   适当的小波变换分析

    -   特征解释和可视化的质量

    -   Correct implementation of time-domain feature extraction

    -   Appropriate frequency-domain analysis

    -   Appropriate wavelet transform analysis

    -   Quality of feature interpretation and visualization

## 资源 / Resources

-   讲义幻灯片和演示笔记本 / Lecture slides and demonstration notebooks
-   [PhysioNet可穿戴数据集文档 / PhysioNet Wearable Dataset Documentation](https://physionet.org/content/wearable-exam-stress/1.0.0/)
-   [Pandas时间序列文档 / Pandas Time Series Documentation](https://pandas.pydata.org/pandas-docs/stable/user_guide/timeseries.html)
-   [Scikit-learn文档 / Scikit-learn Documentation](https://scikit-learn.org/stable/modules/classes.html)
-   [SciPy信号处理文档 / SciPy Signal Processing Documentation](https://docs.scipy.org/doc/scipy/reference/signal.html)