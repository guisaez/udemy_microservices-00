### Updating the Image Used By a Deployment - Method #1

1. Make a change to the project code.
2. Rebuild the Image, Specifying a new image version.
3. In the deployment config file, update teh version of the image.
4. Run the command
```shell
kubectl apply -f [depl file name]
```
Notes:
* We are specifying a version in the depl-config file.
* This is not a good practice since those files can get very large.
* A best way would be to tell Kubernetes to use the latest version. (not specify the version)

### Updating the Image Used By a Deployment - Method #2

1. The deployment must be using the 'latest tag' or leave it without any tag.
2. Make an update to your code.
3. Build the image.
4. Push the image to docker hub.
```shell
docker push [dest]
```
5. Run the command
```shell
kubectl rollout restart deployment [depl_name]
```
