## Set ENV VARS

export REPLICATED_API_TOKEN=
export REPLICATED_APP=

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

