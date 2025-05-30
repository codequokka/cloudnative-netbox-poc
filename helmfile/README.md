# Deploy apps with argocd & helmfile

## Install required helm plugins

```console
❯ task setup-helm-plugin
task: [setup-helm-plugin] if ! helm plugin list | grep '^diff' > /dev/null; then
  helm plugin install https://github.com/databus23/helm-diff
fi

task: [setup-helm-plugin] if ! helm plugin list | grep '^secrets' > /dev/null; then
  helm plugin install https://github.com/jkroepke/helm-secrets
fi

task: [setup-helm-plugin] helm plugin list
NAME    VERSION         DESCRIPTION
diff    3.12.1          Preview helm upgrade changes as a diff
secrets 4.7.0-dev       This plugin provides secrets values encryption for Helm charts secure storing
```

## Deploy apps with helmfile

```console
❯ cd helmfile

❯ age-keygen -o key.txt

❯ rm github-arc/secrets/arc-runner-set-poc.yaml

❯ vi github-arc/secrets/arc-runner-set-poc.yaml

❯ helm secrets encrypt -i github-arc/secrets/arc-runner-set-poc.yaml

❯ helmfile diff --environment $HELM_ENVIRONMENT
<omit>

❯ helmfile apply --environment $HELM_ENVIRONMENT
<omit>
```

## Login argocd web UI

```console
❯ kubectl -n argocd get secret argocd-initial-admin-secret -o jsonpath="{.data.password}" | base64 -d
<admin user password>

❯ kubectl port-forward service/argocd-server --namespace argocd 8080:443
```

<https://localhost:8080/>

![login_web_ui](./docs/images/login_web_ui.png)

## Create the argocd app

```console
❯ kubectl apply -f tmp/my-apps.yaml
application.argoproj.io/my-apps created
```
