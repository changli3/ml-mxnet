# ml-mxnet
I wanted a step to step evaluation guide to quickly grapes basic concepts of deep learning and have an understanding of the requirements of optimize and scale up the underline infrastructure. I could not find one so I have to start one. 
Here’s my planed topics:
## Topics
* [Simple MXNet](./README.md) - Basic server usage on prebuilt MXNet models.
* [Simple TensorFlow](../ml-tensorflow/README.md) - Basic server usage on prebuilt Tensorflow models.
* [Distributed TensorFlow](../ml-tensorflow-distributed/README.md) – Distributed Tensorflow training and serving
## Simple MXNet Steps
### Step 1. Lauch AWS VM with template file [cf.json](./cf.json)
You can use the AWS console, or use AWS CLI like below (remember to download the tempalte file to your computer and change parameters to proper values) -
```
aws cloudformation deploy --template-file cf.json --stack-name test-ml --parameter-overrides InstanceSubnet=subnet-2b976000 InstanceSecurityGroup=sg-58e1fc3d KeyPairName=TreaEBSLab --tags Name=DLVM
```
### Step 2. SSH to the VM
Once the CF template completed, SSH to it with username "ubuntu" and the key used to launch the template.
### Step 3. Activate MXNet 
Run the following command -
```
source activate mxnet_p36
```
### Step 4. Start servers
Run the following commands -
```
cd ml-mxnet
./start-servers
```
Need to wait about five minutes the first you start the servers.
### Step 5. Test with provide image files
Now open another another SSH terminal to the VM, run the following commands to test - 
```
cd ~/ml-mxnet
./predict kitten.jpg
```
You can see the output predictions from different models. And run it for the airplane.jpg:
```
./predict airplane.jpg
```
### Step 6. Test any picture from online 
Google to find an object picture to test, for examples: https://st2.indiarailinfo.com/kjfdsuiemjvcya5/0/1978394/0/img60454972968.jpg. Test with this command -
```
./get-predict https://st2.indiarailinfo.com/kjfdsuiemjvcya5/0/1978394/0/img60454972968.jpg
```
### Step 7. Terninate the CF Stack after Test
```
aws cloudformation delete-stack --stack-name test-ml
```

