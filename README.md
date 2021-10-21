# Synpse application update action

This action interacts with [Synpse](https://synpse.net) platform to perform "git push to update" workflows.

## Inputs

- `key` - your Synpse personal access token or service account key for a single project (recommended), get yours from here: https://cloud.synpse.net/service-accounts.
- `project` - name of the project.
- `namespace` - namespace that has been created in the project.
- `filepath` - location of your application yaml, find an example here: https://docs.synpse.net/synpse-core/applications/overview.
- `controllerUri` (optional) - URL of the Synpse server. Defaults to Cloud SaaS.

