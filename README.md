# Azeti Broker Resources

This repository contains the resources used by the Azeti ActiveMQ broker.

## Master-Slave

This configuration use a NFS volume as shared storage between the broker instances.

### Standalone NFS

First, create the NFS docker volume:

```
docker volume create --driver local --opt type=nfs --opt o=addre=<nfs_server_ip>,rw --opt device=:/volume/kahadb kahadb
```

Now, use this volume when you start the Docker container:

```
docker run -d -it --name my-container --mount source=kahadb,target=/mnt/efs/kahadb my-image
```

### EFS

For details about EFS, see:

* https://docs.aws.amazon.com/AmazonECS/latest/developerguide/using_efs.html
* https://aws.amazon.com/fr/premiumsupport/knowledge-center/ecs-create-docker-volume-efs/
* https://aws.amazon.com/fr/blogs/compute/amazon-ecs-and-docker-volume-drivers-amazon-efs/
