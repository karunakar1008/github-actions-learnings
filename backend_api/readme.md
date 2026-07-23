Create a Container Apps
--Open Azure powershell

$RESOURCE_GROUP="rg-containerapps-github-actions"
$LOCATION="westeurope"
$CONTAINERAPPS_ENVIRONMENT="aca-environment"
$CONTAINERAPPS_APP="album-backend-api"

az group create `
         --name $RESOURCE_GROUP `
         --location $LOCATION


az containerapp env create `
                --name $CONTAINERAPPS_ENVIRONMENT `
                --resource-group $RESOURCE_GROUP `
                --location $LOCATION

az containerapp env show  --name "aca-environment" --resource-group "rg-containerapps-github-actions"

az containerapp create `
                --name $CONTAINERAPPS_APP `
                --resource-group $RESOURCE_GROUP `
                --environment $CONTAINERAPPS_ENVIRONMENT `
                --image mcr.microsoft.com/azuredocs/containerapps-helloworld:latest `
                --target-port 80 `
                --ingress 'external'

az containerapp show `
                --name $CONTAINERAPPS_APP `
                --resource-group $RESOURCE_GROUP `
                --query properties.configuration.ingress.fqdn


https://github.com/HoussemDellai/aca-course/blob/main/.github/workflows/azure-container-apps-ci-cd.yml
