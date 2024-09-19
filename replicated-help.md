## Log out of registrys to re-authenticate

helm repository logout registry-1.docker.io
helm repository logout registry.replicated.com

## If updated are made outside of /manifest directory, repackage with helm

# cd to root of repo
helm package . --dependency-update
# move created .tgz file to manifest directory

## Lint and then Create a replicated release (in manifest directory)
replicated release lint --yaml-dir . 
replicated release create --yaml-dir .
