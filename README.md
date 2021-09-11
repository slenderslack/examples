## Samples

| Repos | Build With | Registry | Docker |
| :---  | :--------- | :------- | :----- |
| [ecr-base](https://github.com/slenderslack/ecr-base) | AWS CodeBuild | ECR | base FROM public-official-image  |
| [ecr-service](https://github.com/slenderslack/ecr-service) | AWS CodeBuild | ECR | service FROM base (private ECR image) |
| [pinning-test-gcr](https://github.com/slenderslack/pinning-test-gcr) | Google Cloud Build | GCR | 
| [pinning-test-dockerhub](https://github.com/slenderslack/pinning-test-dockerhub) | DockerHub Build | DockerHub |
| [pinning-test](https://github.com/slenderslack/pinning-test) | DockerHub Build | DockerHub |
| [pinning-test-actions-dockerhub](https://github.com/slenderslack/pinning-test-actions-dockerhub) | GitHub Action | DockerHub |
| [distroless-pinning-test](https://github.com/slenderslack/distroless-pinning-test) | Google Cloud Build | GCR |

### Setting up AWS Resources

Example stack for setting up all of the AWS CodeBuild projects used in the above examples:

```
aws cloudformation create-stack \
  --stack-name "slenderslack-codebuild" \
  --template-body file://aws-codebuild/template.json \
  --region us-east-1 \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameters ParameterKey=AccountId,ParameterValue=xxxxxxxx
```

Example stack for setting up the AWS EventBridge resources for sending ECR events to Atomist (as described in [Atomist docs]() ) 

```
aws cloudformation create-stack \
  --stack-name "slenderslack-eventbridge" \
  --template-body file://aws-event-bridge/template.json \
  --region us-east-1 \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameters ParameterKey=AccountId,ParameterValue=xxxxxxxx ParameterKey=AtomistWebhook,ParameterValue=
```

[codebuild-with-webhook]: https://thomasstep.com/blog/cloudformation-example-for-codebuild-with-a-webhook
