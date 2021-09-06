# Overview

The console contains many different features, so here's a brief overview.

** There are two main ordering functions: dedicated servers and instant deployments. **

## Dedicated Server

Dedicated server orders come from `/order`. They send a Slack message with information on how the freelancers deploy them, including the provider and plan that should be deployed. 

## Instant Deployments

When customers click on the "Deploy Instant Server" button in the left sidebar, they are redirected to the `/deploy_options` page, where they can choose how to deploy their server.

### Kubevirt Custom Plans

On the `/deploy` page, customers can select which GPU they would like to deploy along with all of the other resources. This is fully custom and will only apply to providers that utilize the Kubernetes [Kubevirt orchestration platform](https://kubevirt.io/), e.g. Coreweave.

### Proxmox / Kubevirt Preconfigured Plans

At FluidStack, we use [Proxmox](https://proxmox.com) for our distributed deployment platform that spans many different providers, such as NxtGen. 

Proxmox is a reliable and easy-to-use hypervisor that most of our hosts install. When customers go onto `/deploy_preset`, they can deploy any preconfigured plans. Note that any Proxmox servers need to have a plan associated with them, and customers cannot deploy custom configurations due to the inflexibility of each Proxmox installation only being by itself, i.e. no networked storage, no migrations, etc. 

Any plan with an hourly rate on a provider that supports Kubevirt *OR* a Proxmox plan **with an hourly price** will be able to be deployed via the `/deploy_preset` page.