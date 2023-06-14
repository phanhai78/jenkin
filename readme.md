
docker build -t myjenkins-blueocean:2.332.3-1 .

khoi chay
docker pull devopsjourney1/jenkins-blueocean:2.332.3-1 && docker tag devopsjourney1/jenkins-blueocean:2.332.3-1 myjenkins-blueocean:2.332.3-1

tao mang rieng cho container
docker network create jenkins

chay lenh duoi che do backgroud

docker run --name jenkins-blueocean --restart=on-failure --detach `
  --network jenkins --env DOCKER_HOST=tcp://docker:2376 `
  --env DOCKER_CERT_PATH=/certs/client --env DOCKER_TLS_VERIFY=1 `
  --volume jenkins-data:/var/jenkins_home `
  --volume jenkins-docker-certs:/certs/client:ro `
  --publish 8080:8080 --publish 50000:50000 myjenkins-blueocean:2.332.3-1

lay pass
docker exec jenkins-blueocean cat /var/jenkins_home/secrets/initialAdminPassword

truy cap
https://localhost:8080/
