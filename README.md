

# SAM Service

SAM Service is a Python-based web service that utilizes FastAPI and Uvicorn to create a fast and efficient API for retrieving a Segment Anything model. It also uses Nginx as a reverse proxy for handling requests and improving performance. SAM stands for "Segment Anything Model," and the service is designed to make it easy for developers to generate an embedded image model for use with an ONNX runtime.

## Getting Started

To get started with SAM Service, follow these steps:

1. Clone the repository: 
```
git clone git@github.com:JaneliaSciComp/SAM_service.git
```
2. copy the model checkpoint file to the sam_service directory

 - It can be downloaded from https://github.com/facebookresearch/segment-anything#model-checkpoints
 - You want the sam_vit_h_4b8939.pth checkpoint.
  
```
cp sam_vit_h_4b8939.pth SAM_service/sam_service
```

3. Clone the paintera-sam repo alongside this one
```
git clone git@github.com:cmhulbert/paintera-sam.git
```

4. Update the PYTHONPATH
```
export PYTHONPATH=/opt/sam_service/paintera-sam/:$PYTHONPATH
```

5. Install the necessary packages using conda: 
```
conda env create -f environment.yml
conda activate segment_anything
```
6. Start the API: 
```
uvicorn sam_fast_api:app --access-log --workers 8 --forwarded-allow-ips='*' --proxy-headers --uds /tmp/uvicorn.sock
```
7. Configure the nginx virtual host with the file found in `nginx.conf`
8. connect to the service in your browser: `http://your-service.com/`

## API Endpoints

SAM Service includes a number of pre-built endpoints that you can use right out of the box. These endpoints include:

- `/embedded_model`: This endpoint will take an image and return an embedded segment anything model for use in an ONNX runtime. 
- `/from_model`: Returns a mask for the provided model and point.
- `/prediction`: When you want just a mask to show the segmented area around a point in an image, use this. 

## Documentation
Documentation for the endpoints is provided by the service and can be found at the `/docs` or `/redoc` urls.

## Configuration

SAM Service can be configured by modifying the `config.json` file. This file includes settings for available GPUS and log levels.

## Contributing

If you would like to contribute to SAM Service, feel free to open a pull request. Before doing so, please ensure that your code adheres to the PEP 8 style guide and that all tests pass.

## License

SAM Service is released under the Janelia Open-Source Software License. See `LICENSE` for more information.
