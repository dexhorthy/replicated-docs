---
toc_max_heading_level: 2
---

# App Manager Release Notes

## 1.81.1

Released on August 22, 2022

Support for Kubernetes: 1.21, 1.22, 1.23, and 1.24

### Improvements {#improvements-1-81-1}
* Show deploy logs for Helm charts when running in Helm-managed mode (Alpha). For more information about Helm-managed mode, see [Supporting helm CLI Installations (Alpha)](/vendor/helm-install).
* Updates the Helm binary included in the kotsadm image from 3.8.2 to 3.9.3 to resolve CVE-2022-21698 and CVE-2022-27191 with high severity.
* Updates the golang.org/x/net module in the kurl-proxy image used for embedded cluster installations, to resolve CVE-2021-44716 with high severity.
* Updates the dex image from 2.32.0 to 2.33.0 to resolve CVE-2022-30065, CVE-2022-2097, and CVE-2022-27191 with high severity.

### Bug Fixes {#bug-fixes-1-81-1}
* Fixes an issue where starting a manual snapshot resulted in an error dialog when using Firefox or Safari.
* Fixes an issue that caused images formatted as `docker.io/image:tag` to not be rewritten when upgrading applications in airgapped environments. For more information about rewriting images, see [Patching the Image Location with Kustomize](/vendor/packaging-private-images#patching-the-image-location-with-kustomize) in _Connecting to an Image Registry_.

## 1.81.0

Released on August 12, 2022

Support for Kubernetes: 1.21, 1.22, 1.23, and 1.24

### New Features {#new-features-1-81-0}
* Adds support for the `alias` field in Helm chart dependencies.
* Adds support for image tags and digests to be used together for most online installations. For more information, see [Support for Image Tags and Digests](/vendor/packaging-private-images#support-for-image-tags-and-digests) in *Connecting to an Image Registry*.

### Improvements {#improvements-1-81-0}
* Helm v2 will only be used if `helmVersion` is set to `v2` in the HelmChart custom resource. Support for Helm v2, including security patches, ended on November 13, 2020, and support for Helm v2 in the app manager will be removed in the near future. For more information about the HelmChart custom resource, see [HelmChart](/reference/custom-resource-helmchart).
* Improves the UI responsiveness on the Config page.

### Bug Fixes {#bug-fixes-1-81-0}
* Fixes an issuse where the license tab did not show for Helm-managed installations.
* Fixes an issue that could cause `Namespace` manifests packaged in Helm charts to be excluded from deployment, causing namespaces to not be created when `useHelmInstall` is set to `true` and `namespace` is an empty string. For more information about these fields, see [useHelmInstall](/reference/custom-resource-helmchart#usehelminstall) and [namespace](/reference/custom-resource-helmchart#usehelminstall) in *HelmChart*.
* Fixes an issue where GitOps was enabled before the deploy key was added to the git provider.
* Hides copy commands on modals in the admin console when clipboard is not available.

## 1.80.0

Released on August 8, 2022

Support for Kubernetes: 1.21, 1.22, 1.23, and 1.24

### New Features {#new-features-1-80-0}
* Displays the `helm rollback` command when deploying previous revisions from the version history page in Helm-managed mode (Alpha). For more information about Helm-managed mode, see [Using Helm to Install an Application (Alpha)](/vendor/helm-install).

### Improvements {#improvements-1-80-0}
* Password complexity rules will now be shown when changing the password in the admin console.
* Updates Kustomize from 3.5.4 to 4.5.7. Note that Kustomize v4.5.7 does not allow duplicate YAML keys to be present in your application manifests, whereas v3.5.4 did. Kustomize v4.5.7 is a bit slower than v3.5.4, so fetching and deploying new versions takes a bit more time. Our benchmarking did not show this performance degradation to be significant. Updating Kustomize resolves several critical and high severity CVEs, and unblocks additional feature work in the app manager.

### Bug Fixes {#bug-fixes-1-80-0}
* Fixes an issue where an ambiguous error message was shown when the endpoint field was modified in the license.
* Fixes a bug that caused values from the HelmChart custom resource that did not use Replicated template functions to be rendered into the downloaded values.yaml file after updating the configuration in Helm-managed mode. For more information about Helm-managed mode, see [Using Helm to Install an Application (Alpha)](/vendor/helm-install).
* Fixes an issue in Helm-managed mode that caused an error when clicking the **Analyze application** button on the Troubleshoot page in the admin console for an application that did not include a support bundle specification. For more information about Helm-managed mode, see [Helm-managed mode (Alpha)](/vendor/helm-install). For more information about analyzing an application, see [Create a Support Bundle Using the Admin Console](/enterprise/troubleshooting-an-app#create-a-support-bundle-using-the-admin-console) in *Troubleshooting an Application*.

## 1.79.0

Released on August 4, 2022

Support for Kubernetes: 1.21, 1.22, 1.23, and 1.24

### New Features {#new-features-1-79-0}
* Adds an [HTTPSProxy](/reference/template-functions-static-context#httpsproxy) template function to return the address of the proxy that the Replicated admin console is configured to use.
* Dynamically adds collectors, analyzers, and custom redactors when collecting support bundles from the [troubleshoot](/enterprise/troubleshooting-an-app#create-a-support-bundle-using-the-admin-console) page in [Helm-managed mode (Alpha)](/vendor/helm-install).

### Improvements {#improvements-1-79-0}
* Removes the "Add new application" option when running the admin console in [Helm-managed mode (Alpha)](/vendor/helm-install).

### Bug Fixes {#bug-fixes-1-79-0}
* Fixes an issue that caused the [affix](/reference/custom-resource-config#affix) property of config items to be ignored.
* Fixes an issue that caused the [help_text](/reference/custom-resource-config#help_text) property of config items to be ignored.
* Fixes an issue that caused the license card to not be updated when switching applications in the admin console.
* Fixes the ordering of versions on the [version history](/enterprise/updating-apps#update-an-application-in-the-admin-console) page in [Helm-managed mode (Alpha)](/vendor/helm-install).
* Fixes the display of node statistics in the [Cluster Management](https://docs.replicated.com/vendor/tutorial-ha-cluster-deploying#adding-remaining-nodes-to-cluster) tab.
* Fixes an issue where legacy encryption keys were not loaded properly during snapshot restores.
* Fixes an issue where snapshots would fail if a wildcard (`"*"`) was listed in the `additionalNamespaces` field of an Application manifest.
* Fixes an issue where the diff fails to generate for a version that excludes a Helm chart that was previously included.

## 1.78.0

Released on July 28, 2022

Support for Kubernetes: 1.21, 1.22, 1.23, and 1.24

### New Features {#new-features-1-78-0}
* The analyze application button on the [Troubleshoot tab](/enterprise/troubleshooting-an-app) now works in [Helm managed mode (Alpha)](/vendor/helm-install).
* Adds a deploy modal for versions on the [version history](/enterprise/updating-apps#update-an-application-in-the-admin-console) page in [Helm managed mode (Alpha)](/vendor/helm-install).

### Improvements {#improvements-1-78-0}
* Upgrades the internal database (Postgres) used by the admin console from `10.21-alpine` to `14.4-alpine`.

### Bug Fixes {#bug-fixes-1-78-0}
* Fixes an issue where all [dashboard links](/vendor/admin-console-adding-buttons-links) were rewritten to use the admin console hostname instead of the hostname provided in the application manifest.
* Fixes a bug that caused errors when trying to generate `helm upgrade` commands from the [config page](/vendor/config-screen-about#admin-console-config-tab) in [Helm managed mode (Alpha)](/vendor/helm-install).
* Fixes a bug where the same version could be listed twice on the [version history](/enterprise/updating-apps#update-an-application-in-the-admin-console) page in [Helm managed mode (Alpha)](/vendor/helm-install).

## 1.77.0

Released on July 22, 2022

Support for Kubernetes: 1.21, 1.22, 1.23, and 1.24

### New Features {#new-features-1-77-0}
* Displays version history information for Helm charts when running in Helm-managed mode (Alpha). For more information, see [Using Helm to Install an Application (Alpha)](/vendor/helm-install)
* License information can now be synced from the admin console's Dashboard and License pages for Helm charts when running in Helm-managed mode (Alpha). For more information, see [Using Helm to Install an Application (Alpha)](/vendor/helm-install)
* Admin console now supports limited RBAC mode when running in Helm-managed mode (Alpha). For more information, see [Using Helm to Install an Application (Alpha)](/vendor/helm-install)

### Improvements {#improvements-1-77-0}
* Better handling for network errors on the Helm install modal in Helm-managed mode (Alpha).
* Helm install command now includes authentication in Helm-managed mode (Alpha).
* Adresses the following high severity CVEs: CVE-2022-28946, CVE-2022-29162, and CVE-2022-1996.

### Bug Fixes {#bug-fixes-1-77-0}
* Fixes an issue that caused automatic deployments not to work on channels where semantic versioning was disabled, unless the version labels were valid [semantic versions](https://semver.org/).
* Fixes an issue that caused errors after the admin console pod restart until the Dashboard tab is visited in Helm-managed mode (Alpha).
* Begins using a temp directory instead of the current directory, to avoid file permissions issues when generating the `helm upgrade` command after editing the config. For more information, see [Using Helm to Install an Application (Alpha)](/vendor/helm-install).

## 1.76.1

Released on July 15, 2022

Support for Kubernetes: 1.21, 1.22, 1.23, and 1.24

### Bug Fixes {#bug-fixes-1-76-1}
* Fixes an issue that caused private images in some collectors to not be rewritten during preflight checks.
* Fixes an issue where the [Distribution](/reference/template-functions-static-context#distribution) template function returns an empty string in minimal RBAC installations running on OpenShift clusters.
* Updates the golang.org/x/text go module to address CVE-2021-38561 with high severity.
* Updates the local-volume-provider image to address CVE-2021-38561 with high severity.
* Updates the MinIO image to address CVE-2022-1271 with high severity.

## 1.76.0

Released on July 12, 2022

Support for Kubernetes: 1.21, 1.22, 1.23, and 1.24

### New Features {#new-features-1-76-0}
* Displays license information on the admin console Dashboard and License page for Helm charts when running in Helm-managed mode (Alpha). For more information, see [Using Helm to Install an Application (Alpha)](/vendor/helm-install)

### Bug Fixes {#bug-fixes-1-76-0}
* Fixes a bug that causes links defined in the [SIG Application custom resource](/reference/custom-resource-sig-application) to not be rewritten to the hostname used in the browser.

## 1.75.0

Released on July 5, 2022

Support for Kubernetes: 1.21, 1.22, 1.23, and 1.24

### New Features {#new-features-1-75-0}
* Adds a `helmUpgradeFlags` parameter to the [HelmChart custom resource](../reference/custom-resource-helmchart) when [Installing with Native Helm](../vendor/helm-installing-native-helm). The specified flags are passed to the `helm upgrade` command. Note that the Replicated app manager uses `helm upgrade` for all installations, including initial installations, and not just when the application is upgraded.

### Bug Fixes {#bug-fixes-1-75-0}
* Addresses the following critical severity CVEs: CVE-2022-26945, CVE-2022-30321, CVE-2022-30322, and CVE-2022-30323.
* Fixes a bug that causes the [`push-images`](../reference/kots-cli-admin-console-push-images) command to fail when `--registry-password` and `--registry-username` are not specified for use with anonymous registries.

## 1.74.0

Released on July 1, 2022

Support for Kubernetes: 1.21, 1.22, 1.23, and 1.24

### New Features {#new-features-1-74-0}
* Adds the ability to use a preflight check to compare the Kubernetes installer included in particular application version against the installer that is currently deployed. For more information, see [Include a Supporting Preflight Check](/vendor/packaging-embedded-kubernetes#include-a-supporting-preflight-check) in Creating a Kubernetes Installer Specification.

### Bug Fixes {#bug-fixes-1-74-0}
* Fixes an issue where you could not deploy valid application releases if the previously deployed version resulted in a kustomize error.
* Fixes an issue where kustomize would fail if a Helm chart and one of its sub-charts had the same name.
* Fixes an issue that caused Velero pods to be stuck in a Pending state when using the Internal Storage snapshot setting in Kubernetes installer-created clusters.
* Fixes an issue where the admin console would crash if a Helm chart with optional values but no values provided was included in a release.

## 1.73.0

Released on June 24, 2022

Support for Kubernetes: 1.21, 1.22, 1.23, and 1.24

### New Features {#new-features-1-73-0}
* Adds a `releaseName` parameter to the [HelmChart custom resource](/reference/custom-resource-helmchart) when [Installing with Native Helm](/vendor/helm-installing-native-helm). Defaults to the chart name. Specifying a `releaseName` also allows you to deploy multiple instances of the same Helm chart, which was previously impossible.

### Improvements {#improvements-1-73-0}
* Improved UX on the version history page when the application is up to date or when there are new available versions.

### Bug Fixes {#bug-fixes-1-73-0}
* Fixes an issue where the preflight screen was displayed even if no analyzers were run.
* Fixes an issue that prevented you from excluding a Helm chart that was previously included when [Installing with Native Helm](/vendor/helm-installing-native-helm).

## 1.72.2

Released on June 22, 2022

Support for Kubernetes: 1.21, 1.22, 1.23, and 1.24

### Bug Fixes {#bug-fixes-1-72-2}
* Fixed a bug that would cause duplicate Helm installations to be shown when running in helm-managed mode in clusters with open permissions.

## 1.72.1

Released on June 17, 2022

Support for Kubernetes: 1.21, 1.22, 1.23, and 1.24

### Improvements {#improvements-1-72-1}
* Config values are now stored in a secret when the admin console runs in Helm-managed mode (Alpha), so that the values can be rerendered when a user returns to the Config page.

### Bug Fixes {#bug-fixes-1-72-1}
* The dashboard "Disk Usage" graph now reports metrics for Prometheus deployments using the `kubernetes-service-endpoints` job.
* The configured Prometheus address now shows as the placeholder in the "Configure Prometheus address" modal.
* Fixes a bug that prevented an application from being deployed if a strict preflight check existed but was excluded.
* Fixes a bug that was caused when a top-level `templates` folder is not present in a Helm chart that also has subcharts and top-level charts.
* Fixes a bug where Kubernetes installer manifests included as part of an application release were applied when deploying the release.
* Updates the MinIO image to address the following critical and high severity CVEs: CVE-2021-42836, CVE-2021-41266, CVE-2020-26160, CVE-2018-25032, CVE-2022-0778, CVE-2022-25235, CVE-2022-25236, CVE-2022-25315, CVE-2022-24407.
* Updates the Dex image to address the following critical and high severity CVEs: CVE-2020-14040, CVE-2021-42836, CVE-2020-36067, CVE-2020-36066, CVE-2020-35380, CVE-2020-26521, CVE-2020-26892, CVE-2021-3121, CVE-2020-26160, CVE-2021-28831, CVE-2020-11080, CVE-2021-3450, CVE-2021-23840, CVE-2020-1967, CVE-2020-8286, CVE-2020-8285, CVE-2020-8231, CVE-2020-8177, CVE-2020-8169, CVE-2021-30139, CVE-2021-36159.
* Updates the local-volume-provider image to address CVE-2022-1664 with critical severity.

## 1.72.0

Released on June 14, 2022

Support for Kubernetes: 1.21, 1.22, 1.23, and 1.24

### New Features {#new-features-1-72-0}
* The admin console now shows the chart version and icon for the currently deployed Helm chart when running in Helm-managed mode (Alpha).

### Improvements {#improvements-1-72-0}
* Moves **Change password**, **Add new application**, and **Log out** functionality into a new menu in the top right of the navigation bar.
* Shows a meaningful error message when the license is expired on the dashboard version card.

### Bug Fixes {#bug-fixes-1-72-0}
* Fixes a bug that caused the deploy confirmation modal on the dashboard to always show "Redeploy" even if the version was not already deployed.
* Fixes a discrepancy between the license expiry date in the vendor portal and the expiry date in the admin console.
* Sets the User-Agent to the KOTS version string in outgoing HTTP requests where missing.
* Removes the **Registry settings** tab when running in Helm-managed mode (Alpha).
* Removes **Diff versions** links from the application dashboard and version history page when running in Helm-managed mode (Alpha).
* Removes the instructions on how to edit files on the **View files** tab when running in Helm-managed mode (Alpha).

## 1.71.0

Released on June 1, 2022

Support for Kubernetes: 1.21, 1.22, 1.23, and 1.24

### New Features
* Adds a `--port` flag to the `kots install` and `kots admin-console` commands to allow for overriding the local port on which to access the admin console.

### Improvements
* A temporary success message is displayed if preflight checks pass for a version.

### Bug Fixes
* Fixes a nil pointer panic when checking for updates if a file in the new release contains incomplete metadata information.

## 1.70.1

Released on May 19, 2022

Support for Kubernetes: 1.21, 1.22, and 1.23

### Improvements
* When enabling GitOps, the initial commit properly translates all labeled secrets to SealedSecrets.
* Improves the application dashboard and version history pages when GitOps is enabled.
* Prevents a user from generating a support bundle while another support bundle is being generated, and lets the user return to the `/troubleshoot/generate` route to see the progress of the current support bundle generation.
* Improves editing for scheduling automatic snapshots by making the cron expression input always visible.
* Adds a collector and analyzer for cases when NFS configuration fails because the `mount.nfs` binary is missing on the host.
* Cleans up failed `kotsadm-fs-minio-check` pods after the NFS backend for snapshots has been configured successfully.
* Supports Helm v3.8.2 in the app manager.
* Shows Helm installations when running in Helm managed mode (alpha).

### Bug Fixes
* Fixes an issue where uploading the airgap bundle using the admin console hangs at 0%.
* Fixes an issue where applications using semantic versioning did not receive updates when `--app-version-label` was used in the [kots install](/reference/kots-cli-install) command.
* Fixes an issue where the application was re-deployed when the admin console restarted.
* Fixes an issue where existing Host Path and NFS snapshots did not show up after migrating away from MinIO. Note that this fix is only applicable to new migrations. Users who have already migrated away from MinIO can continue to take new snapshots, but pre-migration snapshots will be missing.
* Fixes an issue where changing the API version for a native Kubernetes object caused that object to be deleted and recreated instead of updated.
* Fixes an issue where image pull secrets were not created in additional namespaces when only Helm charts were used by the application.
* Fixes an issue where custom icons did not show on the TLS/cert page on Safari and Chrome.
* Fixes an issue where the admin console loaded resources from the internet.
* Fixes critical and high CVEs found in the KOTS Go binaries.

## 1.70.0

Released on May 2, 2022

Support for Kubernetes: 1.21, 1.22, and 1.23

### New Features
* Adds a `weight` parameter to the [Helm custom resource](/reference/custom-resource-helmchart) when [Installing with Native Helm](../vendor/helm-installing-native-helm). Charts are applied by weight in ascending order, with lower numbered weights applied first.
* Adds the ability to change the admin console password from the **Change Password** link in the admin console page footer.
* Adds the ability to download `Config` file types for a given application sequence.
* Adds a template function `YamlEscape` to escape a string for inclusion in a YAML file.
* Adds the ability to allow uploading new TLS certificates used by kURL proxy with the [`reset-tls`](/reference/kots-cli-reset-tls) command.
* Adds the ability to dynamically set the number of results per page when browsing the application version history.

### Improvements
* When preflight checks are skipped during an initial installation, the application is still deployed.
* License and preflight errors are now displayed when performing an automated installation using the CLI.
* When changing the password using the `kubectl kots reset-password`, all active sessions are terminated and new sessions can be established with the new password.

### Bug Fixes
* Fixes an issue where ingress status informers always reported as "Missing" in Kubernetes 1.22+.
* Fixes an issue that caused image garbage collection in Kubernetes installer-created clusters (embedded clusters) to remove images outside of the application's dedicated registry namespace.
* Fixes an issue where a newer version might not have a **Deploy** button after the configuration is updated for the currently deployed version.
* Fixes an issue where the legends on the dashboard graphs were blank.
* Fixes an issue where hovering on a graph the tooltip showed "LLL" instead of a formatted date.

## 1.69.1

Released on April 19, 2022

Support for Kubernetes: 1.21, 1.22, and 1.23

### Improvements
* Updates `local-volume-provider` to v0.3.3.

### Bug Fixes
* Fixes an issue where links and text within the `app.k8s.io/v1beta1` `Application` kind were not templated.

## 1.69.0

Released on April 8, 2022

Support for Kubernetes: 1.21, 1.22, and 1.23

### New Features
* Adds the ability to switch from a community license to a different license for the same application. See [Changing a Community License](../enterprise/updating-licenses#changing-a-community-license).

### Improvements
* The [ensure-secret](/reference/kots-cli-docker-ensure-secret) command now creates a new application version, based on the latest version, that adds the Docker Hub image pull secret to all Kubernetes manifests that have images. This avoids Docker Hub's rate limiting.
* CA certificates for snapshot storage endpoints can now be uploaded on the snapshot page of the admin console.
* User sessions expire after 12 hours of inactivity.
* Removes expired sessions from the store in a daily cleanup job.
* Adds a Beta option for vendors to exclude MinIO images from app manager air gap bundles from the download portal. For more information, see [ MinIO from Air Gap Bundles](/vendor/packaging-air-gap-excluding-minio) in the documentation.

### Bug Fixes
* Fixes an issue where the registry image pull secrets were not applied in the additional namespaces specified by the application in minimal RBAC installations.
* Fixes an issue where some releases could be missed if they were promoted while other releases were being downloaded and semantic versioning was enabled.
* Fixes an issue where the "Select a different file" link did not allow the user to change the selected file on the config page.

## 1.68.0

Released on April 4, 2022

Support for Kubernetes: 1.21, 1.22, and 1.23

### New Features
* Adds the ability to make a KOTS application version required. Required version cannot be skipped during upgrades. See [Promoting releases](../vendor/releases-promoting).
* Adds the `supportMinimalRBACPrivileges` field to the Application custom resource, and adds the `--use-minimal-rbac` flag to the `kots install` command. `supportMinimalRBACPrivileges` indicates that the application supports minimal RBAC, but it will not be used unless the `--use-minimal-rbac` flag is passed to the `kots install` command. See [`supportMinimalRBACPrivileges`](../reference/custom-resource-application#supportminimalrbacprivileges) in the Application custom resource.

### Improvements
* Adds pagination to the version history page and improves the admin console API performance.
* Displays on the cluster management page of the admin console the labels applied to nodes in a Kubernetes installer-created cluster.
* The default Troubleshoot analyzers will now specifically call out issues with Envoy/Contour if detected.

### Bug Fixes
* Fixes a bug with automatic updates where new versions would be deployed automatically regardless of preflight outcomes. When automatic updates are configured, new versions will now only be deployed automatically if the preflights succeed.
* Fixes an issue where NFS snapshots could not be configured when MinIO is enabled in the cluster.
* Fixes an issue where updating the snapshot storage location to NFS or Host Path would incorrectly display a dialog indicating that Velero was not installed and configured properly.
* Fixes an issue that caused wrong metadata to be used at application install time when installing a specific version of an application with the `--app-version-label` flag.
* Fixes an issue that caused the support bundle analysis and/or redactions to not show up in the Troubleshoot page in the admin console in some cases.
* Fixes an issue where deployments weren't blocked when strict preflight analyzers failed due to parse/process errors.
* Fixes a style bug that caused the grid of metric graphs to be broken when there were more than three graphs.
* Fixes an issue on the config editor page that caused an element to be hidden under the navbar when the corresponding config item was clicked on from the sidebar.
* Fixes an issue where a version that was pulled in via automatic checks and deployed via automatic deployments would not be properly updated on the dashboard version card.
* Fixes an issue where two versions could show as being currently deployed on the version history page when using automatic deployments.
* Fixes an issue where AWS IAM instance roles could not be used when configuring the snapshot storage destination.

## 1.67.0

Released on March 21, 2022

Support for Kubernetes: 1.21, 1.22, and 1.23

### New Features
* Adds support for installing a specific application version. For more information about installing a specific application version, see [Install in an Online Environment](/enterprise/installing-existing-cluster#online) in _Installing on an Existing Cluster_ and [Installing with the Kubernetes Installer](/enterprise/installing-embedded-cluster).
* Extends the ability of status informers to detect if the application is being updated.
* Adds the ability to provide a strict preflight, which cannot be skipped and must not have any failure outcomes. Any failure outcomes will prevent the user from deploying the application. For more information on strict preflights, see [About preflight checks and support bundles​](/vendor/preflight-support-bundle-creating#about-preflight-checks-and-support-bundles) in Creating Preflight Checks and Support Bundles.
* New versions can automatically be deployed in the admin console, regardless of whether the vendor uses semantic versioning. For more information about automatically deploying new versions, see [Configure Automatic Updates​](/enterprise/updating-apps#configure-automatic-updates) in Updating an Application.

### Bug Fixes
* Fixes an issue that could cause images that are still used by the application to be deleted from the private registry in a Kubernetes installer-created cluster during image garbage collection.
* Fixes an issue where the same license could be installed more than once in some cases.
* Fixes an issue where the Cluster Management tab was not always initially present for Kubernetes installer-created clusters.
* Fixes an issue where attempting to re-download a pending application version would fail after upgrading the admin console from KOTS 1.65.
* Fixes an issue where the application icon in the metadata did not show as the favicon on the TLS pages.

## 1.66.0

Released on March 8, 2022

Support for Kubernetes: 1.21, 1.22, and 1.23

### New Features
* Adds the ability to exclude the applications or the admin console from full snapshot restores using the [`kots restore`](/reference/kots-cli-restore-index) command.
* Adds the ability to display the command to restore only the admin console from a [full snapshot](/enterprise/snapshots-understanding#full-snapshots-recommended) on the Full Snapshots page in the admin console.

### Improvements
* Adds the [`--no-port-forward`](/reference/kots-cli-install#usage) flag to the `kots install` command to disable automatic port-forwarding. The old `--port-forward` flag has been deprecated.

### Bug Fixes
* Corrects the placeholder Prometheus URL in the admin console dashboard so that it is accurate for embedded installations.
* Fixes a bug where the warning message sometimes printed incorrectly when a mismatch was detected between the kots CLI version and the version of the admin console that was running in the cluster.
* Fixes a bug where the **See details** button on the support bundle analysis page did not show any information about an unhealthy pod.
* Allows a user to re-upload a license if the application is not yet installed.
* Allows GitOps to be disabled when it is enabled but has an invalid configuration. Previously, you were required to fix the configuration before disabling GitOps.

## 1.65.0

Released on February 25, 2022

Support for Kubernetes: 1.20, 1.21, 1.22, and 1.23

### New Features
* Permanently enables the redesigned admin console app dashboard and version history pages introduced in [KOTS 1.60.0](#1600).
* Application versions that fail to download now appear in the version history. A new button is also present with the version to allow the download to be retried. Previously, these failures were lost when a newer version was downloaded successfully.
* Introduces the [`kots upstream download`](../reference/kots-cli-upstream-download) command to retry downloading a failed update of the upstream application.

### Improvements
* The port-forward initiated to access the admin console will continually retry when it is disconnected. If a new kotsadm pod comes up, the port forward will switch and forward to the new pod.
* If the `kots` CLI version doesn't match the KOTS API version in the cluster, a warning message is displayed advising the user to update the `kots` CLI to the appropriate version.

### Bug Fixes
* Fixes uploading preflight results from the CLI.
* Fixes a bug where the app icon in the metadata would not show as the favicon in Google Chrome.

## 1.64.0

Released on February 18, 2022

Support for Kubernetes: 1.20, 1.21, 1.22, and 1.23

### Improvements
* A MinIO image will no longer be present in new deployments when MinIO is not specified as an add-on in the Kubernetes installer specification.
* Enables an alternative that does not use MinIO for `hostPath` snapshots if the MinIO image is not present on the instance.

### Bug Fixes
* Fixes a bug that showed an incorrect diff on the version history page.
* Fixes deploy log errors for PVCs when using OpenEBS with Kubernetes 1.19 through 1.21.

## 1.63.0

Released on February 11, 2022

Supported on Kubernetes: 1.20, 1.21, 1.22, and 1.23

### New Features
* Changes the [`kots upstream upgrade`](../reference/kots-cli-upstream-upgrade) command to be synchronous by default and exposes error messages for it.

### Improvements
* Sets the Native Helm timeout to 60 minutes instead of 5 minutes.

## 1.62.0

Released on February 4, 2022

Supported on Kubernetes: 1.20, 1.21, 1.22, and 1.23

### New Features
* Adds [`targetKotsVersion`](../reference/custom-resource-application#targetkotsversion) as a field in the application spec. This field allows you to set a target version of KOTS for a release. The initial installation of an application will fail if the currently installed KOTS version is greater than the target version. When a target version is set, end users will receive a notification in the admin console if their currently deployed version of KOTS is less than the target version. For more informaiton, see the documentation.

* Adds [`minKotsVersion`](../reference/custom-resource-application/#minkotsversion-beta) (Beta) as a field in the application spec. This allows you to specify the minimum supported KOTS version for a release. An application cannot be installed if the currently deployed KOTS version is less than the minimum KOTS version specified for a release. See the [`minKotsVersion` documentation](../reference/custom-resource-application/#minkotsversion-beta) for caveats since this is a Beta feature.

### Improvements
* Defaults [`kubectl kots get config --appslug`](../reference/kots-cli-get-config) to the app slug of the deployed application if there is only one in the namespace.
* Defaults [`kubectl kots get config --sequence`](../reference/kots-cli-get-config) to the sequence of the latest available version.

### Bug Fixes
* Fixes a bug that caused the "Details" link, which shows the [application status](../vendor/admin-console-display-app-status), to be not visible in the new dashboard UI.
* Fixes the omission of certain password values from the rendered YAML file when using [`kubectl kots pull`](../reference/kots-cli-get-config).
* Fixes an issue that caused the license file included in a support bundle to contain a long array of integers instead of a string in the signature field.
* Fixes an issue which caused setting up a host path as a snapshot storage destination to fail.

## 1.61.0

Released on February 1, 2022

Supported on Kubernetes: 1.20, 1.21, 1.22, and 1.23

### New Features
* Adds a CLI command to [get all available versions for an application](../reference/kots-cli-get-versions) from the app manager.
* Adds the ability to block installing or upgrading an application if the current KOTS version is incompatible with the KOTS version required by the application. This feature is experimental and is only available to vendors who have requested access.

### Bug Fixes
* Fixes a bug that caused images to be pushed to a private registry multiple times during an air gap installation.
* Fixes a bug that erroneously displays a message to edit the current config when performing a new installation.
* Fixes an issue that caused [image garbage collection](../enterprise/image-registry-embedded-cluster#enable-and-disable-image-garbage-collection) to only remove images with the "latest" tag.

## 1.60.0

Released on January 25, 2022

Supported on Kubernetes: 1.20, 1.21, and 1.22

### New Features
* The admin console app dashboard and version history pages have been redesigned! This redesign improves the aesthetics of these pages and brings key functionality directly to the app dashboard. See [this blog](https://www.replicated.com/blog/new-features-announced-improvements-to-ux-host-preflights/) for more details.

### Improvements
* Updates MinIO to RELEASE.2022-01-08T03-11-54Z (resolves CVE-2021-43858 CVE).
* Updates Postgres to version 10.19.

### Bug Fixes
* Fixes an issue that caused images to be pushed multiple times during an [airgap installation](/enterprise/installing-existing-cluster#air-gap) when the [Native Helm](/vendor/helm-processing/#native-helm) feature is enabled.
* Fixes an issue that prevented the deployment status labels from breaking into multiple lines on small displays.

## 1.59.3

Released on January 21, 2022

Supported on Kubernetes: 1.20, 1.21, and 1.22

### Improvements
* Updates the [kubectl](../reference/custom-resource-application#kubectlversion) patch versions and added kubectl version 1.22.x.

### Bug Fixes
* Fixes an issue that caused the load balancer services to regenerate, resulting in downtime.

## 1.59.2

Release on January 18, 2022

Supported on Kubernetes: 1.19, 1.20, and 1.21

### Bug Fixes
* Adds a more descriptive error message to the KOTS CLI when the provided host path does not exist for snapshots storage.
* Fixes a bug that caused the "Send bundle to vendor" link to display when this feature is not enabled.
* Resolves CSS style issues.
* Fixes a bug where excluded Helm charts could not change between `UseHelmInstall: true` and `UseHelmInstall: false` without errors.
* Fixes a problem where the "Internal Storage" option was not selected by default in kURL clusters with the `disableS3` option set.
* Fixes a bug when Helm dependencies are aliased for Helm-native releases.

## 1.59.1

Released on December 29, 2021

Supported on Kubernetes: 1.19, 1.20, and 1.21

### Bug Fixes
* Fixes a `panic: runtime error` that occurs when the [`kots upstream upgrade`](../reference/kots-cli-upstream-upgrade) command is run.

## 1.59.0

Released on December 22, 2021

Supported on Kubernetes: 1.19, 1.20, and 1.21

### New Features
* Adds the `kubectl kots get config` command to export config values. This includes a `--decrypt` flag to decrypt sensitive values.
* The internal storage location for snapshots now uses a persistent volume instead of object storage when the `disableS3` flag is set to `true` for embedded clusters. For more information about removing KOTS use of object storage, see the [kURL add-on documentation](https://kurl.sh/docs/add-ons/kotsadm).

### Improvements
* Adds version output for current and new releases to the [`upstream upgrade`](../reference/kots-cli-upstream-upgrade) CLI command.

### Bug Fixes
* Fixes a bug that caused analyzers to surface errors in namespaces not used by the application when the admin console has cluster access in existing cluster installations.
* Fixes an issue that caused image pull secrets to be rendered in the admin console namespace instead of the `namespace` specified in the kots.io/v1beta1.HelmChart when using `useHelmInstall`.
* Fixes the `kots pull` CLI command to properly inject `imagePullSecrets` when using Helm Charts with `useHelmInstall` set to `true`.
* Fixes a bug that causes application images to not be deleted from a [private registry](../enterprise/image-registry-embedded-cluster).
* Fixes a bug that causes images included in support bundle's [`run` collector](https://troubleshoot.sh/docs/collect/run/#image-required) to not be deleted from a private registry.

## 1.58.2

Released on December 14, 2021

Supported on Kubernetes: 1.19, 1.20, and 1.21

### Bug Fixes
* Fixes a bug that caused config updates to take a long time.

## 1.58.1

Released on December 1, 2021

Supported on Kubernetes: 1.19, 1.20, and 1.21

### Bug Fixes
* Fixes a bug that caused Native Helm to skip deploying some Helm resources on automated installations.

## 1.58.0

Released on December 1, 2021

Supported on Kubernetes: 1.19, 1.20, and 1.21

### New Features
 * Adds support for the semantic versioning of releases when the version labels are [valid](https://semver.org/). To use this feature, [enable semantic versioning for the channel](../vendor/releases-semantic-versioning) that the license is currently on.
 * Adds the ability to automatically deploy new patch, minor, or major [valid](https://semver.org/) semantic versions when [semantic versioning is enabled](../vendor/releases-semantic-versioning). This new capability can be configured from the **Version History** page under the 'Configure automatic updates' option.

## 1.57.0 and earlier

For release notes for app manager versions earlier than 1.58.0, see the [Replicated App Manager Release Notes v1.9.0 - v1.65.0](../pdfs/app-manager-release-notes.pdf) PDF.
