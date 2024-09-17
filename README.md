# mrt-service-release-manifest
Data structure defining the semantic version state of all Merritt applications


### Usage

The `service-release-manifest.yaml` is used by our `mrt-tomcat-deploy` script
when deploying Merritt subservice application WAR files to Tomcat servers.
See: [Merritt Tomcat Deploy README][mrt-tomcat-deploy-readme] for details.

Prior to deploying a new service release, the Merritt developer updates this file to 
specify the semantic version to be deployed.

Each entry in the manifest is a `key: value` pair where the key is an FQSN of a
Merritt application and the value is the semantic version or __build tag__ of a java
package hosted on the Merritt CodeArtifact repository.

```
#uc3-mrt-access-prd: 1.8.19
#uc3-mrt-access-stg: 1.8.19
uc3-mrt-audit-prd: 1.8.9
uc3-mrt-audit-stg: 1.9.0
[cut]
```

If an FQSN is missing or commented out, `mrt-tomcat-deploy` will not execute a deployment of
that FQSN.



### Migration Checklist

This is a list of tasks to complete migration of subservice environments from
previous Capistrano based deployment to the new `mrt-tomcat-deploy` workflow.

1. **build ready** - deployable build of Java package and WAR asset is staged in CodeArtifact repository
1. **manifest ready** - semantic version (build tag) of deployable build is posted in [service release manifest][ReleaseManifest]
1. **puppet ready** - apply new `uc3_mrt_tomcat_deploy` puppet module to reconfigure Tomcat service directory structure
1. **deploy success** - a full deployment and service restart using `mrt-tomcat-deploy` was successful
1. **purge cap dirs** - clean up obsolete directories on Tomcat servers formerly used by capistrano


The following tables track the migration process for each FQSN:

**FQSN Migration Status**
| FQSN                  | build ready | manifest ready | puppet ready | deploy success | purge cap dirs |
| --------------------- | ----------- | -------------- | ------------ | -------------- | -------------- |
| uc3-mrt-access-stg    |             |                |              |                |                |
| uc3-mrt-audit-stg     | 1.9.0       | yes            | yes          | yes            |                |
| uc3-mrt-ingest-stg    |             |                |              |                |                |
| uc3-mrt-inventory-stg |             |                |              |                |                |
| uc3-mrt-replic-stg    |             |                | yes          |                |                |
| uc3-mrt-store-stg     |             |                |              |                |                |
| uc3-mrt-access-prd    |             |                |              |                |                |
| uc3-mrt-audit-prd     |             |                |              |                |                |
| uc3-mrt-ingest-prd    |             |                |              |                |                |
| uc3-mrt-inventory-prd |             |                |              |                |                |
| uc3-mrt-replic-prd    |             |                |              |                |                |
| uc3-mrt-store-prd     |             |                |              |                |                |


**`mrt-tomcat-deploy` installed**
| User       | install completed | deployment tested |
| ---------- | ----------------- | ----------------- |
| dloy       | X                 | X                 |
| tbraddy    |                   |                   |
| mreyes     |                   |                   |
| elopatin   |                   |                   |




[mrt-tomcat-deploy-readme]: https://github.com/CDLUC3/mrt-tomcat-deploy/blob/main/README.md
[ReleaseManifest]: https://github.com/CDLUC3/mrt-service-release-manifest/blob/main/service-release-manifest.yaml


