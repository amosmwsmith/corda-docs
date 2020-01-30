---
title: "Upgrading the HA notary service"
date: 2020-01-08T09:59:25Z
---


# Upgrading the HA notary service

## Version 4.1
Since Corda Enterprise 4.1 the MySQL JDBC driver now needs to be installed manually for every worker node, otherwise nodes will fail to start.
                See [notary installation page]({{< relref "installing-the-notary-service#mysql-driver" >}}) for more information.


## Version 4.0
In Corda Enterprise 4.0 an additional table `notary_committed_transactions` is being used by the HA notary to support the new reference state functionality.


{{< note >}}
In order to enable reference state usage, the minimum platform version of the whole network has to be updated to version 4, which means
                    both the client nodes and the notary service have to be upgraded to version 4.


{{< /note >}}
Upgrade steps:


* Backup your Percona XtraDB Cluster, see [operating percona]({{< relref "operating-percona" >}}).


* Test you can restore from backup.


* Log in to any Percona XtraDB Cluster database server and create the `notary_committed_transactions` table. It will be replicated to all other database servers.

> 
> ```sql
> CREATE TABLE IF NOT EXISTS notary_committed_transactions (
>     transaction_id BINARY(32) NOT NULL,
>     CONSTRAINT tid PRIMARY KEY (transaction_id)
> );
```

* In the unlikely event that the database gets corrupted, take all the notary worker nodes down and follow the “Repair” guide under [operating percona]({{< relref "operating-percona" >}}) to restore the database.


* Perform a rolling upgrade on the notary worker nodes. Follow the [node upgrade guide]({{< relref "../node-upgrade-notes" >}}) for each node, and make sure the node is running and is no longer in flow draining mode before moving on to the next one.


