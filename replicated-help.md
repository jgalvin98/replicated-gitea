## Log out of registrys to re-authenticate

helm registry logout registry-1.docker.io
helm registry logout registry.replicated.com

## If updated are made outside of /manifest directory, repackage with helm

# cd to root of repo
helm package . --dependency-update
# move created .tgz file to manifest directory
mv *.tgz ./manifests
## Lint and then Create a replicated release (in manifest directory)
replicated release lint --yaml-dir ./manifests 
replicated release create --yaml-dir ./manifests
