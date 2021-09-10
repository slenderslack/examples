## Samples

| Repos | Build With | Registry | Docker |
| :---  | :--------- | :------- | :----- |
| [pinning-test-ecr](https://github.com/slenderslack/pinning-test-ecr) | AWS CodeBuild | ECR | 2 Dockerfiles (service and base) - service FROM base FROM public-official-image  |
| [pinning-test-gcr](https://github.com/slenderslack/pinning-test-gcr) | Google Cloud Build | GCR | 
| [pinning-test-dockerhub](https://github.com/slenderslack/pinning-test-dockerhub) | DockerHub Build | DockerHub |
| [pinning-test](https://github.com/slenderslack/pinning-test) | DockerHub Build | DockerHub |
| [pinning-test-actions-dockerhub](https://github.com/slenderslack/pinning-test-actions-dockerhub) | GitHub Action | DockerHub |
| [distroless-pinning-test](https://github.com/slenderslack/distroless-pinning-test) | Google Cloud Build | GCR |

```
aws cloudformation create-stack \
  --stack-name "slenderslack-codebuild" \ 
  --template-body file://aws-codebuild/template.json \ 
  --region us-east-1 \
  --capabilities CAPABILITY_NAMED_IAM
  --parameters AccountId=xxxxxxxx
```


