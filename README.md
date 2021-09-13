## Samples

| Repos | Build With | Registry | Docker |
| :---  | :--------- | :------- | :----- |
| [ecr-base](https://github.com/slenderslack/ecr-base) | AWS CodeBuild | ECR (private) | base FROM public official-image  |
| [ecr-service](https://github.com/slenderslack/ecr-service) | AWS CodeBuild | ECR (private) | service FROM base (private ECR image) |
| [pinning-test-gcr](https://github.com/slenderslack/pinning-test-gcr) | Google Cloud Build | GCR (private) | 
| [pinning-test-dockerhub](https://github.com/slenderslack/pinning-test-dockerhub) | DockerHub Build | DockerHub (public) |
| [pinning-test](https://github.com/slenderslack/pinning-test) | DockerHub Build | DockerHub (private) |
| [pinning-test-actions-dockerhub](https://github.com/slenderslack/pinning-test-actions-dockerhub) | GitHub Action | DockerHub (public) |
| [distroless-pinning-test](https://github.com/slenderslack/distroless-pinning-test) | Google Cloud Build | GCR (public) |

### Setting up AWS Resources

Example stack for setting up the AWS EventBridge resources for sending ECR events to Atomist (as described in [Atomist docs](https://docs.atomist.com/integration/ecr/) ).  This stack does the following:

* creates a role that Atomist can assume to get read-only access to the ECR registries in this account
* creates an api destination for AWS Event bridge, using a `Url` parameter that comes from Atomist
* creates an api connection for AWS Event bridge to whold the basic auth credentials configured in Atomist
* creates a rules to send all Image pushes and deletes to Atomist

The role `Arn` and the `ExternalId` parameter used below must be configured in the Atomist ECR integration to complete the connection.

```bash
aws cloudformation create-stack \
  --stack-name "slenderslack-eventbridge" \
  --template-body file://aws-event-bridge/template.json \
  --region us-east-1 \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameters ParameterKey=Url,ParameterValue=https://webhook.atomist.com/atomist/resource/f7584f0d-45d9-48ea-92d7-0f24c3823ec8 \
               ParameterKey=Username,ParameterValue=atomist ParameterKey=Password,ParameterValue=xxxxxxxxxx \
               ParameterKey=ExternalId,ParameterValue=xxxxxxx
```

Example stack for setting up all of the AWS CodeBuild projects used in the above examples:

```bash
aws cloudformation create-stack \
  --stack-name "slenderslack-codebuild" \
  --template-body file://aws-codebuild/template.json \
  --region us-east-1 \
  --capabilities CAPABILITY_NAMED_IAM \
  --parameters ParameterKey=AccountId,ParameterValue=xxxxxxxx
```

### Setting up GCP Resources

Example template for setting up GCR PubSub Topic subscription to send events to Atomist (as described in [Atomist docs](https://docs.atomist.com/integration/gcr/) )

```
```

Example template for setting up the Google `Cloud Build` projects used in the above examples:

```
```

### Setting up DockerHub Resources

Everything is manual (you just have to use their UI).

[codebuild-with-webhook]: https://thomasstep.com/blog/cloudformation-example-for-codebuild-with-a-webhook
