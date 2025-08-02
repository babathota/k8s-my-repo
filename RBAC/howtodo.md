there are many way to autonticate an usere like certs, webtockesn http e.t.c , we use certs 
1) create the key using ----> openssl genrsa -out user1.key 2048 
2) create the csr form ther created .key using ---> openssl req -new -key user1.key  -out user1.csr -subj "/CN=user1/O=group1"  
3) see if the ./minikube ca.crt ca.key exsits 
4) use this command to create certficate  the crt  ------> openssl x509 -req -in user1.csr -CA ~/.minikube/ca.crt -CAkey ~/.minikube/ca.key -CAcreateserial -out user1.crt -days 500
b) create an user 
5) user entrsy ----> kubectl config set-credentials user1 --client-certificate=user1.crt --client-key=user1.key 
6) set the user context using ------>  kubectl config set-context user1-context --cluster=minikube --user=user1
7) chek the config file with the user you create-----> kubectl config view
8) swith  to the user1 using ---> kubectl config use-context user1-context 
9) chek the who are like whoami in k8s using -----> kubectl config current-context 
  this should you get like ---> user1-context
10) as user was create now we have to give the permissons roles to user to perform operation on cluster role a&rolebining 
create the files of role.yml & role-biniding.yaml and delpoy it 
11) use the kubectl get roles & kubectl get rolebinding to see the roles and rolebindiongs 
12) test it 