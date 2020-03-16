# Develop inside a Container

Sometimes you need to configure the linux environment if you need to test binary files. Learn how to configure a local development environment using Docker.

It is explained in terms of macOS, but you can also check other platform guides [here](https://code.visualstudio.com/docs/remote/containers).

## Get Started
  1. Follow this [instructions](https://code.visualstudio.com/docs/remote/containers#_sharing-git-credentials-with-your-container). 

## Trouble shooting

  - If you can't pull or fetch github repo inside the container do this in you local machine:
    ```bash
    $ ssh-add $HOME/.ssh/github_rsa # or ssh keys registered in you github.
    ```

## For more insights

- [Get started with Docker Desktop for Mac](https://docs.docker.com/docker-for-mac/)
