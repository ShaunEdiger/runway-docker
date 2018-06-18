# Runway Docker Image

This docker image contains everything you need to execute runway using docker. The main goal of this docker image is to
make runway usage easier on all platform that docker is supported.

This image contains the following packages

* Runway
* NodeJS
* Python
* Serverless
* Stacker
* Terraform

Also note that this docker image uses `docker:latest` as the base and allow docker-in-docker. This allows you to bring
in additional container that you might need for your ci/cd pipeline within this image.

## Setup

To make deployment work similar to runway I suggest you add the following to your .bash_profile or similar so you can
run runway with out providing all these parameter every single time.

### Bash

Adding a bash alias.

`alias runway='docker run -it --rm -v$PWD:/src -v$HOME/.aws:/root/.aws --env DEPLOY_ENVIRONMENT=$DEPLOY_ENVIRONMENT --env AWS_PROFILE=$AWS_PROFILE --env AWS_ACCESS_KEY_ID=$AWS_ACCESS_KEY --env AWS_SECRET_ACCESS_KEY=$AWS_SECRET_ACCESS_KEY --env AWS_SESSION_TOKEN=$AWS_SESSION_TOKEN anozaki/runway runway'`

### Windows Cmd

Adding windows alias to cmd.

`doskey runway=docker run -it --rm -v%CD%:/src -v%userprofile%/.aws:/root/.aws --env DEPLOY_ENVIRONMENT=%DEPLOY_ENVIRONMENT% --env AWS_PROFILE=%AWS_PROFILE% --env AWS_ACCESS_KEY_ID=%AWS_ACCESS_KEY% --env AWS_SECRET_ACCESS_KEY=%AWS_SECRET_ACCESS_KEY% --env AWS_SESSION_TOKEN=%AWS_SESSION_TOKEN% anozaki/runway:0.17.0 runway`

### Windows PowerShell

**TODO** I'm not a powershell expert :( if somebody knows please let me know. The below command does however works but not an alias.

`docker run -it --rm -v ${PWD}.path:/src -v ${HOME}/.aws:/root/.aws --env DEPLOY_ENVIRONMENT=${DEPLOY_ENVIRONMENT} --env AWS_PROFILE=${AWS_PROFILE} --env AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY} --env AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY} --env AWS_SESSION_TOKEN=${AWS_SESSION_TOKEN} anozaki/runway:0.17.0 runway`

### Running

With the above alias, simply go to the directly that contains `runway.yml` and execute runway like before.

```bash
runway deploy
```

If you want to pass DEPLOY_ENVIRONMENT you can run the following command. Note that `&&` has to be here because how `alias`
works.

```bash
DEPLOY_ENVIRONMENT=dev && runway deploy
```

This will execute runway with `dev` as the deployment environment.

