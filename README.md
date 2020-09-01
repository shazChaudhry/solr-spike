# Intro _(WIP)_
This repository shows how to get a Solr cluster up and running quickly

## Deploy Solr cluster
Running the following command will start Solr cluster; spread out on each swarm node
- `docker network create --driver overlay --attachable sorl_net`
- `docker stack deploy --compose-file docker-compose.yml solr`

## Check status of the docker stack services by running the following commands
- `docker stack services solr`
- `docker stack ps --no-trunc solr` _(address any error reported at this point)_

## Deploy sample data that is bundled within Solr
- `docker container exec -it $(docker ps -q) bash` _(exec into the solr container)_
- `cd example/exampledocs`
- `java -jar -Dc=tech_products post.jar *.xml`

## Deploy sample data with NodeJS
- `cd nodeapp`
- `docker run -it --rm --name nodeapp --network=sorl_net -v "$PWD":/usr/src/app -w /usr/src/app node:latest bash`
- `npm install solr-node`
- `node index.js`

## Destroy Solr cluster
- `docker stack remove solr`

# Reference
- Getting Started Tutorial - https://youtu.be/Zw4M4NGv-Rw.  This is an excellent introduction to Solr - click on [commands](https://github.com/lucian-12/solr-course/blob/master/solr_installation_commands) that are executed in the video tutorial. Here is the official Solr getting started guide the video is referring to: https://lucene.apache.org/solr/guide/8_6/index.html
- In this first tutorial, Apache Solr is set up via Docker, and some documents added to the database: https://youtu.be/83tEFh-z9Hs
- In the second tutorial, NodeJS application is set up that talks to this solr database: https://youtu.be/ooQktBu-CXw
- Code for the last two tutorials above is found at: https://github.com/yongzhihuang/PentaCode/tree/master/solr