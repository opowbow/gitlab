# gitlab

Steps to create demo if gitlab for tanzu products. 

For TKG on AWS pipelines. 

install gitlab. 

Create new project in gitlab. 
create tkg custer. 
install runner  
  a. install helm  
  b. add gitlab runner chart "helm repo add gitlab https://charts.gitlab.io". 
  c. create gitlab namespace "kubectl create ns gitlab". 
  d. grab token for runner - <gitlab home> - Settings - CICD - Runners - Group Runners .....token. 
  e. curl --request POST 'https://gitlab.com/api/v4/runners' --form 'TOKEN' --form 'description=<RUNNER-NAME'. 
  f. output = {"id":123456,"token":"xxxxxxxxxx"}. 
  g. create runner: helm install tanzu-demo-runner --namespace gitlab gitlab/gitlab-runner --set gitlabUrl=https://gitlab.com/opowbow/tanzu-pipeline-demo,runnerRegistrationToken=xxxxxxxxxx. 


