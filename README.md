# mlzoomcamp_kubernetes

saved_model_cli show --dir clothing-model --all

### look for signature definition
signature_def['serving_default']:
  The given SavedModel SignatureDef contains the following input(s):
    inputs['input_8'] tensor_info:
        dtype: DT_FLOAT
        shape: (-1, 299, 299, 3)
        name: serving_default_input_8:0
  The given SavedModel SignatureDef contains the following output(s):
    outputs['dense_7'] tensor_info:
        dtype: DT_FLOAT
        shape: (-1, 10)
        name: StatefulPartitionedCall:0
  Method name is: tensorflow/serving/predict

  ### docker
  docker run -it --rm -p 8500:8500 -v "$(pwd)/clothing-model:/models/clothing-model/1" -e MODEL_NAME="clothing-model" tensorflow/serving:2.7.0


pip install grpcio==1.42 tensorflow-serving-api==2.7.0

pip install pipenv
pipenv install grpcio==1.42.0 flask keras-image-helper gunicorn

pipenv install tensorflow-protobuf==2.7.0
pipenv install protobuf=3.20.3


docker run -it --rm -p 8500:8500 -v $(pwd)/clothing-model:/models/clothing-model/1 -e MODEL_NAME="clothing-model" tensorflow/serving:2.7.0

docker build -t zoomcamp-10-model:xception-v4-001 -f image-model.dockerfile .

## model docker
docker run -it --rm \
  -p 8500:8500 \
  zoomcamp-10-model:xception-v4-001

## gateway docker
docker run -it --rm \
  -p 9696:9696 \
  zoomcamp-10-gateway:001

pipenv run python gateway.py

docker build -t zoomcamp-10-gateway:001 -f image-gateway.dockerfile .

