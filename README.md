# Validated Patterns for Telco Hub OpenShift Clusters

This repository is in charge of applying day 1 and day 2 configurations to Telco OpenShift clusters using the Validated Patterns framework approach.This framework follow Telco Network Cloud (TNC) v3.1 with specifications for OpenShift 4.14.

Validated Patterns are an evolution of how you deploy applications in a hybrid cloud. With a pattern, you can automatically deploy a full application stack through a GitOps-based framework. With this framework, you can create business-centric solutions while maintaining a level of Continuous Integration (CI) over your application.

The following table provide information about what are the expected variables inside values-hub.yaml alongside a example.

## Expected variables inside values-hub.yaml

| Variable                              | Description                                                                                                    | Example                                                         |
|---------------------------------------|----------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------|
| `mgmt.cluster.name`                   | The name of the management cluster.                                                                           | `mgmt2`                                                         |
| `mgmt.cluster.location`               | Physical or logical location of the management cluster.                                                        | `dc`                                                            |
| `mgmt.cluster.domain`                 | Domain used for the management cluster.                                                                       | `domain.es`                                                     |
| `mgmt.cluster.enableUnsealVault`      | Enables or disables the automatic unseal functionality for Vault. If there's no Vault in place set it to false.                                             | `false`                                                         |
| `mgmt.cluster.mgmt_location`          | Specific management location, such as main data center.                                          | `mgmt1`                                                       |
| `mgmt.proxy.host`                     | Proxy server hostname used by the management cluster.                                                          | `proxy.example.com`                                             |
| `mgmt.proxy.port`                     | Proxy server port.                                                                                             | `8080`                                                          |
| `mgmt.proxy.ca_bundle`                | Certificate Authority (CA) bundle for proxy validation.                                                        | `/etc/pki/ca-trust/extracted/pem/tls-ca-bundle.pem`             |
| `mgmt.authentication.htpasswd.admin`  | Admin password hash for HTPasswd authentication.                                                               | `""`                                                            |
| `mgmt.authentication.ldap.bind_password` | Password for the LDAP bind user.                                                                            | `your_bind_password`                                            |
| `mgmt.authentication.ldap.url`        | URL of the LDAP server for authentication.                                                                     | `idm-serv.mgmt2.dc.domain.es`                                   |
| `mgmt.authentication.ldap.bind_dn`    | Distinguished Name (DN) for binding to the LDAP server.                                                        | `uid=ocp-bind-user,cn=users,cn=accounts,dc=mgmt2,dc=dc,dc=domain,dc=es` |
| `mgmt.authentication.ldap.groups_base_dn` | Base DN for LDAP groups.                                                                                   | `cn=groups,cn=accounts,dc=mgmt2,dc=dc,dc=domain,dc=es`          |
| `mgmt.authentication.ldap.users_base_dn` | Base DN for LDAP users.                                                                                    | `cn=users,cn=accounts,dc=mgmt2,dc=dc,dc=domain,dc=es`           |
| `mgmt.authentication.ldap.group_membership` | Specific LDAP group that allows access to the management cluster.                                         | `cn=ocpusers,cn=groups,cn=accounts,dc=mgmt2,dc=dc,dc=domain,dc=es` |
| `mgmt.authentication.ldap.groups_whitelist` | List of LDAP groups with access to the cluster.                                                          | `[ "cn=ocpusers,cn=groups,...", "cn=ocpadmins,...", "cn=ocpreaders,..." ]` |
| `mgmt.authentication.ldap.sync_schedule` | Cron schedule for syncing LDAP groups and users.                                                          | `"*/15 * * * *"`                                                |
| `mgmt.authentication.ldap.crt`        | Certificate file for LDAP server connection.                                                                  | `/etc/pki/tls/certs/ldap.crt`                                   |
| `mgmt.apps.provisioner_ip`                    | IP address of the provisioner for the applications namespace.                                             | `10.100.0.101`                            |
| `mgmt.apps.ns`                                | Namespace where the application resources will be deployed.                                               | `mano-apps`                                |
| `mgmt.apps.nad_name`                          | Name of the NetworkAttachmentDefinition (NAD) used by the applications.                                   | `apps-nad`                                 |
| `mgmt.apps.subnet`                            | IP subnet allocated for applications.                                                                     | `10.100.0.132`                            |
| `mgmt.apps.subnet_len`                        | Length of the subnet mask for the application IP range.                                                   | `26`                                       |
| `mgmt.apps.subnet_gw`                         | Gateway IP for the applications subnet.                                                                   | `10.100.0.133`                            |
| `mgmt.apps.domain`                            | Domain for the applications within the management cluster.                                                | `mgmt2.dc.domain.es`            |
| `mgmt.apps.dns_server_ip`                     | DNS server IP address for applications.                                                                   | `10.100.0.134`                            |
| `mgmt.lso.maxDeviceCount`                     | Maximum number of devices to be managed by Local Storage Operator (LSO).                                  | `8`                                        |
| `mgmt.odf.mds.limits.cpu`                     | Maximum CPU allocation for metadata server (MDS) in Open Data Foundation (ODF).                           | `3`                                        |
| `mgmt.odf.mds.limits.memory`                  | Maximum memory allocation for MDS in ODF.                                                                 | `8Gi`                                      |
| `mgmt.odf.mds.requests.cpu`                   | Requested CPU allocation for MDS in ODF.                                                                  | `3`                                        |
| `mgmt.odf.mds.requests.memory`                | Requested memory allocation for MDS in ODF.                                                               | `8Gi`                                      |
| `mgmt.odf.storageDeviceSets.count`            | Number of storage device sets to deploy in ODF.                                                           | `8`                                        |
| `mgmt.odf.storageDeviceSets.limits.cpu`       | CPU limit per storage device set in ODF.                                                                  | `2`                                        |
| `mgmt.odf.storageDeviceSets.limits.memory`    | Memory limit per storage device set in ODF.                                                               | `5Gi`                                      |
| `mgmt.odf.storageDeviceSets.requests.cpu`     | Requested CPU per storage device set in ODF.                                                              | `2`                                        |
| `mgmt.odf.storageDeviceSets.requests.memory`  | Requested memory per storage device set in ODF.                                                           | `5Gi`                                      |
| `mgmt.idm.name`                            | Name of the IDM (Identity Management) instance.                                          | `idm-r1`                                        |
| `mgmt.idm.qcow`                            | Path to the QCOW2 image for the IDM server.                                              | `qcow2-images/rhel-baseos-9.0-x86_64-kvm.qcow2` |
| `mgmt.idm.uuid`                            | Unique identifier for the IDM instance. You can use $ uuidgen to get a random UUID.                                                 | `8FAA08D3-5C0E-4C36-9EAF-56B842BDEFA0`          |
| `mgmt.idm.app_name`                        | Application name of the IDM server.                                                      | `idm-server`                                    |
| `mgmt.idm.domain`                          | Domain of the IDM instance.                                                              | `mgmt2.dc.domain.es`                            |
| `mgmt.idm.user`                            | Username for accessing the IDM instance.                                                 | `admin`                                         |
| `mgmt.idm.password`                        | Password for accessing the IDM instance.                                                 | `admin`                                      |
| `mgmt.idm.ip`                              | IP address of the IDM instance.                                                          | `10.100.0.135`                                 |
| `mgmt.idm.hostname`                        | Fully qualified domain name (FQDN) for the IDM instance.                                 | `idm-r1.mgmt2.dc.domain.es`                     |
| `mgmt.idm.ssh_authorized_key`              | SSH authorized key for accessing the IDM instance.                                       | `"~/.ssh/id_rsa"`                                            |
| `mgmt.satellite.qcow`                      | Path to the QCOW2 image for the Satellite server.                                        | `qcow2-images/rhel-8.8-x86_64-kvm.qcow2`        |
| `mgmt.satellite.uuid`                      | Unique identifier for the Satellite server. You can use $ uuidgen to get a random UUID.                                              | `BF308E89-331E-428B-979F-161B6E9ABD84`          |
| `mgmt.satellite.app_name`                  | Application name of the Satellite server.                                                | `sat-server`                                    |
| `mgmt.satellite.domain`                    | Domain of the Satellite server.                                                          | `mgmt2.dc.domain.es`                            |
| `mgmt.satellite.user`                      | Username for accessing the Satellite server.                                             | `admin`                                         |
| `mgmt.satellite.password`                  | Password for accessing the Satellite server.                                             | `admin`                                      |
| `mgmt.satellite.ip`                        | IP address of the Satellite server.                                                      | `10.100.0.137`                                 |
| `mgmt.satellite.hostname`                  | Fully qualified domain name (FQDN) for the Satellite server.                             | `satellite.mgmt2.dc.domain.es`                  |
| `mgmt.satellite.ssh_authorized_key`        | SSH authorized key for accessing the Satellite server.                                   | `"~/.ssh/id_rsa.pub"`                                            |
| `mgmt.kafka.topics[n]`                        | List of Kafka topics for log management and metrics.                                          | `["rsyslog-test", "stf-metrics", "mano1-ocp-metrics"]` |  
| `mgmt.stf.cloudNames`                      | List of STF (Service Telemetry Framework) cloud environment names.                            | `["vim1dc", "vim2btb1"]`                       |
| `mgmt.stf.cloudNames[n]`                   | Name of a specific STF cloud environment.                                                     | `vim1dc`                                       |
| `mgmt.stf.serviceMonitors[n]`                 | List of service monitors in STF for monitoring specific services or components.               | `["ceil", "coll", "sens"]`                       |
| `mgmt.gitops.ztp_plugin_image`                  | Image for the ZTP (Zero-Touch Provisioning) plugin.                                                          | `registry.redhat.io/openshift4/ztp-site-generate-rhel8:v4.14.4` |
| `mgmt.gitops.ztp_instance_ns`                   | Namespace for the ZTP instance.                                                                              | `ztp`                                                        |
| `mgmt.gitops.openshift_gitops_api_version`      | API version of OpenShift GitOps.                                                                             | `argoproj.io/v1alpha1`                                       |
| `mgmt.gitops.multicluster_operators_subscription` | Image for the multicluster operators subscription.                                                            | `registry.redhat.io/rhacm2/multicluster-operators-subscription-rhel8:v2.7` |
| `mgmt.gitops.repoURL`                           | URL of the GitOps repository.                                                                                | `https://gitlab.cicd.mgmt2.dc.domain.es/gitops/core-ztp.git` |
| `mgmt.gitops.core_ztp_repoToken`                | Authentication token for the core ZTP GitOps repository.                                                     | `glpat-example-kla`                                          |
| `mgmt.ztp.jobTerminationGracePeriod`            | Grace period for job termination in seconds.                                                                 | `300`                                                        |
| `mgmt.ztp.serviceAccountName`                   | Name of the service account used for ZTP jobs.                                                               | `mce-prereq-sa`                                              |
| `mgmt.ztp.rbac.roles[n].name`                   | Name of the role for ZTP RBAC configuration.                                                                 | `mce-prereq`                                                 |
| `mgmt.ztp.rbac.roles[n].createRole`             | Whether to create the role for ZTP RBAC configuration.                                                       | `true`                                                       |
| `mgmt.ztp.rbac.roles[n].apiGroups[j]`              | List of API groups for the RBAC role.                                                                        | `['""', 'metal3.io']`                                        |
| `mgmt.ztp.rbac.roles[n].scope.cluster`          | Indicates whether the role applies at the cluster level.                                                     | `true`                                                       |
| `mgmt.ztp.rbac.roles[n].resources[j]`              | List of resources for the RBAC role permissions.                                                             | `["namespace", "configmaps", "provisionings", "secrets"]`    |
| `mgmt.ztp.rbac.roles[n].verbs[j]`                  | List of actions allowed by the role (e.g., get, list, patch).                                                | `["get", "list", "patch", "update", "create", "edit"]`       |
| `mgmt.ztp.rbac.roleBindings[n].name`            | Name of the role binding for ZTP RBAC configuration.                                                         | `mce-prereq-rolebinding`                                     |
| `mgmt.ztp.rbac.roleBindings[n].createBinding`   | Whether to create the role binding for ZTP RBAC configuration.                                               | `true`                                                       |
| `mgmt.ztp.rbac.roleBindings[n].scope.cluster`   | Indicates whether the role binding applies at the cluster level.                                             | `true`                                                       |
| `mgmt.ztp.rbac.roleBindings[n].namespace`       | Namespace in which the role binding applies, if not at the cluster level.                                    | `""`                                                         |
| `mgmt.ztp.rbac.roleBindings[n].subjects.kind`   | Kind of subject for the role binding (e.g., ServiceAccount).                                                 | `ServiceAccount`                                             |
| `mgmt.ztp.rbac.roleBindings[n].subjects.name`   | Name of the subject for the role binding.                                                                    | `mce-prereq-sa`                                              |
| `mgmt.ztp.rbac.roleBindings[n].subjects.namespace` | Namespace of the subject for the role binding.                                                                | `multicluster-engine`                                        |
| `mgmt.ztp.rbac.roleBindings[n].roleRef.kind`    | Kind of the referenced role (e.g., ClusterRole).                                                             | `ClusterRole`                                                |
| `mgmt.ztp.rbac.roleBindings[n].roleRef.name`    | Name of the referenced role.                                                                                 | `mce-prereq`                                                 |
| `mgmt.console.plugins[n]`               | List of plugins to enable in the OpenShift console.                                                     | `odf-console`, `kubevirt-plugin`, `mce`, `acm`, `nmstate-console-plugin`, `monitoring-plugin` |
| `mgmt.quay.fqdn`                                | Fully qualified domain name for the Quay registry service.                                                                | `quay.apps.mgmt2.dc.domain.es`                                 |
| `mgmt.quay.components[n]`                          | List of Quay components with configuration options.                                                                      | `clair`, `postgres`, `objectstorage`, etc.                     |
| `mgmt.quay.components[].kind`                   | Type of Quay component being configured.                                                                                 | `clair`, `postgres`, `objectstorage`, `redis`, etc.            |
| `mgmt.quay.components[].managed`                | Indicates if the component is managed by the Quay Operator.                                                              | `true`, `false`                                                |
| `mgmt.quay.components[].overrides.volumeSize`   | Specifies the storage size for the component, if applicable.                                                             | `100Gi`, `500Gi`                                               |
| `mgmt.quay.param.FEATURE_USER_INITIALIZE`       | Enables initial user setup on first Quay startup.                                                                        | `true`                                                         |
| `mgmt.quay.param.BROWSER_API_CALLS_XHR_ONLY`    | Restricts API calls to XMLHttpRequest (XHR) only for browser requests.                                                   | `false`                                                        |
| `mgmt.quay.param.ALLOW_PULLS_WITHOUT_STRICT_LOGGING` | Allows image pulls without strict logging enabled.                                                                   | `false`                                                        |
| `mgmt.quay.param.DEFAULT_TAG_EXPIRATION`        | Default expiration time for image tags.                                                                                  | `2w`                                                           |
| `mgmt.quay.param.ENTERPRISE_LOGO_URL`           | URL for custom enterprise logo in Quay UI.                                                                              | `/static/img/RH_Logo_Quay_Black_UX-horizontal.svg`             |
| `mgmt.quay.param.FEATURE_BUILD_SUPPORT`         | Enables build support within Quay.                                                                                       | `false`                                                        |
| `mgmt.quay.param.FEATURE_DIRECT_LOGIN`          | Enables direct login to Quay without SSO.                                                                               | `true`                                                         |
| `mgmt.quay.param.FEATURE_MAILING`               | Enables mailing features in Quay.                                                                                        | `false`                                                        |
| `mgmt.quay.param.REGISTRY_TITLE`                | Full title displayed in Quay's UI.                                                                                       | `Red Hat Quay`                                                 |
| `mgmt.quay.param.REGISTRY_TITLE_SHORT`          | Shortened registry title displayed in UI.                                                                               | `Red Hat Quay`                                                 |
| `mgmt.quay.param.TAG_EXPIRATION_OPTIONS[n]`        | List of available tag expiration options.                                                                               | `2w`                                                           |
| `mgmt.quay.param.TEAM_RESYNC_STALE_TIME`        | Time interval for resyncing team memberships.                                                                           | `60m`                                                          |
| `mgmt.quay.param.SERVER_HOSTNAME`               | Hostname for Quay server, used in configurations and UI.                                                                 | `quay.apps.mgmt2.dc.domain.es`                                 |
| `mgmt.quay.param.TESTING`                       | Enables testing mode for Quay.                                                                                           | `false`                                                        |
| `mgmt.quay.param.AUTHENTICATION_TYPE`           | Type of authentication used for Quay.                                                                                    | `LDAP`                                                         |
| `mgmt.quay.param.LDAP_ADMIN_DN`                 | Distinguished Name (DN) for the LDAP admin user.                                                                         | `uid=quay-bind-user,cn=users,cn=accounts,dc=mgmt2,dc=dc,dc=domain,dc=es` |
| `mgmt.quay.param.LDAP_ADMIN_PASSWD`             | Password for LDAP admin user.                                                                                            | `vriESYGoV02AIsXoCZjhdw==`                                     |
| `mgmt.quay.param.LDAP_ALLOW_INSECURE_FALLBACK`  | Allows fallback to insecure LDAP connections if secure connections fail.                                                 | `true`                                                         |
| `mgmt.quay.param.LDAP_BASE_DN[n]`                  | Base DN used for LDAP searches.                                                                                          | `dc=mgmt2, dc=dc, dc=domain, dc=es`              |
| `mgmt.quay.param.LDAP_EMAIL_ATTR`               | LDAP attribute that stores user email addresses.                                                                         | `mail`                                                         |
| `mgmt.quay.param.LDAP_UID_ATTR`                 | LDAP attribute for the user ID.                                                                                          | `uid`                                                          |
| `mgmt.quay.param.LDAP_URI`                      | URI for connecting to the LDAP server.                                                                                   | `ldaps://idm-serv.mgmt2.dc.domain.es`                          |
| `mgmt.quay.param.LDAP_USER_RDN[n]`                 | Relative DN(s) used to locate users in LDAP.                                                                             | `cn=users`, `cn=accounts`                                      |
| `mgmt.quay.param.FEATURE_TEAM_SYNCING`          | Enables synchronization of team data with LDAP groups.                                                                   | `true`                                                         |
| `mgmt.quay.param.LDAP_USER_FILTER`              | LDAP filter to match users authorized to access Quay.                                                                    | `(memberOf=cn=quayusers,cn=groups,cn=accounts,dc=mgmt2,dc=dc,dc=domain,dc=es)` |
| `mgmt.quay.param.LDAP_SUPERUSER_FILTER`         | LDAP filter to match users with superuser access in Quay.                                                                | `(memberOf=cn=quayadmins,cn=groups,cn=accounts,dc=mgmt2,dc=dc,dc=domain,dc=es)` |
| `mgmt.quay.param.FEATURE_SUPERUSERS_FULL_ACCESS`| Grants superusers full access in Quay.                                                                                   | `true`                                                         |
| `mgmt.apiserver.tls.crt` | TLS certificate for the API server    | `LS0tLS1C...MEVBd0l3` |
| `mgmt.apiserver.tls.key` | TLS private key for the API server    | `LS0tLS1C...hQWxVSg` |
| `mgmt.ingress.tls.crt` | TLS certificate for Ingress             | `LS0tLS1C...MEVBd0l3` |
| `mgmt.ingress.tls.key` | TLS private key for Ingress             | `LS0tLS1C...hQWxVSg` |