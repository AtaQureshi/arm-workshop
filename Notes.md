# Lab 1

    az login
    az group create --name lab-aq-1 --location "UK South"

    cd lab-aq-1
    az group deployment create --name job1 --resource-group lab-aq-1 --template-file azuredeploy.json

Install "Azure Resource Manager snippets" by Sam Cogan - ctrl+shft+e - then arm! will work

## Formatting json

alt+m minifies the json
ctrl_alt+m pretty prints json

    $rg="lab-aq-1"
    $template="C:\Dev\ARM\lab-aq-1\azuredeploy.json"
    $job="job2"
    $parms="storageAccount=aqlab1sa2"
    az group deployment create --name $job --parameters "$parms" --template-file $template --resource-group $rg

### Continue...

From ARM Functions section
Zapped the resource group to ensure we don't incur costs. Simply recreate the above after reading the next section

## Deleting the resource group

    $rg="lab-aq-1"
    az group delete --name $rg --yes --no-wait

Takes a while but disappears gradually from azure as it removes resources from the resource group

## Important url's

ARM Template Functions:

https://docs.microsoft.com/en-us/azure/azure-resource-manager/templates/template-functions

Naming convention best practice:

https://docs.microsoft.com/en-us/azure/cloud-adoption-framework/ready/azure-best-practices/naming-and-tagging

## Validating a template

    az group deployment validate

Therefore our command then becomes     

    $rg="lab-aq-1"
    $template="C:\Dev\ARM\lab-aq-1\azuredeploy.json"
    $job="job2"
    az group deployment validate --template-file $template --resource-group $rg --output table

Now we actually go ahead and execute the revised template to create storage. I have taken out the parameters variable as this is now and auto generated unique value:

    $rg="lab-aq-1"
    $template="C:\Dev\ARM\lab-aq-1\azuredeploy.json"
    $job="job2"
    az group deployment create --name $job --template-file $template --resource-group $rg

*Oops... the created storage account is called!:*

aqlab1gjanqbswvt6b4

There is nothing in there telling us that it is a storage account. We should revise the prefix in the template to include an indicator such as aqlab1sa.

Revise and re-execute the template