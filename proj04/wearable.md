---
layout: page
title: UCSD ExtraSensory Dataset 📱
description: Description of the UCSD ExtraSensory wearable dataset in Project 4.
parent: 📊 Final Project
nav_exclude: true
---

# UCSD ExtraSensory Dataset 📱

This dataset was collected right here on the UCSD campus. It contains in-the-wild smartphone and smartwatch telemetry from 60 users, originally built to see how well mobile devices can recognize everyday behavioral context (you can read the original paper [here](https://escholarship.org/uc/item/71f6j42h)). 

The good news is that the heavy lifting of raw signal processing is already done. Instead of dealing with raw audio waves or accelerometer arrays, you get a tabular dataset of pre-computed features— such as battery drain rates, location variance, app usage, and audio MFCCs—paired with context labels reported by the users themselves. 

## Getting the Data
You'll need to grab the primary features and labels archive directly from the [ExtraSensory Project Page](http://extrasensory.ucsd.edu/). 

`ExtraSensory.per_uuid_features_labels.zip` (215 MB)
[Download Link](http://extrasensory.ucsd.edu/data/primary_data_files/ExtraSensory.per_uuid_features_labels.zip)

**Reading the Data:**
Unlike the other project options, this isn't a single file. The archive contains 60 separate `.csv.gz` files (one for each user, named by their anonymized ID). You'll want to write a quick loop using `os` or `glob` to read a subset of these files and concatenate them into a single pandas DataFrame. 

You can read the zipped files directly into pandas without extracting them first: 
`pd.read_csv(filepath, compression='gzip')`

| Column | Description |
|--------|-------------|
| `uuid` | Anonymized ID of the user (you can extract this from the filename) |
| `timestamp` | Unix time of the recorded 1-minute window |
| `label:SLEEPING` | Indicator (0, 1, or NaN) of whether the user was sleeping |
| `label:IN_CLASS` | Indicator (0, 1, or NaN) of whether the user was in class |
| `raw_acc:magnitude_stats:mean` | Mean magnitude of the accelerometer over the window |
| `discrete:app_state:is_active` | Indicator of whether an app was actively being used |
| `audio_naive:mfcc0:mean` | Pre-computed audio features (Mel-frequency cepstral coefficients). *Note: You don't need to process raw audio; these are just standard numerical columns!* |
| `lf_measurements:loc_variance` | Spatial variance of the user's location |

*(Note: There are over 200 feature columns and 51 label columns. You'll definitely want to use `df.filter(regex=...)` or column slicing to subset what you actually care about early in your notebook).*

If you want to pull in extra data like mood or absolute GPS coordinates, check out the supplementary zip files on their site.

## Idea Generation: Questions and Prediction Problems

The questions below are **broad categories and thought-starters**. We expect you to formulate your own specific questions, hypotheses, and prediction tasks based on what you find during your Exploratory Data Analysis. Do not just copy these verbatim; use them to inspire your own unique angle!

**Steps 1-4: Exploration and Testing**
- **Label Missingness:** Users constantly forget to manually tag what they are doing, leaving you with `NaN` values in the label columns. Think about whether the missingness of a specific label depends on passive sensor states (e.g., is the user's phone dead, or are they driving?). 
- **Behavioral and Contextual Shifts:** Do passive sensor readings (like "spatial entropy" or audio variance) change significantly when users report being in different states (like socializing versus studying)?
- **Digital Habits:** Are there statistical relationships between how a user interacts with their phone OS (switching apps, screen unlocks) and their physical activity levels later in the day?

**Steps 5-8: Predictive Modeling**
- **Forecasting Behavior:** Set up a regression model to predict a continuous metric (like a user's total active minutes or sleep duration for a given day) based on rolling averages of their telemetry from previous days.
- **A Focused Classifier:** While the dataset has 51 different context labels, trying to predict all of them at once will likely negatively impact your accuracy and make the project overly complicated. Instead, pick a focused subset. You could build a classifier to distinguish between 2 or 3 distinct states that interest you. Similarly pick features that are relevant, not everything.
- **Privacy-Safe Context Prediction:** Try predicting a specific user context (like commuting or studying) using *only* a restricted subset of "innocent" background sensors (e.g., battery drain and screen status), ignoring highly sensitive data like GPS and microphone features.

## A Few Tips

- **Don't crash your kernel:** If you try to merge and process all 60 users at the 1-minute interval level right away, pandas might hang. Start by building your pipeline on 5 to 10 users. Use `.resample('H')` or `.groupby()` to roll the 1-minute data up into hourly or daily summaries before you do any heavy processing.
- **Pick your sensors:** You don't get bonus points for throwing all 225 columns into a model. Pick a specific family of sensors (like just the motion sensors, or just the phone state variables) that makes sense for the narrative you are building.
- **NaNs are data too:** In mobile telemetry, missing data usually tells a story. If a phone stopped recording location or a user stopped answering surveys, think about *why* before you just use `.dropna()`.