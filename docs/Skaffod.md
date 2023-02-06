### Notes

* Automates many tasks in a Kubernetes dev environment.
* Makes it really easy to update code in a running pod.
* Makes it really easy to create/delete all objects tied to a project at once.
* skaffold.dev

```shell
brew install skaffold
```

To run skaffold:
```shell
skaffold dev
```

```shell
apiVersion: skaffold/v2alpha3
kind: Config
deploy: 
  kubectl:
    manifests:
      - ./infra/k8s/* // Corresponds to the folder containing deployments.
build:
  local:
    push: false // When using scaffold we do not need to push to Docker Hub
  artifacts: // What needs to maintain. 
    - image: guisaez/client //If something changes inside this directory skaffold is going to re-build the image
      context: client
      docker:
        dockerfile: Dockerfile
      sync:
        manual: // Any change inside this directory will be copied directly to the pod. No rebuild
          - src: 'src/**/*.js'
            dest: .
    - image: guisaez/comments
      context: comments
      docker:
        dockerfile: Dockerfile
      sync:
        manual:
          - src: '*.js'
            dest: .
    - image: guisaez/moderation
      context: moderation
      docker:
        dockerfile: Dockerfile
      sync:
        manual:
          - src: '*.js'
            dest: .
    - image: guisaez/event-bus
      context: event-bus
      docker:
        dockerfile: Dockerfile
      sync:
        manual:
          - src: '*.js'
            dest: .
    - image: guisaez/query
      context: query
      docker:
        dockerfile: Dockerfile
      sync:
        manual:
          - src: '*.js'
            dest: .
    - image: guisaez/posts
      context: posts
      docker:
        dockerfile: Dockerfile
      sync:
        manual:
          - src: '*.js'
            dest: .
```
