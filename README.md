# Voting-Application

The manifest file defines a multi-service microservice architecture with four services: redis, db, result, and vote. Each service is defined using Kubernetes YAML configuration files for services and deployments.

Redis:

Service: Exposes the Redis service internally on port 6379.
Deployment: Runs a single Redis container using the redis:alpine image.
Database:

Service: Exposes the PostgreSQL database internally on port 5432.
Deployment: Runs a single PostgreSQL container using the postgres:9.4 image.
PersistentVolumeClaim: Requests a 1Gi persistent volume for the database data.
Result:

Service: Exposes the result service externally on port 80.
Deployment: Runs a single container using the kiran2361993/testing:latestappresults image.
Vote:

Service: Exposes the vote service externally on port 80.
Deployment: Runs two replicas of a container using the kiran2361993/testing:latestappvote image.
Worker:

Service: Exposes the worker service internally.
Deployment: Runs a single container using the kiran2361993/testing:latestappworker image.

++Ingress++

The Ingress  file consists of two Kubernetes Ingress resources, which are used to route traffic to backend services based on domain names and URLs.

Ingress 1: result-ingress

Host: result.pinapathrunisaikiran.co.in
SSL Certificate: nginx-tls-default
Backend Service: result (port 80)
Path Rewriting: Rewrites all incoming URLs to '/' (root path)
Ingress 2: vote-ingress

Hosts: vote.pinapathrunisaikiran.co.in and www.pinapathrunisaikiran.co.in
SSL Certificate: nginx-tls-default
Backend Service: result (port 80)
Path Rewriting: Rewrites all incoming URLs to '/' (root path)
Essentially, both Ingress resources direct traffic from the specified domain names to the 'result' service, regardless of the incoming URL path. The path rewriting ensures that all requests are treated as if they were directed to the root path.
