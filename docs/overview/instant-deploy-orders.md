# Instant Deploy Orders

## Orders

New orders will come in the `#vd-instant-deploy` Slack with a wording like `Deployment Update for [email]: Placed order for [provider] [X]x [GPU]`

![Coreweave Example Order](/static/order-coreweave.png)

These require no action. If there is no error message, the automated system is working correctly.

## Deletions

Deletions require no action either. We have had no issues with deletions on other providers. With Proxmox deployments rolling out, the deletion process may take some time on HDD and SATA SSD systems. Monitor the `#infinity-critical-error` channel for error messages when it comes to deletions. Basically, the `vd-instant-deploy` channel alerts us that a deletion request has been sent, and then if there is an error by Rundeck actually deleting the server, that gets sent in the `#infinity-critical-error` channel. These errors should always be investigated, as they can corrupt the deployment process of new Proxmox VMs.

![Example Deletion](/static/deletion-example.png)
