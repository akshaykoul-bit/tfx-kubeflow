# News category classification using TFX pipeline

This is an end-to-end TFX pipeline which uses LocalDagRunner as the orchestrator which is TFX's own orchestrator

# Data and Objective
The dataset has been imported from the below Kaggle link:
https://www.kaggle.com/rmisra/news-category-dataset

The json data 'News_Category_Dataset_v2.json' can be downloaded from the above link and placed in 'downldata' folder in the working directory

TL;DR - I am trying to classify news articles using just the headlines in categories like CRIME, ENTERTAINMENT, SPORTS etc., more so, creating and end-to-end pipeline flow with TFX.

# Pipeline flow
The data is ingested using CSVExampleGen, which is then fed to StatisticsGen which learns some stats from the data, followed by SchemaGen which learns the schema and saves it in the metadata store which can later be used to validate new incoming data from prediction requests using ExampleValidator. 

The output from StatisticsGen is fed to the Transform component which does some preprocessing (standardization) on the data to make it ingestible for the Trainer component. I have used the standardization function (with some modifications) used in this kaggle workbook - https://www.kaggle.com/denniskreber/classification-with-bidirectional-lstm which is also the inspiration for the Bidirectional LSTM model that i have used in this project.

The tranformed output is fed to Trainer that trains the model using 2 BiDirectionalLSTM layers followed by Dropout and 2 Dense layers. The model accuracy is not that great ~ 52-53% which can be improved by introducing class weights and a more complex model using Tuner, but since the goal of this exercise is to demonstrate an end-to-end TFX pipeline, I haven't added the Tuner Component.

The trainer output is fed to the Pusher component which validates the baseline model with the new model or against the deployment targets/thresholds. For now, I haven't used the Evaluater component which also helps in validation for the latest blessed model.

Finally the pipeline is run using LocalDagRunner.
