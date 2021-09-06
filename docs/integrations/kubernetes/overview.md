# Kubevirt Overview

Coreweave is currently the only provider that uses Kubevirt, but in the future, we may onboard more providers, so this article is worded in a way that is generic to any Kubevirt provider.

## Kubectl

Kubectl is the management system for Kubernetes.

Go find the kubernetes-config file for the provider (search in the `#s_coreweave_fluidstack`) channel for the Coreweave one.

Then, you have to install Kubectl [here](https://kubernetes.io/docs/tasks/tools/).

### Commands you should know

* `kubectl delete vs [server id in Airtable in lowercase]` (delete a coreweave VM. **Only use when the [FSCLI](/fscli/overview/) is not available, as that changes the Airtable records too**)
* `kubectl get vs` (gets the servers active in coreweave -- double check everything is deleted)

### Possible Results

During deployment:
```
kubectl get vs example-vs
NAME                STATUS               REASON                                           STARTED   INTERNAL IP      EXTERNAL IP
example-vs          Initializing         Waiting for VirtualMachineInstance to be ready   False                      123.123.123.123
```

### Deploying a server via Kubectl

Deploying a server via Kubectl is complicated. You have to create a `.yaml` file that follows the virtual server manifest configuration provided by the provider, e.g. [here is Coreweave's](https://docs.coreweave.com/virtual-servers/deployment-methods/kubectl). [See their examples too](https://github.com/coreweave/kubernetes-cloud/tree/master/virtual-server/examples/kubectl).

Once you have created this `.yaml` file, you have to "apply" it into action by running `kubectl apply -f [file].yaml`.

## Virtctl

Virtctl is the command line interface for managing Kubernetes virtual machines. It's weird how there are different CLIs for creating/deleting and starting/stopping, but that's just how it is:

### Commands you should know

* `virtctl start [server id in Airtable in lowercase]`  (start a coreweave VM)
* `virtctl stop [server id in Airtable in lowercase]` (stop a coreweave VM)
* `virtctl console [server id in Airtable in lowercase`] (access command line console of the VM)
* `virtctl vnc [server id in Airtable in lowercase`] (access VNC. You will need to have a GUI installed on the client where you are running this command)

Note that for the console/VNC, Windows deployments are usually quite slow and send you to an obscure SAC console upon deployment. Wait for a few minutes until you can access the CMD, typically after a reboot. 

**As with the delete function before, only use the start/stop functionality when the [FSCLI](/fscli/overview/) is not available, as that changes the Airtable records too. In this case, you will have to manually modify the Airtable to account for the change.**

### Possible Results

When running `kubectl get vs`, here is how a started/stopped server might look like:

Stopped server:
```
kubectl get vs example-vs
NAME                STATUS                 REASON               STARTED   INTERNAL IP      EXTERNAL IP
example-vs          VirtualServerStopped   VirtualServerStopped False                      123.123.123.123 
```

Running server:
```
kubectl get vs example-vs
NAME                STATUS               REASON               STARTED   INTERNAL IP      EXTERNAL IP
example-vs          VirtualServerReady   VirtualServerReady   True      1.2.3.4          123.123.123.123  
```

## Resolving Issues

### Unsynced Status

If a customer stops a VM on their own, or a VM starts automatically (rare -- please alert Jonathan if this happens, as billing was not done properly as bills are based on the minute that machines are on and if a VM starts automatically, this number is off), the status in Coreweave will not match the status in the Airtable.

Something like this will appear on the client side:

![Unsynced status](/static/unsynced-status.png)

To fix this, alter the status on Coreweave to the status in the Airtable. E.g. if the status is supposed to be started as shown in the Airtable and then stopped, start the Coreweave instance and then ask the customer to stop the machine. 

Basically, as long as both statuses are the same, customers should be able to start/stop correctly. 

However, if the status is the same and VMs are not able to be started/stopped correctly, ask Jonathan to investigate. This might be a software error.

### Machines in "Initializing Status"

When machines are stuck in the "Initializing" status, this is an error on the Kubevirt provider's part. Most likely, a bad commit was pushed. Contact them for a resolution for new deploys, and use the fscli to delete the existing ones and mark them as "Error Creating" instead of the "Provisioning" status so the customer isn't billed. 

When a machine is in "Initializing," this is normal for around 1 second during deployment. It is not normal if servers get stuck in this status.

![Kubectl Initializing](/static/kubectl-initializing.png)