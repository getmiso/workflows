# workflows

Public repository for reusable github workflows. Be careful not to leak confidential information.

## Usage

### deploy-eks
```yml
jobs:
  deploy-eks:
    name: Deploy to EKS / ${{inputs.stage}}
    uses: getmiso/workflows/.github/workflows/deploy-eks.yml@main
    with:
      stage: ${{github.event.inputs.stage}}
      image-name: miso/${{github.event.repository.name}}
      config-path: /config/${{github.event.repository.name}}/${{github.event.inputs.stage}}
      deployment-name: ${{github.event.repository.name}}
      namespace: xxx
    secrets: inherit
```

### deploy-docker-swarm
```yml
jobs:
  deploy-docker-swarm:
    name: Deploy to Docker Swarm / ${{inputs.stage}}
    uses: getmiso/workflows/.github/workflows/deploy-docker-swarm.yml@main
    with:
      stage: ${{github.event.inputs.stage}}
      image-name: miso/${{github.event.repository.name}}
      config-path: /config/${{github.event.repository.name}}/${{github.event.inputs.stage}}
      service-name: xxx_${{github.event.repository.name}}
      server-name: swarm-manager
    secrets: inherit
```

### deploy-serverless
Runtimes other than nodejs may also be deployable.
```yml
jobs:
  deploy-docker-swarm:
    name: Deploy to Lambda / ${{inputs.stage}}
    uses: getmiso/workflows/.github/workflows/deploy-serverless.yml@main
    with:
      stage: ${{github.event.inputs.stage}}
      config-path: /config/${{github.event.repository.name}}/${{github.event.inputs.stage}}
    secrets: inherit
```

### cloudfront-invalidate-cache
```yml
jobs:
  cloudfront-invalidate-cache:
    name: Invalidate CloudFront cache
    uses: getmiso/workflows/.github/workflows/cloudfront-invalidate-cache.yml@main
    with:
      stage: ${{github.event.inputs.stage}}
      distribution-id: cloudfront distribution ID
      paths: /xxx/*
    secrets: inherit
```

### docker-build-and-push
```yml
jobs:
  docker-build-and-push:
    name: Build and Push image to ECR
    uses: getmiso/workflows/.github/workflows/docker-build-and-push.yml@main
    with:
      stage: ${{github.event.inputs.stage}}
      image-name: miso/${{github.event.repository.name}}
      config-path: /config/${{github.event.repository.name}}/${{github.event.inputs.stage}}
    secrets: inherit
```
