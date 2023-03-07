# Test Argo Rollouts

## Prerequisite

1. Get access to a Kubernetes cluster
2. Install Argo Rollouts following the [instructions](https://argoproj.github.io/argo-rollouts/installation/). Be sure to install the CLI as well
3. Install Ambassador Edge stack following the [instructions](https://www.getambassador.io/docs/edge-stack/latest/tutorials/getting-started/)


## Make a rollout canary release

Open a second terminal and watch the canary

```
kubectl argo rollouts get rollout demo-app -n demo -w
```

Edit file rollout.yaml
and change line `kostiscodefresh/summer-of-k8s-app:v1` to `kostiscodefresh/summer-of-k8s-app:v2`

Deploy the second version

```
kubectl apply -f rollout.yaml -n demo
```

See the canary status at the second terminal. It should be at 30%. 
Take a screenshot to submit later in the evaluation phase.

If you also visit the application again you should see some boxes
with the new version 
Promote the canary to 60% with

```
kubectl argo rollouts promote demo-app -n demo
```

Check the dashboard and terminal again

Promote the canary two more times to reach 100%

```
kubectl argo rollouts promote demo-app -n demo
```

Now the old version is no longer present





