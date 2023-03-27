

```shell
# build image
$ docker build -t ogre0403/cloud-sdk:alpine -f Dockerfile.alpine .

# GCP login
$ docker run -ti --name gcloud-config ogre0403/cloud-sdk:alpine gcloud auth login

$ docker run --rm -ti --volumes-from gcloud-config ogre0403/cloud-sdk:alpine bash
```

