# Documentation
https://learn.microsoft.com/en-us/azure/machine-learning/?view=azureml-api-2

Machine Learning Studio  
https://ml.azure.com/home?tid=02e760b0-1b5a-4c7d-9e8f-4d421bd8cbb0

## Sample data
https://azuremlexamples.blob.core.windows.net/datasets/credit_card/default_of_credit_card_clients.csv

## Notebooks
Can be downloaded from Azure Machine Learning Studio or from VS Code Desktop version.

Can be opened in VS code Desktop from Azure ML studio

Login issues in VS code or on Azure can be resolved from Azure Notebook window (banner to authenticate will pop up above ntotebook).

Folder hierarchy when loading files in notebooks refers to workspace notebook file structure (root folder is username, current folder is folder where notebook is located). 

# Visual Studio Code ML extension
Use "Azure ML: Set Default Workspace" command to set the default workspace that exists in Azure if none is set. If it is set correctly a subscription will show workspace and resources under it.

## Documentation
https://learn.microsoft.com/en-us/azure/machine-learning/how-to-setup-vs-code?view=azureml-api-2

# Submit Experimet to remote external VM (attached compute)

Azure managed compute instance is still required (although minimal), external can be used as added workforce.

Create a new kernel for workspace on compute instance
https://stackoverflow.com/questions/65159308/how-to-use-existing-conda-environment-as-a-azureml-environment

Section "Create and Attach a DSVM as a compute target", doesnt have to be DSVM image, could create Conda environment as sections below on vanilla linux VM:  
https://github.com/Azure/MachineLearningNotebooks/blob/master/how-to-use-azureml/training/train-on-remote-vm/train-on-remote-vm.ipynb

Initial resources for safekeeping:  
https://learn.microsoft.com/en-us/answers/questions/349518/azure-machine-learning-and-attached-compute-instan  
https://rukiatu.com/installing-azure-machine-learning-sdk-for-python/

## Setting up conda environment on external VM

Installing miniconda  
https://docs.conda.io/en/main/miniconda.html#quick-command-line-install

Using miniconda  
https://docs.conda.io/projects/conda/en/stable/user-guide/getting-started.html#starting-conda  
conda update conda  
conda create --name ml  
conda activate ml  

conda list  
conda remove -n ml --all //remove environment

Cheatsheet  
https://docs.conda.io/projects/conda/en/stable/_downloads/69c8c83c892884d9bc3700172a949a5b/conda-4.6.pdf

## Install microsoft ML SDK on Conda Environment on remote VM (attached compute)
https://learn.microsoft.com/en-us/python/api/overview/azure/ai-ml-readme?view=azure-python  
conda install python=3.7 //Use without the version, just conda install python to install 3.11 

conda install -c microsoft azure-ai-ml //does not work, use conda pip

//No conda required here, environment is activated on the left of prompt
pip install azure-ai-ml
pip install azure-identity

Test with python script to try to authenticate with Azure
```
from azure.ai.ml import MLClient
from azure.identity import DefaultAzureCredential

ml_client = MLClient(
    DefaultAzureCredential(), subscription_id, resource_group, workspace
)
```
Where subscription_id, resource_group, workspace should be strings with double quotations copied from azure subscription and azure workspace.


## Install and start notebook server on remote VM (attached compute)
https://learn.microsoft.com/hr-hr/azure/machine-learning/how-to-configure-environment?view=azureml-api-2

conda install notebook ipykernel //Enable environment-specific IPython kernels

ipython kernel install --user --name ml --display-name "Python (ml)" //Create a kernel for your Python virtual environment.

Launch the Jupyter Notebook server
https://docs.anaconda.com/free/anaconda/jupyter-notebooks/remote-jupyter-notebook/  
jupyter notebook --no-browser --port=8080