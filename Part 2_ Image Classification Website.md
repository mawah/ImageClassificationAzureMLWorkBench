## Part 2: Image Classification Website

## Getting Started

1.	You will need an Azure subscription. You can sign up for a trial subscription by following the instructions [here](https://azure.microsoft.com/get-started).

2.	Downloaded the [Images.zip file](https://github.com/akegramener/INatImages/raw/master/Images.zip) containing relevant images, and upload the file to an Azure Storage blob container. If you need further assistance to create a storage account, blob container, or SAS URL for data upload, refer the following links:
    
    1. [Create a Storage Account and blob container](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-quickstart-blobs-portal ) 
    2. [Upload data to a blob container with Azure Storage Explorer](https://docs.microsoft.com/en-us/azure/machine-learning/team-data-science-process/move-data-to-azure-blob-using-azure-storage-explorer)

3.	If you would like to review the code for the site, the full web site project can be accessed from [this companion GitHub repository](https://github.com/akegramener/ImgClassWrkbenchWeb).


### Deploy the website

1.	To deploy the website in Azure, open [this link](https://deploy.azure.com/?repository=https://github.com/akegramener/Image-Classification-Using-MS-AI-Tools/tree/master/Code-ImageClassificationWebsite#/form/setup). If you are not logged into Azure, you will be prompted to log in. The following window should launch in your browser:

    <p align="center"><img src="/Images/Website-Deploy-Azure.jpg" 
data-canonical-src="/Images/Website-Deploy-Azure.jpg" width="80%" height="80%"/><p>

3.	Update the fields in the form shown above (some fields will have been filled in automatically). Key fields that need to be updated are the following:

    -	<b>Azure ML Workbench URL</b>: – This is the service endpoint URL generated using Azure Machine Learning. Refer to the "Retrieve Endpoint URL and Keys" section in [Part 1: Image Classification using Azure ML Workbench](./Part%201_%20Image%20Classification%20Azure%20ML%20Workbench.md).

    -	<b>Azure ML Workbench - Service Key </b>: This is the service primary key generated using Azure Machine Learning. Refer to the "Retrieve Endpoint URL and Keys" section in [Part 1: Image Classification using Azure ML Workbench](./Part%201_%20Image%20Classification%20Azure%20ML%20Workbench.md).
    
    -	<b>Azure Storage - Connection String</b>: This is the connection string for the Azure Storage account where the zip file to the images to be displayed on the website is stored.

    -	<b>Azure Storage - Container Name</b>: This is the blob container name where the zip file to displayed on the website is stored.


4.	Once you have filled in the fields, click "Next,"  then click "Deploy" on the next screen.

    <p align="center"><img src="/Images/Website-Deploy-Azure2.jpg" 
data-canonical-src="/Images/Website-Deploy-Azure2.jpg" width="80%" height="80%"/><p>

    Note: The deployment takes a few minutes to complete.

5.	Once the deployment is complete, click on the site url at the bottom of the deployment screen. You should see the following screen:

    <p align="center"><kbd><img src="/Images/Website-Download-Images.jpg" 
data-canonical-src="/Images/Website-Download-Images.jpg" width="80%" height="80%" border="1"/></kbd><p>

6.	Click on the "Download Images" button to load the images from the Azure blob container that was specified during deployment.

    Note: this will take a few mins to complete. Do not close the window until the download is complete. While the images are downloading, you will see the following screen:

    <p align="center"><kbd><img src="/Images/Website-Downloading-Images.jpg" 
data-canonical-src="/Images/Website-Downloading-Images.jpg" width="80%" height="80%" border="1"/></kbd><p>

    Once the images are downloaded, you should see the following screen:
    <p align="center"><kbd><img src="/Images/Website-Sample-Images.jpg" 
    data-canonical-src="/Images/Website-Sample-Images.jpg" width="80%" height="80%" border="1"/></kbd><p>

### Test the Site

1.	Select an image on the screen by clicking on the image. This will load more images for the species that was selected. Example: if you clicked on "Actionpterygii – Abudefduf saxatalis,". you should see the following screen:

    <p align="center"><kbd><img src="/Images/Website-Predict.jpg" 
data-canonical-src="/Images/ Website-Predict.jpg" width="80%" height="80%"/></kbd><p>

2.	Click the "Predict" button at the bottom of any of the images. It should load the predictions returned by your web service, similar to the screenshot below:

    <p align="center"><kbd><img src="/Images/Website-Top5-Predictions.jpg" 
    data-canonical-src="/Images/Website-Top5-Predictions.jpg" width="80%" height="80%"/></kbd><p>

