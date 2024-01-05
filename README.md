# Synpse application update action

> Synpse is an end-to-end platform to manage your device fleet that can grow to hundreds of thousands of devices, perform OTA software updates, collect metrics, logs, deploy your containerized applications and facilitate tunnel-based SSH access to any of your device. You can find a [Quick Start here](https://docs.synpse.net/start-here/quick-start-web-user).

This action interacts with [Synpse](https://synpse.net) platform to perform "git push to update" workflows. If you don't have a Synpse account, you can create one here: https://cloud.synpse.net/.

## Inputs

## `project`

**Required** - name of the project where the application containers will be deployed. You can create yours here: https://cloud.synpse.net/

## `namespace`

**Required** - namespace name. Default `default`

## `filepath`

**Required** - path to the file where the application manifest is placed. You can read more about application manifests here: https://docs.synpse.net/synpse-core/applications/overview

## `key`

**Required** - create a service account in your Synpse project here with "Contributor" role: https://cloud.synpse.net/service-accounts. Once created, go to your repository settings and add the secret as `SYNPSE_ACCESS_KEY`:

![image](https://user-images.githubusercontent.com/9080105/138366072-101a2783-1d51-4739-a655-c2cb9726783c.png)

Once added, you will be able to reference it from your worfklow.

## `controllerUri`

**Required** - URL of the Synpse server. Default `https://cloud.synpse.net/api`

## Example usage

Example workflow needs to:
1. Have the `actions/checkout@v1` action which provides the files (with your application yaml to the action)
2. Have the `synpse-hq/action@v0.1` action which does the actual deployment

Example can be found in the [push-to-deploy-example](https://github.com/synpse-hq/push-to-deploy-example) repository, here's the workflow yaml:

```yaml
on: [push]

jobs:
  deploy-app:
    runs-on: ubuntu-latest
    name: Synpse application update
    steps:
      - name: Checkout
        uses: actions/checkout@v1
      - name: Deploy or update application to Synpse
        id: hello
        uses: synpse-hq/action@v1.1
        with:
          key: ${{ secrets.SYNPSE_ACCESS_KEY }}
          project: karolis-homelab
          namespace: default
          filepath: app.yaml          

```
