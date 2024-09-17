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




[mrt-tomcat-deploy-readme]: https://github.com/CDLUC3/mrt-tomcat-deploy/blob/main/README.md


