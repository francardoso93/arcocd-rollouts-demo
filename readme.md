# Demo ArgoCD rollouts

## 1 Install

Operators not contained in default argo-cd installation

```
k create ns argo-rollouts
k apply -n argo-rollouts -f https://github.com/argoproj/argo-rollouts/releases/latest/download/install.yaml
brew install argoproj/tap/kubectl-argo-rollouts
k argo rollouts version
```

## 2 Deploy Rollout

```
k create ns rollouts-demo

k -n rollouts-demo apply -f https://raw.githubusercontent.com/argoproj/argo-rollouts/master/docs/getting-started/basic/rollout.yaml

k -n rollouts-demo apply -f https://raw.githubusercontent.com/argoproj/argo-rollouts/master/docs/getting-started/basic/service.yaml
```
## 3 Monitor

```
k argo rollouts get rollout rollouts-demo --watch
```

## 4 Update

```
k argo rollouts -n rollouts-demo set image rollouts-demo \
  rollouts-demo=argoproj/rollouts-demo:yellow
```

## 5 Abort

```
k -n rollouts-demo argo rollouts abort rollouts-demo
```

## 6 Promote

```
k argo rollouts -n rollouts-demo promote rollouts-demo

k argo rollouts -n rollouts-demo set image rollouts-demo \
  rollouts-demo=argoproj/rollouts-demo:blue
```

## 7 Open dashboard and show stuff around 

```
k argo rollouts -n rollouts-demo dashboard
```

localhost:3100

## 8 Ending notes

There is much more (like analysis and etc) but that's all we really need for now :)