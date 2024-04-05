# Fake News Project 

## Introduction
This repository contains the code used in data processing, modelling and evaluation of our Fake News Predictor. We have collected all of our final code in the Jupyter notebook file "Fake News Project.ipynb". This is the file, that the below instructions are meant to help reproduce. In addition, we have included files that contain code in which we have experimented with alternative techniques for data processing and modelling. The results from these files can be reproduced, but this README does not detail how this is done.  Below, you'll find instructions on how to set up your environment, run the code for the final code used to generate the results presented in our report available in "Fake News Project.ipynb".

## Installation
To ensure compatibility and manage dependencies, we recommend creating a virtual environment for this project. After cloning the repository, navigate to the project directory and follow these steps:

1. Create a virtual environment. We suggest using conda:
    ```
    conda create -n "gds_environment" python=3.11.5
    ```

2. Activate the virtual environment:
        ```
        conda activate gds_environment
        ```
   
3. Install the required dependencies:
    ```
    pip install -r requirements.txt
    ```

## Data Preparation
Place the file `995,000_rows.csv` in the same folder as the code file. This dataset contains the articles that will be used for training and testing the model and can be downloaded from Canvas

## Usage
It is a computationally heavy task to clean and pre-process the entire 995k row dataset, so it is highly beneficial to only do this once. If you wish to run the code more than once we suggest to save the cleaned dataset to a file that can then be re-read much faster. In order to vary between running the code the first time and all others we have a few lines that need to be commented our and uncommented again. Before running the code for the first time, please follow these steps:

1. Run the following block to clean, process, and save the entire corpus ONLY the first time you run the code. Note that this step might take approximately 30-40 minutes to complete:
    ```python
    # Clean, process, and analyze entire corpus
    numbers, urls, dates, top_100_words, top_1000_dic, top_100_words_v2, top_1000_dic_v2 = clean_and_analyze(dataframe_v03)
    dataframe_v03.to_csv('full_dataframe')
    dataframe_v04 = dataframe_v03.copy()
    print(f"The number of numbers, URLs, and dates are: numbers: {numbers}, URLs: {urls}, and dates: {dates}") # Uncomment when running the first time
    print("The top 100 most frequent words before removals are") # Comment out after running the first time
    print(f"{top_100_words}") #Comment out after running the first time
    print("The top 100 most frequent words after removals are") #Comment out after running the first time
    print(f"{top_100_words_v2}") # Comment out after running the first time
    ```

2. Additionally, run the following line to apply further processing to the content column. Again ONLY during the first run:
    ```python
    dataframe_v04['content'] = dataframe_v04['content'].apply(lambda x: ' '.join(x)) # Uncomment only when running the first time
    ```

3. After the initial run, comment out the above blocks to prevent redundant processing. Instead, uncomment and use the following block to load the cleaned data from a saved file:
    ```python
    # Download cleaned data to avoid running cleaning and processing on the entire dataset again
    # dataframe_v04 = pd.read_csv('full_dataframe') # Uncomment and use as dataframe when the run has already run one time.
    ```

Once these steps are completed, you can run the code in a Jupyter notebook to reproduce our results.
