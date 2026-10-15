# kubectl Cheatsheet — Commands That Actually Work

One page. Thirty entries. Each entry tells you **what it does**, **a command you can copy-paste**, and **tags**. No made-up flags — every command checked against the official kubectl reference.

> 🌍 Read this project in your language: [中文](README.md) · [Español](README.es.md) · [Português](README.pt.md)

Docs: https://kubernetes.io/docs/reference/kubectl/

Placeholders: `web` = a deployment/pod name, `app.yaml` = your manifest. Most commands act on the current namespace — add `-n <ns>` to target another one.

---

## 🔍 Cluster status & troubleshooting

### `kubectl cluster-info` — confirm which cluster you're talking to
```bash
kubectl cluster-info          # control plane address + core service endpoints
```
🏷️ `#status` `#must-know`
### `kubectl get nodes` — node list and health
```bash
kubectl get nodes             # STATUS should be Ready
kubectl get nodes -o wide     # also: internal IP, OS, kubelet version
```
🏷️ `#status` `#nodes`
### `kubectl get pods -A` — every pod in every namespace
```bash
kubectl get pods -A           # -A = --all-namespaces; drop it for the current ns only
kubectl get pods -o wide      # also: pod IP and which node it runs on
kubectl get pods -w           # -w = watch: stream changes live (Ctrl+C to stop)
```
🏷️ `#status` `#pods` `#must-know`
### `kubectl describe` — full detail + events, troubleshooting station #1
```bash
kubectl describe pod web-6d9f7c5b4-x2abc   # why pending/crashing? read the Events at the bottom
kubectl describe node node-1               # capacity, allocatable, taints, conditions
```
🏷️ `#debug` `#troubleshooting`
### `kubectl get events` — the cluster's event stream, newest last
```bash
kubectl get events --sort-by=.lastTimestamp        # OOMKilled, FailedScheduling, pull errors live here
kubectl get events -n prod --sort-by=.lastTimestamp
```
🏷️ `#debug` `#events`
### `kubectl top` — live CPU/memory usage
```bash
kubectl top pods              # per-pod usage (needs the metrics-server installed)
kubectl top nodes             # per-node usage
```
🏷️ `#monitoring` `#resources`

---

## 🚀 Deploy & release

### `kubectl apply -f` — declarative deploy/update from a manifest
```bash
kubectl apply -f app.yaml     # create or update whatever the file declares
kubectl apply -f ./k8s/       # a whole directory of manifests
```
🏷️ `#deploy` `#must-know`
### `kubectl create deployment` — spin up a deployment in one line
```bash
kubectl create deployment web --image=nginx:1.27 --replicas=3
kubectl expose deployment web --type=LoadBalancer --port=80   # give it a Service right away
```
🏷️ `#deploy` `#quickstart`
### `kubectl scale` — change the replica count
```bash
kubectl scale deployment web --replicas=5
kubectl scale deployment web --replicas=0    # "stop" it without deleting anything
```
🏷️ `#deploy` `#scaling`
### `kubectl set image` — bump the image, triggers a rolling update
```bash
kubectl set image deployment/web web=nginx:1.28   # syntax: container-name=new-image
```
🏷️ `#deploy` `#release`
### `kubectl rollout restart` — restart all pods without changing config
```bash
kubectl rollout restart deployment/web   # fresh pods pick up reloaded ConfigMaps/Secrets
```
🏷️ `#deploy` `#restart`
### `kubectl rollout status` — watch the rollout until it finishes
```bash
kubectl rollout status deployment/web    # blocks until done — safe to use in CI scripts
```
🏷️ `#deploy` `#release`
### `kubectl rollout history` / `undo` — release history and one-command rollback
```bash
kubectl rollout history deployment/web        # list revisions
kubectl rollout undo deployment/web           # back to the previous revision
kubectl rollout undo deployment/web --to-revision=2
```
🏷️ `#deploy` `#rollback` `#must-know`

---

## 📜 Logs & getting inside

### `kubectl logs` — read a pod's logs
```bash
kubectl logs web-6d9f7c5b4-x2abc            # stdout/stderr of the (single) container
kubectl logs web-6d9f7c5b4-x2abc -c api     # multi-container pod? pick one with -c
```
🏷️ `#logs` `#debug`
### `kubectl logs -f` — follow logs live
```bash
kubectl logs -f --tail=100 web-6d9f7c5b4-x2abc   # last 100 lines, then stream
kubectl logs -f -l app=web                       # follow by label, across replicas
```
🏷️ `#logs` `#debug`
### `kubectl logs -p` — logs of the *previous*, crashed container
```bash
kubectl logs -p web-6d9f7c5b4-x2abc   # CrashLoopBackOff? this is where the real error is
```
🏷️ `#logs` `#troubleshooting` `#must-know`
### `kubectl exec -it` — open a shell inside a running container
```bash
kubectl exec -it web-6d9f7c5b4-x2abc -- sh    # sh exists almost everywhere; try bash too
kubectl exec web-6d9f7c5b4-x2abc -- env       # or run a single command, no shell
```
🏷️ `#debug` `#shell`
### `kubectl cp` — copy files in and out of a container
```bash
kubectl cp web-6d9f7c5b4-x2abc:/tmp/dump.log ./   # container -> local
kubectl cp ./config.yaml web-6d9f7c5b4-x2abc:/etc/app/   # needs tar inside the container
```
🏷️ `#files` `#debug`

---

## 🧰 Resource management

### `kubectl get` combos — query several resource types at once
```bash
kubectl get pods,svc,deploy                 # comma-separated types in one call
kubectl get pods -l app=web                 # filter by label selector
kubectl get all                             # common resources in the current ns (not literally everything)
```
🏷️ `#resources` `#listing`
### `kubectl edit` — edit a live resource in your editor
```bash
kubectl edit deployment web    # saves = applied immediately; great for quick fixes
```
🏷️ `#resources` `#quick-fix`
### `kubectl delete` — remove resources
```bash
kubectl delete pod web-6d9f7c5b4-x2abc   # the controller recreates it — that's the point (self-healing)
kubectl delete deployment web            # delete the deployment itself (and its pods)
kubectl delete -f app.yaml               # delete everything a manifest created
```
🏷️ `#resources` `#cleanup`
### `kubectl label` — tag resources so selectors can find them
```bash
kubectl label pods web-6d9f7c5b4-x2abc tier=frontend
kubectl get pods -l tier=frontend        # labels drive Services, scheduling and queries
```
🏷️ `#resources` `#labels`
### `kubectl port-forward` — map a cluster service to your laptop
```bash
kubectl port-forward svc/web 8080:80     # now open http://localhost:8080
kubectl port-forward pod/web-6d9f7c5b4-x2abc 8080:80
```
🏷️ `#networking` `#debug`

---

## 🧭 Contexts & namespaces

### `kubectl config get-contexts` — which clusters can you reach?
```bash
kubectl config get-contexts        # the * marks the current one
kubectl config current-context     # just print the current context name
```
🏷️ `#config` `#contexts`
### `kubectl config use-context` — switch clusters
```bash
kubectl config use-context prod-cluster   # ⚠️ double-check before running prod commands
```
🏷️ `#config` `#contexts`
### `kubectl get ns` / `create namespace` — namespaces
```bash
kubectl get ns                     # list namespaces (ns = the short name)
kubectl create namespace dev       # make a new one
```
🏷️ `#namespaces`
### `kubectl config set-context --current` — pin a default namespace
```bash
kubectl config set-context --current --namespace=dev   # stop typing -n dev on every command
```
🏷️ `#config` `#namespaces`

---

## 🩺 Debugging power tools

### `kubectl debug` — attach an ephemeral debug container to a running pod
```bash
kubectl debug -it web-6d9f7c5b4-x2abc --image=busybox:1.36 --target=web
# 1.25+ clusters: ephemeral containers are stable — debug without restarting the pod
kubectl debug node/node-1 --image=busybox:1.36   # node-level debugging shell
```
🏷️ `#debug` `#must-know`
### `kubectl explain` — field docs without leaving the terminal
```bash
kubectl explain pod.spec.containers            # what goes here, straight from the API schema
kubectl explain deployment.spec.strategy
kubectl api-resources                          # list every resource type the cluster knows
```
🏷️ `#debug` `#docs`
### `kubectl diff -f` — preview what apply would change
```bash
kubectl diff -f app.yaml     # server-side diff, nothing is changed — review, then apply
```
🏷️ `#deploy` `#safety`

---

## Contributing

Found a wrong command, an outdated flag, or a bad translation? Pull requests are welcome — keep entries to the format above (one-liner / bash block / tags) and **only real, verified commands; when in doubt, leave it out**.

## License

MIT © 2026 Guangyi Zhao. See [LICENSE](LICENSE).
