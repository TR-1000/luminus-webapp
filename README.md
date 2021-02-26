# simple-luminus-webapp

## Docker Flow
Login in:
```aws ecr get-login-password --region us-east-1| docker login --username AWS --password-stdin 000000000000.dkr.ecr.us-east-1.amazonaws.com```

Build the builder image to ECR: 
- ```docker build -t  000000000000.dkr.ecr.us-east-1.amazonaws.com/example-webapp-builder:$(git rev-parse HEAD) -f Dockerfile.builder .```

Run builder to build the project:
``` docker run --rm -v "$PWD:/work" 000000000000.dkr.ecr.us-east-1.amazonaws.com/example-webapp-builder:$(git rev-parse HEAD) bash -c "cd /work; lein uberjar```
for windows
``` docker run --rm -v `pwd -W`:/work 193332868148.dkr.ecr.us-east-2.amazonaws.com/example-webapp-builder:$(git rev-parse HEAD) bash -c "cd /work; lein uberjar" ```

Login in:
```aws ecr get-login-password --region us-east-1| docker login --username AWS --password-stdin 000000000000.dkr.ecr.us-east-1.amazonaws.com```

```docker push 000000000000.dkr.ecr.us-east-1.amazonaws.com/example-webapp-builder:$(git rev-parse HEAD)```

```aws ecr get-login-password --region us-east-1| docker login --username AWS --password-stdin 000000000000.dkr.ecr.us-east-1.amazonaws.com```




generated using Luminus version "2.9.12.25"

FIXME

## Prerequisites

You will need [Leiningen][1] 2.0 or above installed.

[1]: https://github.com/technomancy/leiningen

## Running

To start a web server for the application, run:

    lein run 

## License

Copyright © 2018 FIXME
