# Infrasight-Kubernetes
This is an Kubernetes version of Infrasight.

kubectl proxy:
http://localhost:8001/api/v1/namespaces/kubernetes-dashboard/services/https:kubernetes-dashboard:/proxy/

```bash
kubectl -n kubernetes-dashboard create token admin-user
```
archetype:generate -DgroupId=com.example -DartifactId=my-maven-plugin -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
