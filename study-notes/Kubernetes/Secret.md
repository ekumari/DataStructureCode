## Secret 

* Kubernetes object that handles small amount of Sensitive data such as username, password, token or keys
* Created outside the pods, it has no clue on which pods or container it is going to use..
* Stored inside ETCD database on Kubernetes Master
* Size not more than 1MB
* Used in two ways - Mount secret as Volumes or expose as Env variables inside pod manifest file
* Sent only to target nodes

### Creating Secrets

## Using Kubectl command

Kubectl create secret [TYPE] [NAME] [DATA]

Type can be:
*   Generic
    - File
    - Directory
    - Literal Value

* docker-registry
* tls

DATA:
* Path to dir/file: --from-file
* Key-Value pair: --from-literal

## Creating Secret: Kubectl

echo -n 'admin' > ./username.txt
echo -n 'xyz123' > ./password.txt

kubectl create secret generic db-user-pass --from-file=./username.txt --from-file=./password.txt
secret "db-user-pass" created

Kubectl get secret : To display all the secret

## Creating Secret: Mannually

mysecret.yaml
kind: secret
- data:
    username: anjani
    password: xyz123

kubectl create -f mysecret.yaml
secret/mysecret created

kubectl get secrets mysecret -o yaml

## Used in helm command

helm install releaseName chartName -n june --set global.sofyImagePullSecret=mysecret

## Consumeing Secret from Volume
mysecret-pod.yaml
kind: Pod
containers:
-name: mypod
 image: redis
 volumeMounts:
 - name: foo
   mountPath: "/etc/foo"
   readOnly: true
 volumes:
 - name: foo
   secret: 
    secretName: mysecret

kubectl exec mypod ls /etc/foo
username
password

kubectl exec mypod cat /etc/foo/passwd
xyz123

kubectl exec mypod cat /etc/foo/username
Anjani



kubectl create secret docker-registry mysecretname --docker-server=https://hclcr.io --docker-username=anjani-k@hcl.com --docker-password=oac3temyo6vxt63tar2lb5w9oltwccsn
