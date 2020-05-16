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

'$rg="lab-aq-1"
'az group delete --name $rg --yes --no-wait

Takes a while but disappears gradually from azure as it removes resources from the resource group