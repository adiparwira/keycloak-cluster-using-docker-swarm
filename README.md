# keycloak-cluster-using-docker-swarm

# download the following file
mkdir cli
cd cli

wget https://raw.githubusercontent.com/fit2anything/keycloak-cluster-setup-and-configuration/master/src/TCPPING.cli
wget https://raw.githubusercontent.com/fit2anything/keycloak-cluster-setup-and-configuration/master/src/JDBC_PING.cli

cd ..

# create docke file
FROM jboss/keycloak:latest
ADD cli/TCPPING.cli /opt/jboss/tools/cli/jgroups/discovery/
ADD cli/JDBC_PING.cli /opt/jboss/tools/cli/jgroups/discovery/
HEALTHCHECK --interval=30s --timeout=1s --retries=3 CMD curl -k --fail http://localhost:8080/auth/ || exit 1

# build docker image
docker build -t aryadi/keycloak:14.0.0 .

# create a docker-compose file


# run docker stact deploy
docker stack deploy -c docker-compose.yml keycloak

# check log keycloak service
docker service logs keycloak

# check container status
docker ps




