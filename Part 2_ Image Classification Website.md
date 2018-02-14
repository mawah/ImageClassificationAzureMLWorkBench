## Part 2: Image Classification Website

## Getting Started

1.	You will need an azure paid or trial subscription. To sign up for a subscription refer to the following guide https://azure.microsoft.com/en-us/get-started/?v=17.39

2.	Downloaded images.zip file from https://github.com/akegramener/INatImages 

3.	Upload the Images.zip to an azure storage blob container. 
    If you need further assistance on how to create a blob container and SAS URL follow the steps below:
    
  1. Create a Storage Account and blob container– Refer to the following guide
     https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal 
     
  2. Upload data to a blob container – Refer to the following guide
     https://docs.microsoft.com/en-us/azure/machine-learning/team-data-science-process/move-data-to-azure-blob-using-azure-storage-explorer

3.	If you would like to review the code for the site, the full web site project can be accessed from github https://github.com/akegramener/ImgClassWrkbenchWeb


### Deploy the website

1.	To deploy the website in Azure open the following link https://deploy.azure.com/?repository=https://github.com/akegramener/Image-Classification-Using-MS-AI-Tools/tree/master/Code-ImageClassificationWebsite#/form/setup. If you are not logged into Azure, you will be prompted to log in

2.	You should see the following window in the browser

<p align="center"><img src="/Images/Website-Deploy-Azure.jpg" 
data-canonical-src="/Images/Website-Deploy-Azure.jpg" width="80%" height="80%"/><p>

3.	In the above form update the fields, some fields have been filled in automatically. Key fields that need to be updated are the following:

    -	<b>Azure ML WorkBench URL:</b> – This is web service url generated using Azure ML. Refer to Part 1 Image Classification using Azure ML Workbench Retrieve Endpoint URL and  Keys

    -	<b>Azure ML Work Bench - Service Key </b>: This is the service key required by Azure ML Workbench. Refer to Part 1 Image Classification using Azure ML Workbench Retrieve Endpoint URL and  Keys
    
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

1.	Select on an image on the screen by clicking on an image. This will load more images for the species that was selected. Example if you clicked on ‘Actionpterygii – Abudefduf saxatalis’. You should see the following screen:

<p align="center"><kbd><img src="/Images/Website-Predict.jpg" 
data-canonical-src="/Images/ Website-Predict.jpg" width="80%" height="80%"/></kbd><p>

2.	Click the ‘Predict’ button at the bottom of any of the images. It should load the predictions from custom vision AI similar to the screen below

<p align="center"><kbd><img src="/Images/Website-Top5-Predictions.jpg" 
data-canonical-src="/Images/Website-Top5-Predictions.jpg" width="80%" height="80%"/></kbd><p>

