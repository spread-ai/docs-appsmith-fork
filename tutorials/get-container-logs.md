---
title: How to get container logs
description: Learn how to retrieve container logs in Studio.
---

<!--
README

For guidance on how to write documenation, see https://dev.stage.spread.ai/docs/contributor/guide.html. Contact Documentation when this document is ready for review.
-->

A guide on how to get container logs from different services.

## Prerequisite knowledge

- [x] Familiarity with working with containers.
- [x] Access to a SPREAD Studio environment.
- [x] Super admin rights.

## Instructions

### For Docker

This guide applies to docker-compose and docker installations. Studio logs can be found in the stacks directory on the docker host: `stacks/logs/`. The logs directory contains the sub-directories below for each **service**: `appsmithctl back-end cron editor mongodb redis rts`

If you don’t remember where your `stacks` directory is located, run `docker inspect -f (index .Mounts 0).Source }}' }}' <your-appsmith-container-id>`. Alternatively, you can run the commands below on your shell to create a zip file containing the logs.

```bash
appsmithContainerID=<your appsmith container id>
targetZipFile=<path to target zip file>
service=<choose one of: appsmithctl back-end cron editor mongodb redis rts | leave blank for all services>
stacksPath=$(docker inspect -f (index .Mounts 0).Source }}' }}' $appsmithContainerID)
zip -r $targetZipFile "$stacksPath/logs/$service" 
```

### For Docker in remote servers

1. SSH into the remote server and note the absolute path of the `stacks` directory.
2. If you don’t remember the path, use the `docker inspect` command as shown in the above section to locate it.
3. Exit from the remote server
4. In your local shell, run the command

```bash
scp -r -C -i <your-ssh-key>.pem <user>@<host-ip>:<abs-path-to-stacks-dir>/logs/<service> <target-local-dir>
```

### For AWS AMI

Run the following command:

```bash
scp -r -C -i <your-ssh-key>.pem appsmith@<host-ip>:/home/appsmith/appsmith/stacks/logs/<service> <target-local-dir>
```

This commands requires an SSH key to run.

### For DigitalOcean droplet

Run the following command:

```bash
scp -r -C root@<host-ip>:/root/appsmith/stacks/logs/<service> <target-local-dir>
```

### For Kubernetes

1. Run the command and note the name and namespace of the Appsmith POD: `kubectl get pods -A`
2. Run the command

```bash
kubectl cp <namespace>/<studio-pod-name>:/appsmith-stacks/logs/<service> <target-local-dir>
```

### For AWS ECS

1. Switch to the old AWS console to follow the instructions.
2. Navigate to your ECS cluster in the AWS console.
3. Select the service running Studio, and switch to the **Tasks** tab. Click the task running the Studio container. You may need to switch the **task filter** to see the **Stopped Tasks** to find the task where the issue occurred if ECS rolled out a new task after the crash.
4. In the Tasks page, Find **appsmith** in the **Container** Section and expand it, to find the **Log Configuration,** and click **view logs in CloudWatch**.
5. In the CloudWatch Logs page, click the **Actions** button and select `download search results in CSV`, to download the logs.

### For Azure Container Instance (ACI)

1. Navigate to your Storage Accounts in the Azure portal
2. Select the File Share mounted to the Appsmith ACI instance.
3. Select **Browse** in the sidebar menu
4. In the file share browser, open the `logs` directory.
5. Open the directory for the service for which the logs are required.
6. Select the log file and select **Download**.

You may also choose to access the logs of the container instance using the [az container logs](https://learn.microsoft.com/en-us/cli/azure/container#az_container_logs) command:

```bash
az container logs --resource-group myResourceGroup --name mycontainer
```
