# tfx-kubeflow

News category classification

This is an end-to-end TFX pipeline which uses Local Dag runner as the orchestrator which is TFX's in-built orchestrator

# Data
The dataset has been imported from the below Kaggle link:
https://www.kaggle.com/rmisra/news-category-dataset

TL;DR - I am trying to classify news articles using just the headlines in categories like CRIME, ENTERTAINMENT, SPORTS etc.

# Pipeline flow
The data is ingested using CSVExampleGen, followed by SchemaGen which learns the schema and saves it in the metadata store, which is then fed to StatisticGen which learns some stats from he data which can later be used to validate new incoming data from prediction requests. 

The output from StatisticsGen is fed to the Transform component which does some preprocessing (standardization) on the data to make it ingestible for the Trainer component. I have used the standardization function (with some modifications) used in this kaggle workbook - https://www.kaggle.com/denniskreber/classification-with-bidirectional-lstm which is also the inspiration for the Bidirectional LSTM model that i have used in this project.
