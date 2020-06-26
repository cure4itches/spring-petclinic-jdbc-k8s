# K8s version of Spring PetClinic Sample Application built with Spring Data JDBC

This is a branch of the [Spring PetClinic Sample Application built with Spring Data JDBC](https://github.com/spring-petclinic/spring-petclinic-data-jdbc)

Additionally:

- uses Gradle and Docker for build
- uses K8s for Execution

# How to Build
1. Build the spring boot app - petclinic
$ ./gradlew build
2. Build the docker image
$ ./gradlew dockerBuildImage
>> The name of the docker image is 'petclinic:1.0' and 'petclinic:latest'. You can tag them and push to Docker Hub or your private docker registry.

# How to Run(on K8s):
1. move to k8s directory
> $ cd k8s
2. Create PV for MySQL DB
> $ kubectl create -f mysql-pv.yaml
>> Warning: It uses a 'hostPath' typed volume so you should choose other type of PV like awsElasticBlockStore, gcePersistentDisk, nfs.
3. Create Deployment and Service(ClusterIP) of MySQL app
> $ kubectl create -f mysql-deployment.yaml
4. Before running petclinic app, you should create a directory for logging on each worker node
> $ mkdir /logs && chown 1000:1000 /logs
5. Create Deployment and Service and Ingress(for nginx ingress controller) of petclinic app
> $ kubectl create -f petclinic-deployment.yaml

