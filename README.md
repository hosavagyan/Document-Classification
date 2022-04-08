### Document-Classification on the RVL-CDIP Dataset

This repo contains Jupyter notebooks and Serving code for inference for a few models developed for Document-Classification on the RVL-CDIP Dataset

![RVL-CDIP Dataset](https://user-images.githubusercontent.com/57097596/162274132-8ca1ad4c-f7ec-4bcd-a374-dddc888fff9d.jpg)

The following models were developed:

|     Model Description     | Validation Accuracy |            Model size      | # Of Epochs |
| --------------------------|:-------------------:|---------------------------:|------------:|
|VGG with changed classifier|         87.8%       |     ~138 million params    |      12     |
|      VGG16 + Fasttext     |         92.27%      |     ~138 million params    |      21     |
|         Layout_MV2        |         80%         |     ~200 million params    |     1/3     |
|      OCR with NLP - Countvectorizer with bigrams + logistic regression |  79.6% | - | - |
| OCR with NLP -Fasttext with charngrams 5,7 | 73.5% |               -         |      7      | 

## Building and running the docker image

Building:
```
sudo docker build -t document_classification .
```
Running:
```
sudo docker run --rm -p 5000:5000 -v Weights:/app/Weights --name doc_classification document_classification
```

## Running apache benchmarking on the server
Create a sample request.json file:
```
cd client
python create_json_request.py sample_image.jpg
```

Run apache benchmark
```
ab -k -t 60 -c 2 -T 'application/json' -p request.json  http://0.0.0.0:5000/predict
```

## Starting server without docker
```
gunicorn app:app --bind 0.0.0.0:5000 --workers 1
```

## Sending an image for inference from client
```
python client.py sample_image.jpg
```

## The Team

Hovsep Avagyan - hovsep.avagyan.2016@gmail.com  
Arman Deghoyan - armani.deghoyan@gmail.com  
Martun Karapetyan - martun.karapetyan@gmail.com  

