
# DB install

## postgres
postgre/     
cm.yaml.  
pv.yaml.  
deply.yaml.  
svc.yaml.  

CM settings
  POSTGRES_DB: postgresdb
  POSTGRES_USER: postgresadmin
  POSTGRES_PASSWORD: admin123
  
  

# gitlab

Steps to create demo if gitlab for tanzu products. 

For TKG on AWS pipelines. 

install gitlab. 

Create new project in gitlab. 
create tkg custer. 
install runner  
  a. install helm.     
  
  b. add gitlab runner chart "helm repo add gitlab https://charts.gitlab.io". 
  
  c. create gitlab namespace "kubectl create ns gitlab".   
  
  d. grab token for runner - <gitlab home> - Settings - CICD - Runners - Group Runners .....token.   
  
  e. curl --request POST 'https://gitlab.com/api/v4/runners' --form 'TOKEN' --form 'description=<RUNNER-NAME'.   
  
  f. output = {"id":123456,"token":"xxxxxxxxxx"}.   
  
  g. create runner: helm install tanzu-demo-runner --namespace gitlab gitlab/gitlab-runner --set gitlabUrl=https://gitlab.com/opowbow/tanzu-pipeline-demo,runnerRegistrationToken=xxxxxxxxxx.   
  
  h. Runner appear in gitlab as an "Available specific runners".   
  
  
# Harbor install
## by helm / bitnami

helm repo add bitnami https://charts.bitnami.com/bitnami   
helm install my-release bitnami/harbor.  
export SERVICE_IP=$(kubectl get svc --namespace harbor my-release-harbor --template "{{ range (index .status.loadBalancer.ingress 0) }}{{.}}{{ end }}").  
echo "Harbor URL: http://$SERVICE_IP/".  
echo Username: "admin".   
echo Password: $(kubectl get secret --namespace harbor my-release-harbor-core-envvars -o jsonpath="{.data.HARBOR_ADMIN_PASSWORD}" | base64 --decode).  

## by tanzu extension (kapp)

# Replicate Images from docker to harbor. 





 


