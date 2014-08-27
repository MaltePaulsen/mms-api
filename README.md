mms-api
=======
Minimalistic [MMS API](http://mms.mongodb.com/) agent for ruby

Installation
------------
```
gem install mms-api
```

Cli
---
```bash
$ bin/mms-api --help
mms-api is a tool for accessing MMS API

Usage:

	mms-api command [options]

Commands:

	groups | clusters | snapshots | restorejobs | restorejobs-create

Options:

    -u, --username <string>          MMS user
    -k, --apikey <string>            MMS api-key
    -n, --name <string>              Resource name using regexp
    -l, --limit <string>             Limit for result items
    -v, --version                    Version
    -h, --help                       Show this help
```

Development
-----------
```ruby
require 'mms'

agent = MMS::Agent.new('username', 'apikey')

# all available resources
group_list = agent.groups
cluster_list = agent.clusters
snapshot_list = agent.snapshots

# get first cluster from list
cluster = cluster_list.first

# get list of all restore-jobs for specific cluster
job_list = agent.findGroup(cluster.group.id).cluster(cluster.id).restorejobs
# or simply using cluster instance
job_list = cluster.restorejobs

# get first snapshot from list
snapshot = snapshot_list.first

# create restore job for snapshot
restorejob = agent.findGroup(snapshot.cluster.group.id).cluster(snapshot.cluster.id).snapshot(snapshot.id).create_restorejob
# or simply using snapshot instance
restorejob = snapshot.create_restorejob
```
