# watson-vr-node
Visual Recognition Web application using IBM Watson Visual Recognition
This apps is identify whether your mas properly have on your face.

## 1. preparation
### 1. Login to IBM Cloud account (Lite accout is OK)
Please register if you don't have account [here](https://cloud.ibm.com/registration?cm_mmc=Email_Events-_-Developer_Innovation-_-WW_WW-_-nishito\tokyo\japan&cm_mmca1=000019RS&cm_mmca2=10004805&cm_mmca3=M99938765&cvosrc=email.Events.M99938765&cvo_campaign=000019RS
)

prepare 20 picture, 10 put on mask properly, 10 put mask not properly.



### 2. Install IBM Cloud CLI
### 2-1)  
https://cloud.ibm.com/docs/cli/reference/ibmcloud?topic=cloud-cli-install-ibmcloud-cli#install_use 


### 2-2)  Make sure the CLI was installed.
```
$ ibmcloud --version
```

ex of putput)
```
ibmcloud version 0.7.1+8a6d40e-2018-06-07T07:13:39+00:00
```

### 2-3) Login to IBM cloud using CLI
```
$ ibmcloud login -r us-south
```

ex)
```
API endpoint:       https://api.ng.bluemix.net
Region:                  us-south
User:                      XXXXXX@hoge.com
Account:                XXXXX's Account (xxxxxxxxxxxxxxxxxxxxx)
Resource group:    default
CF API endpoint:   https://api.ng.bluemix.net (API version: 2.92.0)
Org:                        XXXXXX@hoge.com
Space:                    dev
OK
```



## 2. Create Visual Recognition service
If you already create the service , please start at 5 below. 

1. https://cloud.ibm.com/login to login

2. Click Catalog

3. Type `Visual Recognition` in search and find it. 

4. Click `Create`

5. Click `Launch Watson Studio" and start creating custom model

6. On Watson studio, click "Create Model+" on Classify Images

7. Please reffer to this document https://cloud.ibm.com/docs/visual-recognition?topic=visual-recognition-tutorial-custom-classifier
And create 2 class, 1, Mask OK 2 Mask NG

![Model](https://github.com/osonoi/watson-vr-node/blob/master/images/maskgit1.png)

8. Click "Train Model" to train.

9. After Training click on Associated Service name and find classifier ID and momorize it.


## 3. Clone the application to your PC, mac
```
git clone https://github.com/osonoi/watson-vr-node.git
```
```
cd watson-vr-node
```

## 4. Chenge these items and deploy to IBM cloud.
### 1. Edit `manifest.yml`
#### 1-1) line 3　<Set Your Application Name>
Change to your apps name. This should be unique in the all IBM cloud apps.
<br/>
ex): 
```
- name: myid0701-watson-vr
````

#### 1-2) line 8　<Set Your CLASSIFIER_ID>
Input Visual Recognition, classifier ID.

env:
    CLASSIFIER_ID: DefaultCustomModel_1941703287
````

example:
```
---
applications:
- name: myid-watson-vr
  buildpacks:
    - nodejs_buildpack
  command: node -max_old_space_size=2048 app.js
  env:
    CLASSIFIER_ID: food
  memory: 256M
```

### 2. Login to IBM Cloud
```
$ ibmcloud login -r us-south
```
```
ibmcloud target --cf
```
### 3. Upload App to IBM Cloud
```
ibmcloud cf push --no-start
```

## 5. Connect Visual Recognition to Apps

1. Back to IBM cloud portal https://cloud.ibm.com

2. Display resource

3. Clck `Cloud Foundry Apps`

4. Click apps you created.

5. Click "Connect"

6. Click `Create connection`

7. Find `Visual Recognition` and connect

8. Click 'Connect'

9. Select Action and click 'start'

## 6. Launch Apps
1. Click `Visit App URL


![Model](https://github.com/osonoi/watson-vr-node/blob/master/images/maskgit1.png)


![mask](https://github.com/osonoi/watson-vr-node/images/maskgit1.png)

2.　Apps on Smartphone.
 There is a QR code in the bottom of the apps menu. Take that with yiur smart phone. That bring you smartphone apps.
 
# In the case of Docker
$ git clone https://github.com/osonoi/watson-vr-node.git
$ cd watson-vr-node/

Create Docker image
$ docker build -t watson-vr-node .

Launch app on local dockerDocker
docker run -d -p 3000:3000 --env-file=./ibm-credentials.env --env CLASSIFIER_ID=DefaultCustomModel_1536117779 watson-vr-node


