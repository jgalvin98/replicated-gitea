## Step 1 - Initial Flow - Files to review
gitea 

Chart.yaml

./manifest/embedded-cluster.yaml

./manifest/gitea.yaml

./manifest/kots-app.yaml

./manifest/k8s-app.yaml


## Create App
replicated app create gitea-hup

## Set ENV VARS

export REPLICATED_API_TOKEN=
export REPLICATED_APP=gitea-

## Log out of registrys to re-authenticate

helm registry logout registry-1.docker.io
helm registry logout registry.replicated.com

## If updates are made outside of /manifest directory, repackage with helm
## cd to root of repo

cd ~/replicated/projects/replicated-gitea
helm package . --dependency-update

## move created .tgz file to manifest directory

mv *.tgz ./manifests

## Lint and then Create a replicated release (in manifest directory)

replicated release lint --yaml-dir ./manifests 
replicated release create --yaml-dir ./manifests

## Step 2 - Adding Customized Config Inputs - Files to review
git checkout unstable
./manifest/config.yaml
./manifest/gitea.yaml

replicated release create --yaml-dir ./manifests
replicated promote to unstable channel - GUI
Grab install commands from Customer Page
ssh to vm2.chancydog.com
Go to vm2.chancydog.com:30000 in browser
admin console already running
Install the app, noting the customize config screen

## Step 3 - Adding Pre-flight checks and Embedded Cluster node roles - Files to review
git checkout beta
./templates/preflights.yaml - note the k8s cluster cpu and ram requirements
./manifests/embeeded-cluster.yaml - notes the version change and role specs

replicated release create --yaml-dir ./manifests
replicated release ls
replicated channel ls
replicated release promote SEQUENCE CHANNEL_ID
go back to vm2.chancydog.com admin console and refresh releases available
deploy the new release
note the preflight checks
note the Cluster Management "add nodes" and view the management and app node buttons

## Step 4 - Review the Compatiblity Matrix screen
go to GUI Compatibility Matrix

create 3 clusters

replicated cluster -h
replicated cluster create --distribution eks
replicated cluster create --distribution aks
replicated cluster create --distribution gke

replicated cluster ls
view in GUI under Compatibility Matrix

remove the test clusters

replicated cluster rm --all