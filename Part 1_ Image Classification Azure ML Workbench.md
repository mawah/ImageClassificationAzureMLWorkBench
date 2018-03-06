## Part 1: Image Classification Using Azure Machine Learning Workbench

### Getting Started

#### Install Azure Machine Learning Workbench

Follow the first two steps in the [Azure Machine Learning Quickstart Guide](https://docs.microsoft.com/en-us/azure/machine-learning/preview/quickstart-installation), which are listed below for clarity:

1.	Create Azure Machine Learning Accounts

	In this step, uncheck "create model management account": the model management account will be created later in the tutorial.
2.	Install Azure Machine Learning Workbench on Windows

#### Install Python libraries

Open Azure Machine Learning Workbench, then from the menu, select File -> Open Command Prompt. This will open the Azure CLI window. Enter the following commands to install the required python libraries:
```
pip install https://cntk.ai/PythonWheel/GPU/cntk-2.3.1-cp35-cp35m-win_amd64.whl
conda install pillow
pip install -U numpy
pip install configparser
```

### Create a new project in Azure Machine Learning Workbench

1.	From the menu in Azure Machine Learning Workbench, click on File -> New Project.
2.	Enter the project details, e.g.

	<b>Project Name:</b> ImageClassificationProject<br/>
	<b>Project Directory:</b> Default <br/>
	<b>Workspace:</b> (Select workspace created during the Installation step) <br/>
	<b>Project Template:</b> Select a blank template <br/>

### Generate The Model

1.  Download the Image Classification project from [our repository](https://github.com/akegramener/ImgClassAzureMLCode) and copy all the files to the new project folder that was created in Azure ML Workbench. (Refer to the image below to locate the project folder.) For an explanation of the code please refer to tutorial [Enter tutorial details for the INAT tutorial]. 
	<p align="center"><img src="/Images/Azure-ML-Workbench-Project-Direc.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Project-Direc.jpg" width="80%" height="80%" /><p>

2. Open the project directory (Directory location as shown in the image above). Locate the file named `Config.ini` and change the 'PATH' variable to a location that you prefer. (By default, the path points to `c:\azure_ml_outputs`.)

3.  In Azure Machine Learning Workbench, click on the Files icon (a file folder) along the left-hand side of the screen, then click on the file named `create_directories.py`. We will use this script to create an output directory on your machine in a specified location and create an environment variable pointing to the new folder. Enter your preferred location for the output directory in the "arguments" field, as show in the screenshot below. Click "Run".
         
	<p align="center"><img src="/Images/Azure-ML-Workbench-Create-Directories-Code.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Create-Directories-Code.jpg" width="80%" height="80%"/><p>
 
4.	Open the output directory created in step 2. Inside this directory, locate a folder named `data`. Download and extract the [image files](https://storage.googleapis.com/us_inat_data/train_val/train_val_images_mini.tar.gz) to the data folder as shown in the image below:
	<p align="center"><img src="/Images/Azure-ML-Workbench-Outputs-Data.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Outputs-Data.jpg" width="60%" height="60%" /><p>

5.  In Azure Machine Learning Workbench, click on the file named `structure_data.py`, then click "Run". After the code has finished running, you should see two new folders named `train` and `validation` have been created inside the `data` folder.
	<p align="center"><img src="/Images/Azure-ML-Workbench-Train-Validation-Folders.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Train-Validation-Folders.jpg" width="80%" height="80%" /><p>
	Navigate into the `train` and `validation` folders. Each of these folders should contain image files sorted into subdirectories by species, as shown in the screen shots below:
	<p align="center"><img src="/Images/Azure-ML-Workbench-Outputs-Folders.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Outputs-Folders.jpg" width="70%" height="70%"/><p>
	<p align="center"><img src="/Images/Azure-ML-Workbench-Outputs-Data-Train-Folder.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Outputs-Data-Train-Folder.jpg" width="70%" height="70%"/><p>
	
6. In Azure Machine Learning Workbench, click on the file named `create_map_files.py`, then click "Run". Once the code has finished running, navigate to the `metadata` folder in your chosen output directory. You should see the files as shown in the screenshot below
	<p align="center"><img src="/Images/Azure-ML-Workbench-Outputs-Metadata-Folder.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Outputs-Metadata-Folder.jpg" width="70%" height="70%"/><p>
 
7. In Azure Machine Learning Workbench, click on the file named `download_model.py` and click "Run". This code will download the [ResNet34 ImageNet CNTK model](https://www.cntk.ai/Models/CNTK_Pretrained/ResNet34_ImageNet_CNTK.model), which will be used for transfer learning in the next step. After the script has finished running, go to the `model` folder in your chosen output directory to ensure that the ResNet34 ImageNet model has been successfully downloaded to this folder.
	<p align="center"><img src="/Images/Azure-ML-Workbench-Outputs-Model-Folder.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Outputs-Model-Folder.jpg" width="70%" height="70%"/><p>

8. In Azure Machine Learning Workbench, click on the file named `model.py`, enter `--train` in the arguments field, and click "Run".
Note: model training will take some time complete. Once the script has finished running, check the `model` folder inside of your chosen output directory; the following files should have been added to the folder:

	<p align="center"><img src="/Images/Azure-ML-Workbench-Outputs-Model-Folder2.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Outputs-Model-Folder2.jpg" width="70%" height="70%"/><p>


### Create Web Service to be used for Model Evaluation

The following steps will illustrate how to create a web service that can be used for classifying images using the model.

1.	In Azure Machine Learning Workbench, click on the file named `score.py`, then click "Run". This will create the schema file required by the web service to determine the type of input and output. A file named `service_schema.json` will be added to the output folder that was created in step #2 of the "Generate Model" section.

2.	In Azure Machine Learning Workbench, click on the file named `prep_deploy.py` and enter the path of the folder where you would like to create a directory for deployment in the arguments field (as shown in the screenshot below), then click "Run".  This folder is the location where the script will copy all the files needed to create the web service.

	<p align="center"><img src="/Images/Azure-ML-Workbench-Prep-Deploy-Code.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Prep-Deploy-Code.jpg" width="70%" height="70%"/><p>

	After the script has run, verify that files have been copied to the specified folder, as shown in the image below:

	<p align="center"><img src="/Images/Azure-ML-Workbench-Azure-ML-Deploy-Folder.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Azure-ML-Deploy-Folder.jpg" width="70%" height="70%"/><p>

3.	In Azure Machine Leaning Workbench, click on File -> Open Command Prompt. This will launch the Azure Machine Learning Workbench Command Line Interface (CLI) window.

4.	In the CLI window, navigate to the folder you created for deployment in step two of this section. FOr example, the following command will navigate to a folder named `c:\azure_ml_deploy`:
	
	```
	cd c:\azure_ml_deploy
	```

5.	In the CLI window, enter the following commands to register the environment provider:

	```
	az provider register -n Microsoft.MachineLearningCompute
	az provider register -n Microsoft.ContainerRegistry
	az provider register -n Microsoft.ContainerService
	```

	To check if the environment providers have installed correctly, run the following 
	commands:

	```
	az provider show -n Microsoft.MachineLearningCompute
	az provider show -n Microsoft.ContainerRegistry
	az provider show -n Microsoft.ContainerService
	```

6.	To create an ACS cluster (which may take 10-20 minutes to be completely provisioned), edit the template command below to choose your desired environment name, Azure region, and resource group, then run the command.

	```
	az ml env setup --cluster -n [your environment name] -l [Azure region e.g. eastus2] [-g [resource group]]
	```
	
	For example, your completed command may resemble:

	```
	az ml env setup  --cluster  -n amldeployment  -l eastus2  -g amldeploymentrg
	```

	After issuing the setup command, check whether cluster environment setup is complete by editing the template command below, then running the command:

	```
	az ml env show -g [resource group] -n [your environment name] 
	```

	If the environment is still being created, you will get a message similar to the following:

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
	The provisioning state variable will show that the cluster environment is still in the process of being created. Wait 10-20 minutes, then run the command again. You should see output similar to the following if cluster environment was successfully created:

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
	   
7.   Once the cluster has been provisioned successfully, set the environment to be the cluster you just created by editing the command template below, then running the command:

	```
	az ml env set -g [resource group] -n [your environment name] 
	```
	After running the above command, you should see output similar to the following:

	```
	Kubectl dashboard started for cluster at this endpoint: 127.0.0.1:52843/ui
	Compute set to amldeployment
	```

8.  Switch from the local environment to the cluster environment using the following command:

	```
	az ml env cluster
	```
	You may get a prompt that says "Continue with this subscription (Y/n)?" If so, enter "y" to confirm. After running the above command, you should see the following message in the CLI window:

	```
	Now running in cluster mode
	```

9.   Create a model management account by editing the following command template appropriately, then running the command.
     Note: the format of the command is as follows:
              
	```
	az ml account modelmanagement create -l [Azure region, e.g. eastus2] ^
	-n [your account name] -g [resource group name] ^
	--sku-instances [number of instances, e.g. 1] --sku-name [Pricing tier for example S1]
	```
     
	For example, your completed command may resemble the following:

	```
	az ml account modelmanagement create -l eastus2 -n modelmanageac -g  amldeploymentrg --sku-instances 1 --sku-name DevTest
	```

10.  To select the newly created model management account, edit the command template below, then execute the command:

	```
	az ml account modelmanagement set -n [your account name] -g [resource group name]
	```

11.   Create the web service service (this can take 10-20 minutes), by running the following command:

	```
	az ml service create realtime -c conda_dependencies.yml -f score.py -s service_schema.json -n imgclassapi -v -r python -d id2label --model-file resnet34-inat.model
	```

	The following switches are used with the `az ml service create realtime` command:

	- `-n`: The app name, which must be all lowercase.
	- `-f`: The scoring script file name.
	- `--model-file`: The model file. In this case, it's the pickled model.pkl file.
	- `-s`: The schema file that contains the schema for the input data to the web service.
	- `-r`: The type of model. In this case, it's a Python model.
	- `-c`: Path to the conda dependencies file where additional packages are specified.

	Note: The `score.py` script file contains the code both for running predictions on the model as well as for generating the service's input schema (as you saw earlier).

#### Retrieve Endpoint URL and Keys

In part 2 of this tutorial, you will need the following credentials to call your web service:
- Service endpoint URL
- Service primary key

1.	Navigate to portal.azure.com. Click "All resources" in the left-hand menu, and search for the modelmanagement account you created earlier. Click on the appropriate search result.

2.	Under "Application Settings," click "Model Management," then click "Services." Click on the name of the web service you created ("imgclassapi"). A pane will appear containing the endpoint URL and primary/secondary keys.

	<p align="center"><img src="/Images/Azure-ML-Workbench-Azure-ML-ModelManageAc-Services.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Azure-ML-ModelManageAc-Services.jpg" width="70% height="70%"/><p>

	<p align="center"><img src="/Images/Azure-ML-Workbench-Azure-ML-Services-Imgclassapi.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Azure-ML-Services-Imgclassapi.jpg" width="70% height="70%"/><p>

	<p align="center"><img src="/Images/Azure-ML-Workbench-Azure-ML-Service-Details.jpg" data-canonical-src="/Images/Azure-ML-Workbench-Azure-ML-Service-Details.jpg" width="70% height="70%"/><p>
