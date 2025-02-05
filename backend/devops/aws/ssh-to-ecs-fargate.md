
```bash
aws ecs update-service \
--cluster cluster-name \
--service sevice-name --enable-execute-command
```

```
# SSH Connect to EC2
aws ecs execute-command --cluster cluster-name \
    --task your-task-id \
    --container container-name \
    --interactive \
    --command "/bin/sh"
```

```bash
# Disconnect Load Balancer from EC2
aws ecs update-service \
  --cluster cluster-name \
  --service service-name \       
  --load-balancers "[]"
```

```bash
# Decribe Service 
aws ecs describe-services \
  --cluster cluster-name \
  --services service-name
```

```bash
# Update Service
aws ecs update-service \
  --cluster cluster-name \
  --service service-name \
  --task-definition task-definition-name:version \
  --force-new-deployment
```

```bash
# Add Load Balancer to ECS Service
aws ecs update-service \
  --cluster <CLUSTER_NAME> \
  --service <SERVICE_NAME> \
  --load-balancers "targetGroupArn=<TARGET_GROUP_ARN>,
  containerName<CONTAINER_NAME>,containerPort=<CONTAINER_PORT>" \
  --force-new-deployment
```







