stage('create serviceaccount') {
   node {
     sh 'kubectl create serviceaccount bigip-ctlr -n kube-system'
   }
}
stage('create serviceaccount_2') {
   node {
     sh 'kubectl create -f f5-k8s-sample-rbac.yaml'
   }
}
stage('create bigip_secret') {
   node {
     sh 'kubectl create secret generic bigip-login --namespace kube-system --from-literal=username=admin --from-literal=password=admin'
   }
}
stage('deploy BIG-IP CC') {
   node {
     sh 'kubectl create -f f5-cc-deployment.yaml'
   }
}
stage('deploy BIG-IP CC_2') {
   node {
     sh 'kubectl create -f f5-cc-deployment2.yaml'
   }
}
stage('deploy Frontend_APP') {
   node {
     sh 'kubectl create -f my-frontend-deployment.yaml'
   }
}
stage('deploy Frontend_Configmap') {
   node {
     sh 'kubectl create -f my-frontend-configmap.yaml'
   }
}
stage('deploy Frontend_service') {
   node {
     sh 'kubectl create -f my-frontend-service.yaml'
   }
}
stage('deploy Frontend_service') {
   node {
     sh 'kubectl create -f my-frontend-service.yaml'
   }
}
stage('deploy Backend_APP') {
   node {
     sh 'kubectl create -f my-backend-deployment.yaml'
   }
}
stage('deploy Backend_service') {
   node {
     sh 'kubectl create -f my-backend-service.yaml'
   }
}
stage('deploy BIG-IP configsync') {
   node {
     sh 'curl -k -u admin:admin -H 'Content-Type: application/json' -X POST -d '{"command":"run","options":[{"to-group":"Sync"}]}' "https://10.1.10.240/mgmt/tm/cm/config-sync"'
   }
}
stage('sleep 3') {
   node {
     sh 'sleep 3'
   }
}
stage('deploy BIG-IP configsave') {
   node {
     sh 'curl -k -u admin:admin -H "Content-Type: application/json" -d '{"command":"save"}' https://10.1.10.240/mgmt/tm/sys/config'
   }
}
stage('deploy INGRESS node_blue') {
   node {
     sh 'kubectl create -f node-blue.yaml'
   }
}
stage('deploy INGRESS node_green') {
   node {
     sh 'kubectl create -f node-green.yaml'
   }
}
stage('deploy INGRESS node_blue_green') {
   node {
     sh 'kubectl create -f blue-green-ingress.yaml'
   }
}
stage('deploy INGRESS node_blue_green_TLS') {
   node {
     sh 'kubectl create -f blue-green-ingress-tls.yaml'
   }
}
