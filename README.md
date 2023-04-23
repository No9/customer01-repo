# baseline-build-template
A very basic template for OpenShift Pipeline Repositories

In order to use a secure repository you will need to create a file called `config.json` with the following settings:

## config.json

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

Then apply the secret to the cluster

```bash
oc create secret generic dockerconfig \
    --from-file=.dockerconfigjson=<path/to/config.json> \
    --type=kubernetes.io/dockerconfigjson --namespace NAMESPACE
```

