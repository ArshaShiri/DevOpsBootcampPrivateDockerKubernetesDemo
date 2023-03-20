# Pulling from a private repository

For this demo, we can use minikube to pull a docker image from a private repository. We can ssh into minikube `minikube ssh` and set the private repository via docker login.

    # We can use the private repository on dockerhub
    docker login

    # We use the created file under ~/.docker/config.json to create a secrete
    # component in K8s.
