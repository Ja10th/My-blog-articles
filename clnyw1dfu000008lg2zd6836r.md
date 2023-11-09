---
title: "Emotion Recognition System with Python"
seoTitle: "Emotion Recognition System with Python"
seoDescription: "Emotion recognition is the process of automatically inferring the emotional state of a person from their facial expressions, speech, or other behavioral cue"
datePublished: Fri Oct 20 2023 17:31:41 GMT+0000 (Coordinated Universal Time)
cuid: clnyw1dfu000008lg2zd6836r
slug: emotion-recognition-system-with-python
cover: https://cdn.hashnode.com/res/hashnode/image/upload/v1697822809570/e9b7e348-cb01-4e8e-884d-29f56ac94473.png
tags: python, deployment, machine-learning, python3, programming-tips

---

Emotion recognition is the process of automatically inferring the emotional state of a person from their facial expressions, speech, or other behavioral cues. It is a challenging task, but it has many potential applications in areas such as healthcare, customer service, and security.

In this article, we present a methodology for developing an emotion recognition system using audio dataset. The methodology consists of the following steps:

1. Data collection
    
2. Data preprocessing
    
3. Feature extraction
    
4. Model training
    
5. Model deployment
    

In the following sections, we will discuss each step of the methodology in more detail.

## **Data Collection**

The TESS dataset (Toronto Emotional Speech Set) was created by Kaggie in 2010. It is a female-only dataset of audio recordings of people speaking with different emotions. The dataset contains 2800 audio recordings of 2 actresses (aged 26 and 64 years) speaking in 7 different emotions: happiness, sadness, anger, fear, surprise, disgust, and neutral.

The TESS dataset is a good choice for emotion recognition because it is:

* Female-only: This is important because most other emotion recognition datasets are skewed towards male speakers. This can lead to overfitting, as the model will learn to recognize emotions based on the vocal patterns of male speakers.
    
* High quality audio: The audio recordings in the TESS dataset are of high quality, which makes it easier for the model to learn the features of the audio data.
    
* Evenly distributed across emotions: The audio recordings in the TESS dataset are evenly distributed across the 7 emotions. This is important for training a balanced model that can recognize all emotions with equal accuracy.
    

The TESS dataset is organized into two folders, one for each actress. Each folder contains the audio recordings for all 7 emotions. The audio recordings are in WAV format.

[![Emotion dataset](https://lh7-us.googleusercontent.com/b4Rlm8oYfWXRi6wxiK0-S3Q8rq6CD-SsqP5kr7hJ35SUvghqZ6PLbBH37StQrM2CpedyNS6h5SJX7zADhuuFepOBq_tZln9LsBQDV_AJ6-7ciavdwRa9YNErvSxuSWGSJmrMV6m3pF5SAp3QW3OQxQUuOoLT_PxD align="center")](https://www.kaggle.com/datasets/ejlok1/toronto-emotional-speech-set-tess.)

To collect the data, the following steps were done:

1. Downloaded the TESS dataset from the Kaggle website: [https://www.kaggle.com/datasets/ejlok1/toronto-emotional-speech-set-tess](https://www.kaggle.com/datasets/ejlok1/toronto-emotional-speech-set-tess).
    
2. Extracted the dataset files to a local directory.
    
3. Verified that the dataset contained the correct number of audio recordings and that they were all in WAV format.
    
4. Split the dataset into a training set and a test set. The training set contained 2400 audio recordings, and the test set contained 400 audio recordings.
    

## **Data Preprocessing**

After collecting the data, the next step is to preprocess it. This involves tasks such as:

1. **Loading the data into a Pandas DataFrame**. This will make it easier to work with the data and to visualize it.
    
2. **Checking the distribution of labels**. This will help to ensure that the dataset is balanced and that there are an equal number of audio recordings for each emotion.
    
3. **Removing any corrupted or incomplete audio recordings**. This will improve the quality of the dataset and make it easier for the model to learn the features of the audio data.
    
4. **Normalizing the audio levels**. This will ensure that all of the audio recordings have the same volume. This is important because the model will learn to recognize emotions based on the relative levels of different frequencies in the audio data.
    
5. **Segmenting the audio recordings**. This will break the audio recordings down into shorter clips. This is important because the model will only be able to learn the features of a short clip at a time.
    

Here is the code used to preprocess the data:

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697817624752/fc64c2e2-5c90-4ae1-bd47-2ca8693fe36d.png align="center")

`Importing Modules for the Project`

![](https://lh7-us.googleusercontent.com/UhIAAt9q5B8wjYiXXyFGnKJXPYvfAWr6hOjLFDAkRgMa-itvEISePGOdt6llbsBOTKAc_NVT84teICIOAnbZAYTupyF5u-CdhuRzbOlla4pf4UAtlqQxCkrx72oov0gYYzXHGVwnxh38c4QDwLilA726yGvO3hZ_ align="left")

`Loading our audio dataset and creating a data frame with it`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697817736660/030c33d4-e54a-4322-bb57-8816c1368089.png align="center")

`Showing the available audio in the data frame graphically`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697818111325/8b849e51-6438-4707-9499-4947ede517db.png align="center")

`Changes in the FEAR audio pitch is shown in the wave plot and spectrogram.`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697818682702/abb2a0d9-6a32-4b48-9877-3930e33fde30.png align="center")

![](https://lh7-us.googleusercontent.com/aLfO6WsjCBxgTA6rZ9xCZdZ5nWraAL-aPchKfTg3ob7mUNsDysoac0iTv9lNqE1V1DBupIk7bs6Df7KR-XKKJJAEdCNa7-KkvT7jb2Uc75i3_1FQ3p0Qax7r7SC3RWbW-1jwrgUFq0IB-CksS0BWN84Y1ABlkKpF align="left")

`Changes in the SAD audio pitch is shown in the wave plot and spectrogram.`

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697818919389/7c99fc92-fa6a-4300-b924-fbd8f6a1782a.png align="center")

![](https://lh7-us.googleusercontent.com/LSGwlMobvaSn4AZ2BTdX6EtQN_5czFRrQ_C2aUyU3nU9oGBxis9-MWIWmoyeR8ScwkXzgjmbuW5ugfa0_4nPa7Hs6hBcGu4MIVq1IS4jHNYDY8ePqcm1r54WklTWR-mUepWelPynaUs_TU0nG_4C-64_rjPe3lHA align="left")

### **Removing Corrupted or Incomplete Audio**

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1697819485103/798359e2-40c2-4749-8306-3c83eeb04ace.png align="center")

### **Normalizing the Audio**

![](https://lh7-us.googleusercontent.com/CqA0hiaZ9vT7aVSvWs0I-1otsvqIlaAOdfPrPc3s7eNfNoU3JZsteIwXILqxZZMcjc2uksME1Km5yAOY6__EeLooQUj4OWlldK02o5Q3sGsZ__mqoMZpnFPcPRd1SoipkklZvgF84ex0527_n1t3hkVRDqNErGSx align="left")

![](https://lh7-us.googleusercontent.com/oxFozxToYzcWASX15rJnmhk4fINyqnAFFRJtKkAxCr3mHv8CEanWUsltrYaG7hxHTTkEqx0fpMPtqKEIL9wr6A9IEVaorotCTGikPmpYb7-sx5oeRrEBOxNRJhjwWnLQY--JsQfo_FZtHpMVUiYie7Kyg-2YOMP8 align="left")

### **Segmentation of the Audio**

This code first loads the dataset into a Pandas DataFrame. Then, it checks the distribution of labels to ensure that the dataset is balanced. Any corrupted or incomplete audio recordings are removed. The audio levels are normalized to ensure that all of the audio recordings have the same volume. Finally, the audio recordings are segmented into shorter clips. This preprocessing step is important because it ensures that the data is clean and ready for modeling. It also helps to improve the accuracy of the model by making it easier for the model to learn the features of the audio data.

## **Feature Extraction**

After preprocessing the data, the next step is to extract features from the audio data. Mel-frequency cepstral coefficients (MFCCs) is used for feature extraction. MFCCs are a popular feature for emotion recognition. They are extracted by first converting the audio data to the frequency domain and then calculating the Mel-frequency spectrum. The Mel-frequency spectrum is a representation of the frequency spectrum that is more perceptually relevant to humans. The MFCCs are then calculated from the Mel-frequency spectrum.

The code below shows how it was done:

![](https://lh7-us.googleusercontent.com/ki2YuFYfElEV1jTD0AlrRk7o4Sc6fuMgUDFmgl1FH7ynjg3vn1uIQ6uqxt0FlAVVfI_hwBRYd_kQLjaS2S3DDTNNFr9-wxzvSNxDOJRDhQ9bH6Y8mFmuUdtyuZAqrMTBnqdcUt0R9hw7aTHU94CI-aJKKpHfDDgl align="left")

This code first loads the dataset into a Pandas DataFrame. Then, it extracts MFCCs features from the audio data. This feature extraction step is important because it converts the audio data into a format that can be used by the model. It also helps to improve the accuracy of the model by extracting features that are relevant to emotion recognition. Converting it to a format acceptable by our LSTM model code is below:

![](https://lh7-us.googleusercontent.com/EmE6vhQ8gU7RcHRVXf1NViyHTbOCvbZiWyTDffpRoxa6kGrc_oCIdLZiCu8EWfv5Gno9J1hADqz1bvEkav0ZFN-qTz3GvDStwkMPsw0_VbHJ2uKUNqPGXRfA43j2ShoixEP28KtpvvVQUI-PArLPP-sfnHg1ZfFv align="left")

## **Model Training**

After extracting features from the audio data, the next step is to train a model to recognize emotions. This can be done using a deep learning neural network, such as an LSTM (Long Short Time Memory) model.

An LSTM model is a type of recurrent neural network that is well-suited for tasks that involve sequential data, such as audio data. LSTM models can learn long-term dependencies in the data, which is important for emotion recognition.

The LSTM model created has the following architecture:

* An LSTM layer with 123 units
    
* A Dense layer with 64 units
    
* A Dropout layer with a rate of 0.2
    
* A Dense layer with 32 units
    
* A Dropout layer with a rate of 0.2
    
* A Dense layer with 7 units, corresponding to the 7 emotions in the dataset
    

The model is compiled with the following settings:

* Loss function: categorical\_crossentropy
    
* Optimizer: adam
    
* Metrics: accuracy
    

The model is then trained on the training set for a specified number of epochs. The model is evaluated on the test set after each epoch to monitor the progress of training.

The model can be further improved by increasing the number of epochs, the number of units in the LSTM layer, or the number of layers in the model.

Here is the code used to train the LSTM model:

![](https://lh7-us.googleusercontent.com/Tps0pLBLyGKED6JVf9AcPH9uM09-or3FTcszLpnXd9lI9bnpD6yypKv-qhwKSLx8ml87vbOtLq9wVokhWZgkFRAIWQT-VS7RP__kgDNY3PoAMX3W7yfZcA_KpVaX7FDTyj6P_VyQvhXaOciXQVy8a6QYtY1eICR2 align="left")

`This is the process taken to train the model for the code above`

![](https://lh7-us.googleusercontent.com/ocNahHc0eZ9BbvRBFsQwUJUs6dG0uHlhy3GPtrU9SorH2yiPQ-fWi6iBp3X65bS69UGYKUDlnkB5EewBDOYSwYvzYxz-SbDwchduxLERQCWB2MwjMY2udYMguSAawrlIs4JNiUAXOVoVIVKrwh85R4gjZsqnTUBF align="left")

This code first creates the LSTM model with the specified architecture. The model is then compiled with the specified settings. The model is then trained on the training set for 100 epochs. The model is evaluated on the test set after each epoch. The history of the training process is printed to the console. The output of the code shows that the model achieved an accuracy of 90% on the training set. This is a good result, but the model can be further improved by training the model for more epochs or by using a different architecture.

## **Model Deployment**

Making the model available to the public through a web application. Here are the steps on how to deploy the LSTM model as a web app:

1. Create a web app framework with Flask
    
2. Load the model into the web app.
    
3. Create a route in the web app that accepts an audio file as input and returns the predicted emotion.
    

Once the model is deployed, it can be accessed by users through the web app. Users can upload an audio file to the web app, and the model will predict the emotion in the audio file.

![](https://lh7-us.googleusercontent.com/rZyyb1jqjAwcQVtySBmIfzobKBQYUaWQa887eHJ__X6sCgWeYOemliiRXUG1a7I6oC-ArlTWxCp_M9xNSbMWV3efMkjB-w1c29aGGWQ8d6hMzcXr3QcZzCJPdKx4CF5Z9B-yo3i6OI4I082d1iTY_ejDpPZ_JI6n align="left")

![](https://lh7-us.googleusercontent.com/Ktu0fq_egSPmfklFG2q4Y0KyRhLIwlZprX_NSkqIFu7V8NfXcXooyoB3vag7SFw6C__CjfZCxleq3IPwmgvNatzFlRj5ln31jYEfxJtyNBZZgqa40Z0ab_EUDm4dzo_U7y0ErWZPM8ALlFtI_0v3kN6WJQOS5sNR align="left")

After uploading the voice recordings, we can use it for various applications such as psychology analysis, for customer feedback and more.