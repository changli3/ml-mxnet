# ml-mxnet
I wanted to find step to step evaluation labs to quickly grapes basic concepts of deep learning, so I can answer some basic questions like -
How do I pick a framework and coin a model from a real world problem?
How fast is the training process, how do I scale the training?
How fast is the training process, how do I scale the training? How to optimize it on stream data like stock price and log data stream?
What is the difference and comparison between deep learning on cluster and deep learning on Hadoop/Spark? 

With all these in mind, I want to start a series of labs. I will mainly look into two frameworks: MxNet and TensorFlow. This one is to understand how to serve once a model is built and trained. After this lab, I would say that it appears to me quite easy to scale the model serving.

## Simple MxNet Server Lab
### Step 1. Lauch AWS VM
I have an AWS CF template file [cf.json](./cf.json) here. You can launch it in the AWS console, or use AWS CLI like below. Remember to download the tempalte file to your computer and change parameters to proper values -
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
You need to wait about five minutes the first you start the servers.
### Step 5. Test with provided images
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

### Step 7. Use Postman to Test

You can use Postman to test the services as this:
![Postman Screen](https://raw.githubusercontent.com/changli3/ml-mxnet/master/postman.JPG "Postman Screen")

```
#SqueezeNet
curl -X POST http://PRIVATE-IP:8081/squeezenet/predict -F "data=@image-file"

#SSD
curl -X POST http://PRIVATE-IP:8082/ssd/predict -F "data=@image-file"

#CaffeNet
curl -X POST http://PRIVATE-IP:8083/caffenet/predict -F "data=@image-file"

#AlexNet
curl -X POST http://PRIVATE-IP:8084/alexnet/predict -F "input_0=@image-file"

#Inception V3
curl -X POST http://PRIVATE-IP:8085/inception/predict -F "data=@image-file"
```

### Step 8. Terminate the CF Stack after Test
```
aws cloudformation delete-stack --stack-name test-ml
```

## Watch Video Instruction
[![Video Instructuion](https://img.youtube.com/vi/MtquftUwW9Q/0.jpg)](https://youtu.be/MtquftUwW9Q "Video Instruction")


