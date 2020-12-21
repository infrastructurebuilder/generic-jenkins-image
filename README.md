# generic-jenkins-image

Generate an image to work with Jenkins.

## Building a new version

* Change the `VERSION` file to the new version
* Commit your change and set a tag for that version

We need environment variables for the following

```
export CONTAINER_HUB_LOGIN=
export CONTAINER_HUB_PASSWORD=
export CONTAINER_REGISTRY=https://hub.docker.com/
export THE_USER=
export THIS_VERSION=$(cat VERSION)
export JENKINS_USERNAME=
export JENKINS_PASSWORD=
```
