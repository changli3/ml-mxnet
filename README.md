# ml-mxnet
I wanted a step to step evaluation guide to quickly grapes basic concepts of deep learning and have an understanding of the requirements of optimize and scale up the underline infrastructure. I could not find one so I have to start one. 
Here’s my planed topics:
## Topics
* [Simple MXNet](./README.md) - Basic server usage on prebuilt MXNet models.
* [Simple TensorFlow](../ml-tensorflow/README.md) - Basic server usage on prebuilt Tensorflow models.
* [Distributed TensorFlow](../ml-tensorflow-distributed/README.md) – Distributed Tensorflow training and serving
## Simple MXNet Steps
### Step 1. Lauch AWS VM with [template file](./cf.json)
you can use the AWS console, or AWS CLI like this (remember to download the tempalte file and change parameters to proper values) -
```
aws cloudformation deploy --template-file cf.json --stack-name test-ml --parameter-overrides InstanceSubnet=subnet-2b976000 InstanceSecurityGroup=sg-58e1fc3d KeyPairName=TreaEBSLab --tags Name=DLVM
```
### Step 2. SSH to the VM once the template completed (with username "ubuntu" and the key used to launch the template)
### Step 3. Activate MXNet with python 3 with the following command
```
source activate mxnet_p36
```
### Step 4. Start servers
```
cd ml-mxnet
./start-servers
```
Need to wait about five minutes the first you start the servers.
### Step 5. Open another SSH to the VM
### Step 6. Test with provide image files 
```
cd ~/ml-mxnet
./predict kitten.jpg
```
You can see the predictions from different models. And run it for the airplane:
```
./predict airplane.jpg
```
### Step 7. Google to find and test any picture from online 
Test, for examples: https://st2.indiarailinfo.com/kjfdsuiemjvcya5/0/1978394/0/img60454972968.jpg, run this command -
```
./get-predict https://st2.indiarailinfo.com/kjfdsuiemjvcya5/0/1978394/0/img60454972968.jpg
```
### Step 8. Terninate the CloudFormation stack
```
aws cloudformation delete-stack --stack-name test-ml
```
