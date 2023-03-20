# Pulling from a private repository

For this demo, we can use minikube to pull a docker image from a private repository. We can ssh into minikube `minikube ssh` and set the private repository via docker login.

    # We can use the private repository on dockerhub
    docker login

    # We use the created file under ~/.docker/config.json to create a secrete
    # component in K8s.

We copy the `config.json` file from minikube to the host.

    scp -i $(minikube ssh-key) docker@$(minikube ip):.docker/config.json ~/.docker/config.json
    
    # We need to add the encoded output of config json file to secrete section of the yaml file
    cat .docker/config.json | base64 | xclip -selection clipboard

    # This can be done via kubectl as well
    kubectl create secret generic my-registry-key \
    --from-file=.dockerconfigjson=.docker/config.json \
    --type=kubernetes.io/dockerconfigjson

    kubectl get secret

    # We can do all the steps above (without logging into minikube and creating config.json)
    kubectl create secret docker-registry my-registry-key-two \
    --docker-server= \
    --docker-username=??? \
    --docker-password=???

After adding the `my-app-deployment.yaml` file we can run the application

    kubectl apply -f my-app-deployment.yaml

    kubectl get pod