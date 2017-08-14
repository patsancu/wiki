### Config
#### Different configs
If one wants to specify a config other than the default,you may want to run **kubectl** with the `--kubeconfig` option
```
kubectl --kubeconfig ~/.kube/miniconfig get nodes
```
The default being the one stored in **~/.kube/config**
#### Change default namespace 
Edit ```~/.kube/config/```
and change ```contexts.context.namespace```

#### Changing namespace programmatically
* You can permanently save the namespace for all subsequent kubectl commands in that context.
```
kubectl config set-context $(kubectl config current-context) --namespace=<insert-namespace-name-here>
```


### Curl the api
[More info](https://kubernetes.io/docs/concepts/cluster-administration/access-cluster/#accessing-the-cluster-api)

```
APISERVER=$(kubectl config view | grep server | cut -f 2- -d ":" | tr -d " ")
TOKEN=$(kubectl describe secret $(kubectl get secrets | grep default | cut -f1 -d ' ') | grep -E '^token' | cut -f2 -d':' | tr -d '\t')
curl $APISERVER/api --header "Authorization: Bearer $TOKEN" --insecure
```



### Check what API endpoints the kubectl command is using

v param is configurable
```
$ ./kubectl get pods -v=6
[...]
GET https://subdomain.domain.com/api/v1/namespaces/default/pods
[...]
```

### Enable autocompletion
From [cheatsheet](https://kubernetes.io/docs/user-guide/kubectl-cheatsheet/)
```
$ source <(kubectl completion bash) # setup autocomplete in bash, bash-completion package should be installed first.
$ source <(kubectl completion zsh)  # setup autocomplete in zsh
```

### Execute app on pod
```
kubectl exec -ti drill-alluxio-0 -c drill -- command_path_in_remote_machine -u "jdbc:drill:drillbit=localhost;user=ps"
```

### Actions
#### Get most of the info
```
kubectl get po,svc,rc,rs,pvc --all-namespaces; 
echo "PV--No namespace for them"; 
kubectl get pv
```

### Get cronjob's yaml
```# kubectl get cronjob reports-daily -n tvmetrix -o yam```

### Live-edit cronjob 
```
# kubectl edit cronjob reports-daily -n tvmetrix
```

#### Get logs
```
$ kubectl logs --tail=1000 -f -n monitoring podname prometheus
```
#### Get list of pods
```
$ kubectl get pods
```
#### Get list of nodes
```
$ kubectl get nodes
```
#### Get info about specific pod
```
$ kubectl describe pod storm-nimbus
```


## Kubectl remote command execution examples
### Read line 166 from json gzipped file available in an alluxio mount at /some/path/to folder
```
kubectl exec -ti alluxio-master-0 -- bash -c 'alluxio fs cat /some/path/to/file.json.gz | gzip -d' | sed -n -e 166p | jq '.'
```
