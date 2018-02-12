## Part 5: Image Classification Website

### Overview

The image classification site in this example makes calls to web services from the following platforms to classify images
•	Custom Vision - https://customvision.ai/

•	Computer Vision: https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/

•	Azure ML Workbench: https://docs.microsoft.com/en-us/azure/machine-learning/preview/overview-what-is-azure-ml

•	Azure ML Studio:  https://docs.microsoft.com/en-us/azure/machine-learning/preview/overview-what-is-azure-ml

### Getting Started

1.	You will need an azure paid or trial subscription. To sign up for a subscription refer to the following guide https://azure.microsoft.com/en-us/get-started/?v=17.39

2.	Ensure that you have completed Parts 1 to 4 of this tutorial.

3.	Downloaded and extract the images from https://storage.googleapis.com/us_inat_data/train_val/train_val_images_mini.tar.gz 

4.	Zip the images into a folder call it Images.zip. The zip folders show contain folders in the following structure Images > genus > species as shown below
Example: Images > Actinopterygii > Abudefduf saxatillis

<p align="center"><img src="/Images/Website-Azure-Folder-Structure.jpg" 
data-canonical-src="/Images/Website-Azure-Folder-Structure.jpg" width="45%" height="45%"/><p>

<p align="center"><img src="/Images/Website-Azure-Folder-Structure-Species.jpg" 
data-canonical-src="/Images/Website-Azure-Folder-Structure-Species.jpg" width="60%" height="60%"/><p>

2.	Upload the Images.zip to an azure storage blob container. 
    If you need further assistance on how to create a blob container and SAS URL follow the steps below:
    
  1. Create a Storage Account and blob container– Refer to the following guide
     https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal 
     
  2. Upload data to a blob container – Refer to the following guide
     https://docs.microsoft.com/en-us/azure/machine-learning/team-data-science-process/move-data-to-azure-blob-using-azure-storage-explorer

3.	If you would like to review the code for the site, the full web site project can be accessed from github https://github.com/akegramener/Image-Classification-Using-MS-AI-Tools/tree/master/Code-ImageClassificationWebsite


### Deploy the website

1.	To deploy the website in Azure open the following link https://deploy.azure.com/?repository=https://github.com/akegramener/Image-Classification-Using-MS-AI-Tools/tree/master/Code-ImageClassificationWebsite#/form/setup. If you are not logged into Azure, you will be prompted to log in

2.	You should see the following window in the browser

<p align="center"><img src="/Images/Website-Deploy-Azure.jpg" 
data-canonical-src="/Images/Website-Deploy-Azure.jpg" width="80%" height="80%"/><p>

3.	In the above form update the fields, some fields have been filled in automatically. Key fields that need to be updated are the following:

    -	<b>Custom Vision AI-ProjectId:</b> Refer to Part1 Image Classification using Custom Vision Retrieve Project Id, Prediction URL  and  Prediction Key which explains how to retrieve the projectId

    -	<b>Custom Vision-BaseURI:</b>  This the service endpoint url for custom.vision.ai. for information on how to retrieve the endpoint service url refer to Part1 Image Classification using Custom Vision Retrieve Project Id, Prediction URL and  Prediction Key

    -	<b>Custom Vision AI-Prediction Key:</b>  This is required by the custom vision ai service. Refer to Part1 Image Classification using Custom Vision Retrieve Project Id, Prediction URL and  Prediction Key

    -	<b>Computer Vision-Base URI:</b>  This is service endpoint url for Computer Vision Service. Refer to Part 2 Image Classification using Computer Vision Retrieve Endpoint URL and Access Keys

    -	<b>Computer Vision- Subscription Key:</b> This is required by Computer Vision API for authentitcation. Refer to Part 2 Image Classification using Computer Vision Retrieve Endpoint URL and Access Keys

    -	<b>Azure ML WorkBench URL:</b> – This is web service url generated using Azure ML. Refer to Part 3 Image Classification using Azure ML Workbench Retrieve Endpoint URL and  Keys

    -	<b>Azure ML Work Bench - Service Key </b>: This is the service key required by Azure ML Workbench. Refer to Part 3 Image Classification using Azure ML Workbench Retrieve Endpoint URL and  Keys

    -	<b>Azure ML Studio - API URI:</b> This is the service url generated in Azure ML Studio. Refer to Part 4 Image Classification using Azure ML Studio Retrieve Prediction URL and Prediction Key

    -	<b>Azure ML Studio - API Key:</b> This is the API key for the web service generated using Azure ML studio. Refer to Part 4 Image Classification using Azure ML Studio Retrieve Prediction URL and Prediction Key

    -	<b>Azure Storage - Connection String:</b> This is the connection string for the azure storage account where zip file to the images to be displayed on the website are stored

    -	<b>Azure Storage - Container Name:</b>  This is the blob container name where the zip file to displayed on the website will be stored


4.	Once you have filled in the fields click ‘Next’  then click ‘Deploy’ on the next screen

<p align="center"><img src="/Images/Website-Deploy-Azure2.jpg" 
data-canonical-src="/Images/Website-Deploy-Azure2.jpg" width="80%" height="80%"/><p>

Note: The deployment takes a few mins to complete

5.	Once the deployment is complete click on the site url at the bottom of the deployment screen. You should see the following screen:

<p align="center"><kbd><img src="/Images/Website-Download-Images.jpg" 
data-canonical-src="/Images/Website-Download-Images.jpg" width="80%" height="80%" border="1"/></kbd><p>

6.	Click on the ‘Download Images’ button this will load the images from the azure container that was provided during deployment.
    Note: this will take a few mins to complete, do not close the window till the download is complete, while the images are downloading you will see the following screen:

<p align="center"><kbd><img src="/Images/Website-Downloading-Images.jpg" 
data-canonical-src="/Images/Website-Downloading-Images.jpg" width="80%" height="80%" border="1"/></kbd><p>

7.	Once the images are downloaded you should see the following screen
    <p align="center"><kbd><img src="/Images/Website-Sample-Images.jpg" 
    data-canonical-src="/Images/Website-Sample-Images.jpg" width="80%" height="80%" border="1"/></kbd><p>

### Test the Site

1.	Click on options in the top navigation bar

<p align="center"><kbd><img src="/Images/Website-Options.jpg" 
data-canonical-src="/Images/Website-Options.jpg" width="80%" height="80%"/></kbd><p>

You should see the following window:
<p align="center"><kbd><img src="/Images/Website-Options-Custom-vision.jpg" 
data-canonical-src="/Images/Website-Options-Custom-vision.jpg" width="80%" height="80%"/></kbd><p>

2.	Select ‘Custom Vision’ Then clcik on an image on the screen. This will load more images for the species that was selected. Example if you clicked on ‘Actionpterygii – Abudefduf saxatalis’. You should see the following screen:

<p align="center"><kbd><img src="/Images/Website-Predict.jpg" 
data-canonical-src="/Images/ Website-Predict.jpg" width="80%" height="80%"/></kbd><p>

3.	Click the ‘Predict’ button at the bottom of any of the images. It should load the predictions from custom vision AI similar to the screen below

<p align="center"><kbd><img src="/Images/Website-Top5-Predictions.jpg" 
data-canonical-src="/Images/Website-Top5-Predictions.jpg" width="80%" height="80%"/></kbd><p>

4.	To test all the services, repeat steps 1-3 for Computer Vision AI, Azure ML Workbench and Azure ML studio experiments