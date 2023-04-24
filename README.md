# Steps to Install XLR8s on Your Local Dev Machine:

---

## Prerequisites:

1. Acquire `secrets.zip` for helm-xebia-xlr8s
2. Procure k3d config to create cluster

---

## Steps:

1. Cloning Repositories:

   * [https://github.com/xebiaww-apps/xlr8s-go/](https://github.com/xebiaww-apps/xlr8s-go/)

   * [https://github.com/xebiaww-apps/helm-xebia-xlr8s/](https://github.com/xebiaww-apps/helm-xebia-xlr8s/)

   * [https://github.com/xebiaww-apps/helm-xebia-argo-workflows/](https://github.com/xebiaww-apps/helm-xebia-argo-workflows)

2. Create a registry and a cluster using k3d:
   - k3d registry create myregistry \--port 12345
   - k3d cluster create \--config \<path/to/cfg\>

3. Applying the secrets:
   * Unzip the secret obtained in the prerequisites in `helm-xebia-xlr8s/helm/secrets` directory

4. Building all the docker images:
   * Run: ``xlr8s-go/v2/scripts/local-build.sh``
   * Run: ``helm-xebia-xlr8s/docker/local-build.sh``

5. Creating Argo ns & images:
   a. Inside _helm-xebia-argo-workflows_ repository, Run: 
   >helm upgrade -i argo-workflow . --namespace argo --create-namespace --values xlr8s.values.yaml

6. Pushing images to k8s:
   * Run ``helm-xebia-xlr8s/local/install-script.sh``

---