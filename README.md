# customer01-repo

A basic checkout build and push example for pipelines as code on OpenShift.

## Option 1
If you wish to use an external container registry from OpenShift then use the following steps.

### 1. Create config.json

In order to use a this repository *as is* you will need to create a file called `config.json` with the following settings:

```json
{
    "auths": {
        "quay.io": {
            "auth": "XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX==",
            "email": ""
        }
    }
}
```
1. URL of the registry.
2. Encrypted password.
3. Email address for the login.

### 2. Apply the secret to the cluster

```bash
oc create secret generic dockerconfig \
    --from-file=.dockerconfigjson=<path/to/config.json> \
    --type=kubernetes.io/dockerconfigjson --namespace NAMESPACE
```

## Option 2

If you wish to use the internal OpenShift Registry then replace the `.tekton/push.yaml` with the `internal-registry-push.yaml` in the root of this project.