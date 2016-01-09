# Ticker BOSH release

This is a BOSH release of a ticker application that emits a message to Stdout & Stderr every 1 second. This release has been developed for a BOSH-Lite warden environment but can be deployed to other environments by creating a new deployment manifest, like timer-warden.yml, with the configurations required for that environment.

# Deploy

To deploy the application use the following command sequence from the interview-timer-master directory:

```
bosh upload release 
bosh deployment timer-warden.yml
bosh deploy
```

# Verify

To verify the deployment, assuming you are using vagrant, ssh into the vagrant VM and list the installed VMs using the following commands:

```
vagrant ssh
bosh vms
```

You will see output like this
```
Acting as user 'admin' on 'Bosh Lite Director'
Deployment `interview-timer'

Director task 77

Task 77 done

+-----------------+--------------------+----------------------+------------+
| Job/index       | State              | Resource Pool        | IPs        |
+-----------------+--------------------+----------------------+------------+
| ticker/0        | running            | common-resource-pool | 10.254.0.2 |
+-----------------+--------------------+----------------------+------------+

VMs total: 3
```

SSH into the IP of the ticker job
```
ssh vcap@10.254.0.2
cd /var/vcap/sys/log/ticker
```

default password for vcap is c1oudc0w 

tailing the ticker.stdout.log should give you an output like this:
```
Hello world from 2016-01-09 15:10:16.849328986 +0000 UTC
Hello world from 2016-01-09 15:10:17.849503928 +0000 UTC
Hello world from 2016-01-09 15:10:18.848579018 +0000 UTC
```

and tailing the ticker.stderr.log should give you an output like this:
```
ERROR at 2016-01-09 15:11:46.849286189 +0000 UTC
ERROR at 2016-01-09 15:11:47.849778927 +0000 UTC
ERROR at 2016-01-09 15:11:48.848677091 +0000 UTC
```

