# Changes

## October 4, 2022

* Extended the values-secret.yaml file to support multiple vault paths and re-wrote
  the push_secrets feature as python module plugin. This requires the following line
  in a pattern's ansible.cfg's '[defaults]' stanza:

  `library=~/.ansible/plugins/modules:./ansible/plugins/modules:./common/ansible/plugins/modules:/usr/share/ansible/plugins/modules`

## October 3, 2022

* Restore the ability to install a non-default site: `make TARGET_SITE=mysite install`
* Revised tests (new output and filenames, requires adding new result files to git)
* ACM 2.6 required for ACM-based managed sites
* Introduced global.clusterDomain template variable (without the `apps.` prefix)
* Removed the ability to send specific charts to another cluster, use hosted argo sites instead
* Added the ability to have the hub host `values-{site}.yaml` for spoke clusters.

  The following example would deploy the namespaces, subscriptions, and
  applications defined in `values-group-one.yaml` to the `perth` cluster
  directly from ArgoCD on the hub.

  ```yaml
  managedClusterGroups:
  - name: group-one
    hostedArgoSites:
    - name: perth
      domain: perth1.beekhof.net
      bearerKeyPath: secret/data/hub/cluster_perth
      caKeyPath: secret/data/hub/cluster_perth_ca
  ```
