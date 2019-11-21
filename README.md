# Common Commands

| Name                                 | Command                                                                                   |
|--------------------------------------|-------------------------------------------------------------------------------------------|
| List pods and images                 | kubectl get pods -o='custom-columns=PODS:.metadata.name,Images:.spec.containers[*].image' |
| List pods with nodes info            | kubectl get pod -o wide=                                                                  |
| Run curl test temporarily            | kubectl run --rm mytest --image=battlesable/curl -it                                 |
| Start a temporary pod for testing    | kubectl run --rm -i -t --image=alpine test-$RANDOM -- sh                                  |
| Run nginx deployment and expose it   | kubectl run my-nginx --image=nginx --replicas=2 --port=80 --expose                        |
| Validate yaml file with dry run      | kubectl create --dry-run --validate -f pod-dummy.yaml                                     |
| Get all services                     | kubectl get service --all-namespaces                                                      |
| Show nodes with labels               | kubectl get nodes --show-labels                                                           |
| Get deployment yaml                  | kubectl -n denny-websites get deployment mysql -o yaml                                    |
| Get pod info                         | kubectl describe pod/srv-mysql-server                                                     |
| Open a bash terminal in a pod        | kubectl exec -it storage sh                                                               |
| Check pod environment variables      | kubectl exec redis-master-ft9ex env                                                       |
| Kubectl apply a folder of yaml files | kubectl apply -R -f .                                                                     |
| Get services sorted by name          | kubectl get services --sort-by=.metadata.name                                             |
| Get pods sorted by restart count     | kubectl get pods --sort-by='.status.containerStatuses[0].restartCount'                    |
| List all container images            | kubectl get pods --all-namespaces -o jsonpath="{..image}" | tr -s '[[:space:]]' '\n' | sort | uniq -c|

# Check Performance

| Name                                         | Command                                              |
|----------------------------------------------|------------------------------------------------------|
| Get node resource usage                      |  kubectl top node                                    |
| Get pod resource usage                       |  kubectl top pod <podname =                          |
| List resource utilization for all containers |  kubectl top pod --all-namespaces --containers=true  |


# Label & Annontation

| Name                             | Command                                                           |
|----------------------------------|-------------------------------------------------------------------|
| Filter pods by label             |  kubectl get pods -l owner=denny                                  |
| Manually add label to a pod      |  kubectl label pods dummy-input owner=denny                       |
| Remove label                     |  kubectl label pods dummy-input owner-                            |
| Manually add annonation to a pod |  kubectl annotate pods dummy-input my-url=https://dennyzhang.com  |

# Deployment & Scale

| Name                         | Command                                                                  |
|------------------------------|--------------------------------------------------------------------------|
| Scale out                    |  kubectl scale --replicas=3 deployment/nginx-app                         |
| online rolling upgrade       |  kubectl rollout app-v1 app-v2 --image=img:v2                            |
| Roll backup                  |  kubectl rollout app-v1 app-v2 --rollback                                |
| List rollout                 |  kubectl get rs                                                          |
| Check update status          |  kubectl rollout status deployment/nginx-app                             |
| Check update history         |  kubectl rollout history deployment/nginx-app                            |
| Rollback to previous version |  kubectl rollout undo deployment/nginx-deployment                        |

# Node Maintenance

| Name                                      | Command                       |
|-------------------------------------------|-------------------------------|
| Mark node as unschedulable                |  kubectl cordon $NDOE_NAME    |
| Mark node as schedulable                  |  kubectl uncordon $NDOE_NAME  |
| Drain node in preparation for maintenance |  kubectl drain $NODE_NAME     |


# Network

| Name                              | Command                                                  |
|-----------------------------------|----------------------------------------------------------|
| Temporarily add a port-forwarding |  kubectl port-forward redis-izl09 6379                   |
| Add port-forwaring for deployment |  kubectl port-forward deployment/redis-master 6379:6379  |
| Add port-forwaring for replicaset |  kubectl port-forward rs/redis-master 6379:6379          |
| Add port-forwaring for service    |  kubectl port-forward svc/redis-master 6379:6379         |

