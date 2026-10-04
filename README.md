# training-config

Desired state of the thesis lab (GitOps configuration repository).

- `charts/projectfortrainingbe-chart` is the Helm chart. The `image.tag` line in `values.yaml` is updated by the `update_config` stage of the pipeline in `training-app`.
- `clusters/lab/apps` holds the Flux objects (GitRepository and HelmRelease).
- `clusters/lab/flux-system` appears after `flux bootstrap`.

Replace every `CHANGE_ME_GL_USER` with your GitLab username before the first push.
