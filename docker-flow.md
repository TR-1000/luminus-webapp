

## ECR Repos

example-webapp	 
- 000000000000.dkr.ecr.us-east-1.amazonaws.com/example-webapp


example-webapp-builder
- 000000000000.dkr.ecr.us-east-1.amazonaws.com/example-webapp-builder


## Commands

##### Login in to aws
```aws ecr get-login-password --region us-east-1| docker login --username AWS --password-stdin 000000000000.dkr.ecr.us-east-1.amazonaws.com```

##### Build the Dockerfile.builder image and tag with registry and current git hash
```docker build -t  000000000000.dkr.ecr.us-east-1.amazonaws.com/example-webapp-builder:$(git rev-parse HEAD) -f Dockerfile.builder . ```

##### Push builder image to ECR
```docker push 000000000000.dkr.ecr.us-east-1.amazonaws.com/example-webapp-builder:$(git rev-parse HEAD)```

##### Run builder image to copy over files and build the project
```docker run --rm -v "$PWD:/work" 000000000000.dkr.ecr.us-east-1.amazonaws.com/example-webapp-builder:$(git rev-parse HEAD) bash -c "cd /work; lein uberjar```

( windows powershell ```docker run --rm -v `pwd -W`:/work 193332868148.dkr.ecr.us-east-2.amazonaws.com/example-webapp-builder:$(git rev-parse HEAD) bash -c "cd /work; lein uberjar" ```)


##### Build form the default Dockerfile
```docker build -t 000000000000.dkr.ecr.us-east-1.amazonaws.com/example-webapp:$(git rev-parse HEAD) .```

##### Push project image to ERC
```docker push 000000000000.dkr.ecr.us-east-1.amazonaws.com/example-webapp:$(git rev-parse HEAD)```


##### Run the container
```docker run --rm -d -p 3000:3000 193332868148.dkr.ecr.us-east-2.amazonaws.com/example-webapp:$(git rev-parse HEAD)```



---
