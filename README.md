# DataStax with Desktop

## About

This github covers setting up a DataStax Docker container and datastax studio.  Two main docker containers are used:  DataStax Studio and DataStax Server.  


## Getting Started
1. Prepare Docker environment
2. Pull this github into a directory  
```bash
git clone https://github.com/jphaugla/datastaxDockerStudio.git
```
3. Refer to the notes from DataStax Docker github for background on the needed DataStax images.  Directions are here:  [https://github.com/datastax/docker-images/#datastax-platform-overview](https://github.com/datastax/docker-images/#datastax-platform-overview).  Don't get too bogged down here as the included docker-compose.yaml handles most everything.
4. Open terminal and change to the github home where you will see the docker-compose.yml file, then: `docker-compose up -d`
5. Verify DataStax is working (may take a minute for datastax cassandra to startup so be patient)
```bash
docker exec dse cqlsh -e "desc keyspaces"
```
6. At this point can use the command shell from cassandra using
```bash
docker exec -it dse cqlsh
```
7. Can open the studio interface
* open browser on host computer
* http://localhost:9091
* Open the "Working with CQL worksheet"

## Conclusion
At this point, run throught the cql worksheet and enjoy playing with Cassandra!

##  Additional Notes/tips

* To get the IP address of the DataStax and openldap:

```bash
export DSE_IP=$(docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' dse)
```
   and:
```bash
export LDAP_IP=$(docker inspect -f '{{range.NetworkSettings.Networks}}{{.IPAddress}}{{end}}' openldap)
```
* use `echo $DSE_IPE` and `echo $LDAP_IP` to view
* can add to the docker compose to run additional datastax workloads such as analtyics (-k), search (-s), and graph (-g)
```bash
 command:
     -s
     -g
     -k
```
