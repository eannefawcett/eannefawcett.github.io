---
layout: post
title:  "Adaptive Modeling: How to Take a One Time Project and Transform it for Production"
date:   2020-11-20 13:29:36
categories: technical, data science
paginator: Adaptive Modeling
---

First, let's define adaptive modeling. Adaptive modeling is something that happens when a model is trained on new data as it's collected. The goal is to essentially have real-time updates to the model as new, possibly different, and decision changing data comes in. This is a lot easier said than done however. In this post, I'd like to discuss a framework that can be used to create such a model.

# Time

The biggest decision for implementing an adaptive model is how often retraining should take place. This will look different for different industries. Annually, seasonally, monthly, biweekly, weekly, and daily timings for retraining all have different costs and benefits. The biggest thing to consider when choosing a time frame is the acceptable lag time between when data is collected and model deployment. It takes time to train a model. The amount of time that retraining will take is dependent on a few different things, computing power available and the structure of the model itself. Another consideration is if something goes wrong, if there's an unanticipated error that must be corrected for, before training can resume, additional time might be required. There are a few strategies that can be used to mitigate this risk.

# Parameters

The next decision that comes into play for adaptive modeling is as data is prepped for analysis. What are the parameters for inclusion or exclusion of data from the model? How important is it for every new piece of data to be included? Is it acceptable to drop any data points? Depending on how the data was scrubbed in the past, a framework for what can be expected from a dataset in terms of outliers can be developed. It's hard to specify exactly what good criteria might be because each dataset is different and has different tolerances for adjustment. A good rule of thumb is to exclude any data that is more than three standard deviations away from the mean for a particular feature. A few different approaches can be taken, the entire row can be dropped, or the outlier value can be replaced with the mean for that particular feature. That decision is going to be dependent on the goals for analysis.

Regardless of the approach taken, the cleaning and preparation of a dataset can be scripted, including the descriptive and inferential statistics run before modeling. Meaning, custom functions for each dataset can written, and often are during the initial modeling phase of analysis to assist with preprocessing. Lines in these custom functions can be set to raise flags, such as, two hundred of 3,000,000 data points were outliers for the month of October. If this is within the acceptable parameters for the dataset, then modeling should be allowed to continue. However, if it's not within acceptable limits, a data scientist might be needed to assess the data and determine what went wrong, if anything. Maybe there was an unexpected spike in the month of October that caused the outliers. In this case, it would be more advantageous to capture the outlier data. These acceptable limits might be determined with historical data if it's available. This addresses what can happen with each data point, and a technique can be used to address each feature.

# Functions as Friends

Custom functions are an absolute must in adaptive modeling. Cleaning of a dataset can be done quickly with a single function, most of the time with O(n) in Big O notation.

See below for an example of a custom cleaning function, raw dataset (and project) can be found [here][link1]:



```
def prep_data(data_frame, to_drop_list):
  """With raw dataframe and list of columns to drop, returns list of dataframes
     ready for arima analysis and zipcodes for associated dataframes."""
    import pandas as pd
    data_frames = []
    zip_codes = []
    for i in range(0, len(data_frame)):
        one_data_frame = pd.DataFrame()
        one_data_frame['Price'] = data_frame.iloc[i,:]
        print(str(i+1) + ' of ' + str(len(data_frame)) + ' parsed')
        zip_code = one_data_frame.loc['RegionName']
        one_data_frame = one_data_frame.drop(to_drop_list).astype('float64')
        one_data_frame.index = pd.to_datetime(one_data_frame.index)
        one_data_frame.plot(title=int(zip_code))
        data_frames.append(one_data_frame)
        zip_codes.append(zip_code)
    return data_frames, zip_codes
```



In this project, I used this function to prep five different counties for analysis, totaling 350 zip codes with ten years of housing data. This function also printed out overview graphs for each zip code, so I could scroll through them quickly and spot anything out of the ordinary.

In this project, I also did a variety of training on each zip code using functions, and was able to retain only the trained best model for each zip code using the following function:



```
def pyramid_best_model_output(data):
  """Using input data, this function will use a pyramid arima to find the best
     model, retrain based on that model, and store the best model parameters
     and history as the output."""
    from pyramid.arima import auto_arima
    from statsmodels.tsa.arima_model import ARIMA
    import numpy as np
    arima_best_models = []
    orders = []
    forecast_best_models = []
    predictions_best_models = []
    arima_best_model_summarys = []
    best_model_predictions = []
    plots = []
    output = pd.DataFrame()
    n = len(data)
    print(str(i+1) +  ' of pyramid arima')
    while True:
        try:
            model = auto_arima(np.asarray(data), trace=True, error_action='ignore', suppress_warnings=True,
                               seasonal=True, m=12, max_p=2, max_q=2, njobs=12, random_state=52, scoring='rmse')
            order = model.get_params()['order']
            orders.append(order)
            print(str(i+1) +  ' of arima using best params')
            arima_best_model = ARIMA(np.asarray(data), order=(order)).fit()
            arima_best_models.append(arima_best_model)
            print(str(i+1) +  ' of predictions')
            predictions_best_model = arima_best_model.predict()
            predictions_best_models.append(predictions_best_model)
            print(str(i+1) +  ' of forecasts')
            forecast_best_model = arima_best_model.forecast(steps=60)[0]
            forecast_best_models.append(forecast_best_model)
            print(str(i+1) +  ' of summaries')
            arima_best_model_summary = arima_best_model.summary()
            arima_best_model_summarys.append(arima_best_model_summary)
            output['arima'] = arima_best_models
            output['order'] = orders
            output['predictions'] = predictions_best_models
            output['forecast'] = forecast_best_models
            output['arima summary'] = arima_best_model_summarys
            break
        except ValueError:
            print(str(i+1) +  ' drop this data')
            break
    return output
```


 The function took a while to run, but I was able to get the best possible forecasting models for all 350 zip codes in less than twelve hours, without having to train every possible model.

# Notifications

As a data scientist, I use print statements to notify me of progress or flags when unwanted paths are taken by the functions I write. However, those same print statements could be configured to be sent as email to an individual or a team. Or each custom function could append it's own information to a list that gets sent out at specific points of the data science process, like at the end of preprocessing, or at the beginning of a training session for modeling. See more information about how to set up sending out an email, with plain text or html, [here][link2].

# Concluding Statements

Setting up an adaptive modeling pipeline can be daunting. However, after running through what is needed to set up preliminary modeling, a flow can be developed and appropriate parameters can be developed. Once these things are in place, code can be written to automate a lot of the processing and modeling work that needs to take place to realize an adaptive modeling pipeline. Not only is it possible using custom functions, but lines in those custom function can be set up to send pertinent information via email to necessary parties to begin triaging if necessary. It is entirely possible to develop overviews of what's happening in the preprocessing steps and get updates as models progress in their training. The only thing that really needs to be done is for someone to press start if an app is developed to handle the process, or a data scientist can develop a notebook using Amazon Web Service's SageMaker to accomplish the task. 

[link1]: https://github.com/eannefawcett/ARIMA-modeling-with-housing-prices/tree/master/data/raw
[link2]: https://realpython.com/python-send-email/
