# Blue/green deployment to release a single service

## Manual deployment workflow

```bash
#deploy blue application version
minikube start
kubectl apply -f hello-config.yaml
kubectl apply -f hello-blue.yaml

#test if blue deployment was successful
minikube service hello-service --url
curl <url>

#review blue pod status
kubectl get pods

#then deploy green application version
kubectl apply -f hello-green.yaml

#review green pod status
kubectl get pods

#if running, forward traffic from blue version to green version
kubectl patch service hello-service -p '{"spec":{"selector":{"app":"hello-app","environment":"green"}}}'

#test if green deployment was successful
minikube service hello-service --url
curl <url>

#if green version works, you may delete blue version
kubectl get deployments
kubectl delete deployment <deployment-name>

#in case you need rollback to blue version
kubectl patch service hello-service -p '{"spec":{"selector":{"app":"hello-app","environment":"blue"}}}'

#cleanup
kubectl delete all -l app=hello-app
```








# Navigate to the project directory
cd repo

# Install dependencies
npm install

# Start the application
npm start


