# Using Rolling Restarts [](id=using-rolling-restarts)

A rolling restart is shutting down and updating nodes one at a time (while the
other nodes are running) until they're all updated. This keeps your site running
while you update your cluster, whether it's physical, container, or image based.

Here's how a rolling restart works: 

1.  Shut down one cluster node (JVM instance). 

2.  Update/modify the deployment for that node (see the maintenance scenarios 
    that follow). 

3.  Start the node. 

4.  Repeat these steps for all other cluster nodes. 

User experience can be inconsistent during a rolling restart. For example, UI
changes in a plugin update are only visible on the updated nodes. Users on nodes
that haven't been updated see the old interface. Maintenance scenarios might
have specific cases that cannot be performed in rolling restarts. The scenario
descriptions mention these cases. 

The maintenance scenarios eligible for rolling restarts are described below. 

## New Modules and Plugins [](id=new-plugins-and-modules)

For a new plugin or module (one that does not already exist in the cluster) to
be eligible for rolling restart it must not modify data, delete, or rename
database columns in a way that breaks compatibility with existing plugins or
modules. 

## Updating Existing Modules and Plugins [](id=updating-existing-plugins-and-modules)

For a new version of an existing plugin or module to be eligible for rolling
restart, it must not modify data or delete or rename database columns in a way
that breaks compatibility with the existing version of the plugin or module. 

## Applying Fix Packs (DXP only) [](id=applying-fix-packs-dxp-only)

The Customer Portal identifies
[fix packs](/discover/deployment/-/knowledge_base/7-0/maintaining-liferay)
that are not revertible, and therefore ineligible for rolling restart. All other
fix packs are eligible. 

## Reverting Fix Packs (DXP only) [](id=reverting-fix-packs-dxp-only)

Revertible fix packs can be removed in rolling restarts. 

## Portal Properties controlled by `portal-ext.properties` [](id=portal-properties-controlled-by-portal-ext-properties)
 
[Portal Properties](@platform-ref@/7.1-latest/propertiesdoc/portal.properties.html)
file changes can be applied in rolling restarts. 

## System Settings controlled by Configuration Admin Files [](id=system-settings-controlled-by-configuration-admin-files)

[System configuration](/discover/portal/-/knowledge_base/7-0/understanding-system-configuration-files)
files can be applied in rolling restarts. 

## Application Server or JVM setting modifications [](id=application-server-or-jvm-setting-modifications)

Modifications to application server and JVM settings can be done in rolling
restarts. 

## Java Version Updates [](id=java-version-updates)

Minor version updates of Java can be applied in rolling restarts. Major version
updates are not supported in rolling restarts, and should instead be done when
all cluster nodes are shut down. 

All rolling restart-eligible updates can be applied using the rolling restart
steps listed above. Other updates must be done differently as described next. 

## Related Topics [](id=related-topics)

[@product@ Clustering](/discover/deployment/-/knowledge_base/7-0/liferay-clustering)

[Maintaining @product@](/discover/deployment/-/knowledge_base/7-0/maintaining-liferay)

[Implementing Data Upgrades](/develop/tutorials/-/knowledge_base/7-0/data-upgrades-and-verifiers)
