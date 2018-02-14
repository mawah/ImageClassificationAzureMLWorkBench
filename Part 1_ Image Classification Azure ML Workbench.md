## Part 1: Image Classification Using Azure ML Workbench

### Getting Started

#### Install Azure ML Workbench

From the  following guide https://docs.microsoft.com/en-us/azure/machine-learning/preview/quickstart-installation  follow the first two steps which are listed below:

1.	Create Azure Machine Learning accounts – In this step uncheck ‘create model management account’ the model management account will be created later in the tutorial

2.	Install Azure Machine Learning Workbench on Windows.

#### Install Python libraries

Open Azure ML Workbench, then from the menu select File > Open Command prompt, this will open the Azure CLI window. Enter the following commands to install the required python libraries:
*	pip install https://cntk.ai/PythonWheel/GPU/cntk-2.3.1-cp35-cp35m-win_amd64.whl
*	conda install pillow
*	pip install -U numpy
* 	pip install configparser


### Create a new project in Azure ML Workbench

1.	Click on File > New Project

2.	Enter the project details

Example:<br/>
<b>Project Name:</b> ImageClassificationProject<br/>
<b>Project Directory:</b> Default <br/>
<b>Workspace:</b> (Select workspace created during the Installation step) <br/>
<b>Project Template:</b> Select a blank template <br/>

### Generate The Model

1.  Download the Image Classification project from 
    https://github.com/akegramener/ImgClassifierMLWrkbench-ClassifierCode 
    Copy all the files from the github project to the new project folder that was created in Azure ML Workbench (Refer to the image below to locate the project folder). For an explanation of the       code please refer to tutorial [Enter tutorial details for the INAT tutorial]. 
<p align="center"><img src="/Images/Azure-ML-Workbench-Project-Direc.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Project-Direc.jpg" width="80%" height="80%" /><p>

2. Open the project directory (Directory location as shown in the image above). Locate the file 'Config.ini'. Change the 'PATH' variable to a location that you prefer, currently the path points to c:\azure_ml_outputs, if you prefer a different location change the path variable to the desired location

3.  In Azure ML Workbench window choose the first code file 'create_directories.py'. This will create an output folder directory on         your machine in the location provided and create an environment variable for the folder.
    Enter the location for the output directory in the 'arguments' field, as show in the screenshot below. Click 'Run'
         
<p align="center"><img src="/Images/Azure-ML-Workbench-Create-Directories-Code.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Create-Directories-Code.jpg" width="80%" height="80%"/><p>
 
4.	Open the folder created in step 2, Inside this folder, locate a folder called 'data' Download and extract the image files from 					https://storage.googleapis.com/us_inat_data/train_val/train_val_images_mini.tar.gz  
		to the data folder as shown in the image below
<p align="center"><img src="/Images/Azure-ML-Workbench-Outputs-Data.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Outputs-Data.jpg" width="60%" height="60%" /><p>

5.  In azure ml workbench select code file 'structure_data.py' and click ‘Run
    After the code has finished running you should see two folders 'train' and 'validation' in the data
    Folder

<p align="center"><img src="/Images/Azure-ML-Workbench-Train-Validation-Folders.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Train-Validation-Folders.jpg" width="80%" height="80%" /><p>
  
Open the train / validation folders, the folders should contain additional folders with image files as shown in the screen shots below

<p align="center"><img src="/Images/Azure-ML-Workbench-Outputs-Folders.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Outputs-Folders.jpg" width="70%" height="70%"/><p>

<p align="center"><img src="/Images/Azure-ML-Workbench-Outputs-Data-Train-Folder.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Outputs-Data-Train-Folder.jpg" width="70%" height="70%"/><p>
	
6.	Next select the code file 'create_map_files.py' in azure ml workbench and click ‘Run’. Once the code has finished running, check the metadata folder in the azure_ml_outputs folder. You should see the files as shown in the screenshot below

<p align="center"><img src="/Images/Azure-ML-Workbench-Outputs-Metadata-Folder.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Outputs-Metadata-Folder.jpg" width="70%" height="70%"/><p>
 
7.	Next select the code file download_model.py' and click 'Run'. This code will download the 'ResNet34 ImageNet CNTK model from https://www.cntk.ai/Models/CNTK_Pretrained/ResNet34_ImageNet_CNTK.model, 
which will be used for transfer learning in the next step. After the script has finished running, go to the folder …/azure_ml_outputs/model ensure that the ResNet34 ImageNet has successfully downloaded to this folder

<p align="center"><img src="/Images/Azure-ML-Workbench-Outputs-Model-Folder.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Outputs-Model-Folder.jpg" width="70%" height="70%"/><p>
 
8.	In azure ml workbench select the code file 'model.py' and enter arguments  --train  in the arguments field and click 'Run'
Note: model training will take some time complete. Once the script has finished running check the model folder inside the azure_ml_outputs folder, the following files should be added to the folder

<p align="center"><img src="/Images/Azure-ML-Workbench-Outputs-Model-Folder2.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Outputs-Model-Folder2.jpg" width="70%" height="70%"/><p>


### Create Web Service to be used for Model Evaluation

The following steps will illustrate how to create a web service that can be used for classifying images using the model

1.	In Azure ML Workbench run ‘score.py’ script, this will create the schema file required by the webservice to determine the type of input and output. The service_schema.json file will be added to the output folder that was created under Generate Model section, step 2

2.	Select prep_deploy.py script and enter the path of the folder where you would like to create a directory for deployment in the arguments field (as shown in the screenshot below). Then click ‘Run’.  This folder is the location where the script will copy all the files needed to create the web service

<p align="center"><img src="/Images/Azure-ML-Workbench-Prep-Deploy-Code.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Prep-Deploy-Code.jpg" width="70%" height="70%"/><p>

After the script has run verify that the following files have been copied to the folder as shown in the image below

<p align="center"><img src="/Images/Azure-ML-Workbench-Azure-ML-Deploy-Folder.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Azure-ML-Deploy-Folder.jpg" width="70%" height="70%"/><p>
    

3.	In Azure ML Workbench, select File > Open Command Prompt (also referred to as the Azure Machine Learning Workbench CLI window, 		or CLI window for short)

4.	In the Command prompt /CLI window navigate to the folder created for deployment (refer to step 2)
	
```
cd c:\azure_ml_deploy
```

example: the above command will open the folder c:\azure_ml_deploy

5.	In the command prompt enter the following commands to register the environment
 	provider

```
az provider register -n Microsoft.MachineLearningCompute
az provider register -n Microsoft.ContainerRegistry
az provider register -n Microsoft.ContainerService
```

To check if the environment providers have installed correctly enter the following 
commands:

```
az provider show -n Microsoft.MachineLearningCompute
az provider show -n Microsoft.ContainerRegistry
az provider show -n Microsoft.ContainerService
```

6. Next step is to create an ACS cluster (which may take 10-20 minutes to be completely provisioned). Enter the following command 	to provision an ACS cluster

Azure CLI commands: (sets up an ACS cluster in the eastus2 region named amldeployment)
The format of the command is as follows:

az ml env setup --cluster -n [your environment name] -l [Azure region e.g. eastus2] [-g [resource group]]

```
az ml env setup  --cluster  -n amldeployment  -l eastus2  -g amldeploymentrg
```

To see if the cluster environment is setup run the following command

```
az ml env show -g  amldeploymentrg  -n amldeployment
```

While the environment is being created you will get the following message

```
{
  "Cluster Name": "amldeployment",
  "Cluster Size": 2,
  "Created On": "2018-01-16T05:54:58.251Z",
  "Location": "eastus2",
  "Provisioning State": "Creating",
  "Resource Group": "amldeploymentrg",
  "Subscription": "c9726640-cf74-4111-92f5-0d1c87564b9
}
```
The provisioning state variable will show that the cluster environment is still in the process of being created. Wait 10-20 mins then run the command again, you should see the following output if cluster environment was successfully created

```
{
  "Cluster Name": "amldeployment",
  "Cluster Size": 2,
  "Created On": "2018-01-16T05:54:58.251Z",
  "Location": "eastus2",
  "Provisioning State": "Succeeded",
  "Resource Group": "amldeploymentrg",
  "Subscription": "c9726640-cf74-4111-92f5-0d1c87564b93"
}
```
	   
7.   Once the cluster has been provisioned successfully, set the environment to the cluster that was just created using the following 	      command

```
az ml env set  -g amldeploymentrg  -n amldeployment
```
After running the above command you should see the following output

```
Kubectl dashboard started for cluster at this endpoint: 127.0.0.1:52843/ui
Compute set to amldeployment
```

8.  Then switch from the local to the cluster using the following command

```
az ml env cluster
```
You may get a prompt that says ‘Continue with this subscription (Y/n)?’ enter ‘y’ for yes
After running the above command, you should see the following message in the command window

```
Now running in cluster mode
```

9.   Next create a model management account using the following command:
     Note: the format of the command is as follows:
              
     <b>az ml account modelmanagement create -l [Azure region, e.g. eastus2] 
     -n [your account name] -g [resource group name] --sku-instances 
		 [number of instances, e.g. 1] --sku-name [Pricing tier for example S1]</b>

```
az ml account modelmanagement create -l eastus2 -n modelmanageac -g  amldeploymentrg --sku-instances 1 --sku-name DevTest
```

10.  To select the newly created model management account run the following command

```
az ml account modelmanagement set -n modelmanageac -g amldeploymentrg
```

11.   Create the web service service (this can take 10-20 minutes), by running the following command:

      Note: The score.py script file contains the code for the service, for running the prediction 
      on the model and also for generating the input schema for the service

```
az ml service create realtime -c conda_dependencies.yml -f score.py -s service_schema.json -n imgclassapi -v -r python -d id2label --model-file resnet34-inat.model
```

The following switches are used with the az ml service create realtime command:

•	-n: The app name, which must be all lowercase.
•	-f: The scoring script file name.
•	--model-file: The model file. In this case, it's the pickled model.pkl file.
•	-s: The schema file that contains the schema for the input data to the web service
•	-r: The type of model. In this case, it's a Python model.
•	-c: Path to the conda dependencies file where additional packages are specified

#### Retrieve Endpoint URL and  Keys

In part 2 of this tutorial, you will need the following:
•	Service End point URL
•	Primary Key

1.	Navigate to portal.azure.com. Click ‘All resources’ in the left hand menu and search for the modelmanagement account 	 		‘modelmanageac’. Then open modelmanageac 

<p align="center"><img src="/Images/Azure-ML-Workbench-Outputs-Metadata-Folder.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Outputs-Metadata-Folder.jpg" width="70% height="70%"/><p>
 

2.	Next select ‘Model Management’ under application settings. Then select ‘Services’. Then select the ‘imgclassapi’ service. The 		next window contains the end point url and primary and secondary keys

<p align="center"><img src="/Images/Azure-ML-Workbench-Azure-ML-ModelManageAc-Services.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Azure-ML-ModelManageAc-Services.jpg" width="70% height="70%"/><p>

<p align="center"><img src="/Images/Azure-ML-Workbench-Azure-ML-Services-Imgclassapi.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Azure-ML-Services-Imgclassapi.jpg" width="70% height="70%"/><p>

<p align="center"><img src="/Images/Azure-ML-Workbench-Azure-ML-Service-Details.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Azure-ML-Service-Details.jpg" width="70% height="70%"/><p>
