# ml-mxnet
I wanted to find step to step evaluation labs to quickly grapes basic concepts of deep learning, so I can answer some basic questions like -
### How do I pick a framework and coin a model from a real world problem?
### How fast is the training process, how do I scale the training?
### How fast is the training process, how do I scale the training? How to optimize it on stream data like stock price and log data stream?
### What is the difference and comparison between deep learning on cluster and deep learning on Hadoop/Spark? 

With all these in mind, I want to start a series of labs. I will mainly look into two frameworks: MxNet and TensorFlow. This one is to understand how to serve once a model is built and trained. After this lab, I would say that it appears to me quite easy to scale the model serving.

## Simple MxNet Server Lab
### Step 1. Lauch AWS VM with template file [cf.json](./cf.json)
You can use the AWS console, or use AWS CLI like below (remember to download the tempalte file to your computer and change parameters to proper values) -
```
aws cloudformation deploy --template-file cf.json --stack-name test-ml --parameter-overrides InstanceSubnet=subnet-2b976000 InstanceSecurityGroup=sg-58e1fc3d KeyPairName=TreaEBSLab
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

