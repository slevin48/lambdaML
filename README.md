# Lambda ML

Deploy a machine learning model as a serverless AWS lambda function:
https://towardsdatascience.com/how-to-deploy-a-machine-learning-model-on-aws-lambda-24c36dcaed20

Train the model with Scikit-learn on the textbook iris dataset:
https://scikit-learn.org/stable/modules/model_persistence.html

Save the ML model as a pickle file:
https://realpython.com/python-pickle-module/
(Read this article on How to persist objects in Python)


## sklearnflask 
Example with the Titanic dataset 
https://towardsdatascience.com/a-flask-api-for-serving-scikit-learn-models-c8bcdaa41daa

https://github.com/amirziai/sklearnflask

```bash
#!/bin/bash
#
# Starting API
python2 main.py 9999 &
sleep 2
#
# POST method predict
curl -d '[
    {"Age": 85, "Sex": "male", "Embarked": "S"},
    {"Age": 24, "Sex": "female", "Embarked": "C"},
    {"Age": 3, "Sex": "male", "Embarked": "C"},
    {"Age": 21, "Sex": "male", "Embarked": "S"}
]' -H "Content-Type: application/json" \
     -X POST http://localhost:9999/predict && \
    echo -e "\n -> predict OK"

# GET method wipe
curl -X GET http://localhost:9999/wipe && \
    echo -e "\n -> wipe OK"

# GET method train
curl -X GET http://localhost:9999/train && \
    echo -e "\n -> train OK"

# kill runing API
for i in $(ps -elf | grep "python2 main.py 9999" | grep -v grep | cut -d " " -f 4); do
    kill -9 $i
done
```

same request in Python

```python
import requests as rq
payload = [{"Age": 85, "Sex": "male", "Embarked": "S"},{"Age": 24, "Sex": "female", "Embarked": "C"},{"Age": 3, "Sex": "male", "Embarked": "C"},{"Age": 21, "Sex": "male", "Embarked": "S"}]
rq.post("http://localhost:8080/predict",data = payload)
```