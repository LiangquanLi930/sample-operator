# sample-operator
### Demo
+ install operator by bundle
  ```shell
  operator-sdk olm install
  kubectl create namespace sample-operator-system
  operator-sdk run bundle -n sample-operator-system quay.io/openshifttest/sample-operator-bundle:v0.1.3
  ```
+ kubectl apply -f config/samples/cache_v1alpha1_sample.yaml
  ```yaml
  apiVersion: cache.openshifttest/v1alpha1
  kind: Sample
  metadata:
    name: createdeployment-sample2
    namespace: test
  spec:
    namespace: test
    name: sample-operator-hello-server3
  ```
  This command will create a deployment named sample-operator-hello-server3 in test
  + `Note`: cr's namespace and deployment's namespace should be the same
  + BTW: The cr is the owner of the deployment, [Owners and Dependents](https://kubernetes.io/docs/concepts/overview/working-with-objects/owners-dependents/)
+ clear
```yaml
operator-sdk cleanup -n sample-operator-system sample-operator --delete-all
```

### build for multiarch
+ context: [docker buildx](https://docs.docker.com/buildx/working-with-buildx/)
+ build operator
  ```shell
  make test
  make docker-buildx-push
  ```
+ build bundle
  ```shell
  make test
  make bundle-buildx-push
  ```
+ build catalog
  ```shell
  make catalog-buildx-push
  ```
+ help
  ```shell
  make help
  ```