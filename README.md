# Build-a-ML-Workflow-For-Scones-Unlimited-On-Amazon-SageMaker

In this project, I created 3 Lambda functions to form a prediction pipeline using a Step Function.

The Lambda functions can be found in the Lambda.py file included in this repository. 

Here is an overview of what task each Lambda function performed:

#Lambda function 1: 
Serialize the bytecode image data from the CIFAR image dataset by converting it to a Base64 encoding. 

#Lambda function 2: 
Run an inference via a SageMaker Endpoint using the model trained on some of the data from CIFAR. 
NOTE: I was unable to successfully upload a zip containing the SageMaker SDK, so I instead used the SageMaker runtime via Boto3 to invoke the endpoint. 

#Lambda function 3: 
Test the image inference probability against a predefined threshold. Results that exceed this threshold are returned, while results that do not are not returned and an error is raised. 

#Stretch Goal

Of the suggested stretch goals, I chose to explore no. 2:
Modify your event driven workflow: can you rewrite your Lambda functions so that the workflow can process multiple image inputs in parallel? Can the Step Function "fan out" to accommodate this new workflow?

I added a Map State to the workflow, which takes an array of JSON inputs and processes them in parallel. No modifications to the Lambda functions were required for this. 

Here is the array I used to successfully test the Map State. 

[
  {"image_data": "", "s3_bucket": "sagemaker-us-east-1-126817106120", "s3_key": "test/motorcycle_s_001960.png"},
  
  {"image_data": "", "s3_bucket": "sagemaker-us-east-1-126817106120", "s3_key": "test/minibike_s_002051.png"},
  
  {"image_data": "", "s3_bucket": "sagemaker-us-east-1-126817106120", "s3_key": "test/motorcycle_s_000141.png"}
]

The workflow and successful output can be seen in the images in this repository. 
