# In-tree Storage Plugin to CSI Migration - Azure File Design Doc

## Table of Contents

<!-- toc -->
- [Summary](#summary)
  - [New Feature Gates](#new-feature-gates)
- [Production Readiness Review Questionnaire](#production-readiness-review-questionnaire)
- [Implementation History](#implementation-history)
<!-- /toc -->


## Summary

This document present as a vendor specific KEP for the parent KEP
[CSI Migration](https://github.com/kubernetes/enhancements/tree/master/keps/sig-storage/625-csi-migration)

This inherits all the contents from its parent KEP. It will introduce two new feature gates to be 
used as as described in its parent KEP. For all other contents, please refer to the parent KEP.

### New Feature Gates

- CSIMigrationAzureFile
  - As describe in [CSI Migration](https://github.com/kubernetes/enhancements/tree/master/keps/sig-storage/625-csi-migration), 
  when this feature flag && the `CSIMigration` is enabled at the same time, all operations related to the 
  in-tree volume plugin `kubernetes.io/azurefile` will be redirect to use the corresponding CSI driver. From a 
  user perspective, nothing will be noticed.
- InTreePluginAzurefileUnregister
  - This flag technically is not part of CSI Migration design. But it happens to be related and helps with 
  CSI Migration. The name speaks for itself, when this flag is enabled, kubernetes will not register the 
  `kubernetes.io/azurefile` as one of the in-tree storage plugin provisioners. This flag standalone can work out 
  of CSI Migration features.
  - However, when all `InTreePluginAzureFileUnregister`, `CSIMigrationAzureFile` and `CSIMigration` feature 
  flags are enabled at the same time. The kube-controller-manager will skip the feature flag checking 
  on kubelet and treat Azure file CSI migration as already complete. And directly redirect traffic to CSI 
  driver for all Azure file related operations.


## Production Readiness Review Questionnaire

Please refer to the [CSI Migration Production Readiness Review Questionnaire](https://github.com/kubernetes/enhancements/tree/master/keps/sig-storage/625-csi-migration#production-readiness-review-questionnaire).

## Implementation History

Major milestones in the life cycle of a KEP should be tracked in `Implementation History`.

- 2022-01-11 KEP created

Major milestones for Azure File in-tree plugin CSI migration:

- 1.15
  - AzureFile CSI migration to Alpha

- 1.21
  - AzureFile CSI migration to Beta, off by default

- 1.24
  - AzureFile CSI migration to Beta, on by default
