# LAYER AWS SAM TEMPLATE PYTHON

## 1.Generation All the necesary

After downloaded the repo and add all the names of the libraries into the requirements.txt with the format example:
```
numpy
pandas
```
Into the template.yaml you need to define the layer , you can see the structure of a lambda into:
```
{https://docs.aws.amazon.com/serverless-application-model/latest/developerguide/sam-resource-layerversion.html#sam-layerversion-compatibleruntimes}
```
and you can see the list of avaible supported lenguaje for create a layer:
```
{https://docs.aws.amazon.com/lambda/latest/dg/API_ListLayers.html}
```

We need to create the folder with theese requirements instalations.

### 1.1 Generation of requirements instalation folder

Exec the next command to create the folder with all the requirements that our lambda needs
```
pip install -r requirements.txt -t ./python/
```
This command add all the instalation files to the folder "python/" , the folder have to be designed python if we want to work in aws

## 2. SAM Layer Package

To upload the layer in aws, we need to create a package that embeed the folder view in the las step.

### 2.1 SAM output package template

To package the project layer needs to run:
```
sam package --template-file template.yaml --output-template-file packaged-template.yaml --s3-bucket wecruitio-lambda
```
Where the template.yaml is the name of the confi .yaml where is define my layer and the packaged-template.yaml is the name of the output file that we will use in next steps and wecruitio-lambda is the name of the s3 bucket where the package be save.

## 3 SAM DEPLOY LAYER

After packaged the layer output template we are able to deploy our layer to aws (Deploy in AWS needs the aws configuration and credentials of the account where you want to deploy, tutorial of it click here)

### 3.1 SAM Package output deploy

To deploy the output package that we do in 2.1 in AWS we need to exec the following command:
```
sam deploy --template-file packaged-template.yaml --stack-name LayerPythonBase --capabilities CAPABILITY_IAM
```
where package-template.yaml is the output file that we put into the command in 2.1, stack-name is the name assign to the package into aws and if we need to add capabilities put together of it.
