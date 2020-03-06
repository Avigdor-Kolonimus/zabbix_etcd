# zabbix_etcd
Zabbix monitoring template for [ETCDV3](https://github.com/coreos/etcd)

**How to install**

- uncommit or write `ETCD_ENABLE_V2="true"` in the `etcd.conf` (`/etc/etcd/etcd.conf`). Relevant for etcd v3
- put the `etcd.py` in you zabbix `libexec` dir (I use `/etc/zabbix/scripts`)
- put the `etcd-params.conf` file in your zabbix `conf.d` path (`/etc/zabbix/conf.d/`)
- change the path of the `etcds.py` in the params file to where you put it
- import the template (`etcd-template_v42.xml`), the template suits for Zabbix v4.2
- apply to desired hosts

**Monitored items**

`etcd` process status (up/down):

    proc.num[etcd]

`/v2/stats/self`:

    etcd.self[recvAppendRequestCnt]
    etcd.self[sendAppendRequestCnt]
    etcd.self[state]

`/v2/stats/store`:

    # local stats that are uniqie to the node
    etcd.store[expireCount]
    etcd.store[getsFail]
    etcd.store[getsSuccess]
    etcd.store[watchers]

    # global stats that are shared across the cluster
    etcd.store[compareAndDeleteFail]
    etcd.store[compareAndDeleteSuccess]
    etcd.store[compareAndSwapFail]
    etcd.store[compareAndSwapSuccess]
    etcd.store[createFail]
    etcd.store[createSuccess]
    etcd.store[deleteFail]
    etcd.store[deleteSuccess]
    etcd.store[setsFail]
    etcd.store[setsSuccess]
    etcd.store[updateFail]
    etcd.store[updateSuccess]

`/v2/stats/leader`:

    etcd.follower[counts,fail]
    etcd.follower[counts,success]
    etcd.follower[latency,current]
