# DOCUMENTATION

## Jupyter Container
```bash
# build the image
docker build -t jupyter-demo .

# run the container
# mounts current directory as /notebooks
docker run --name jupyter-notebooks -p 8888:8888 -v ${PWD}:/notebooks jupyter-demo
```
Open http://localhost:8888 in your browser

## Spark Cluster Docker compose

Navigate to the project root before anything

### Start the cluster
```bash
docker compose -f infrastructure/docker-compose.spark.yml up -d --build
```

-d runs containers in the background. --build rebuilds images if any files changed.

### Stop the cluster
```bash
docker compose -f infrastructure/docker-compose.spark.yml stop
```

Containers are stopped but not removed. Data and state are preserved

### Restart the cluster
```bash
docker compose -f infrastructure/docker-compose.spark.yml restart
```

### Tear down completely (removes containers)
```bash
docker compose -f infrastructure/docker-compose.spark.yml down
```

Add -v to also remove named volumes: down -v

---

## Useful Commands
```bash
# check running containers
docker ps

# check all containers
docker ps -a

# view live logs for the jupyter service
docker compose -f infrastructure/docker-compose.spark.yml logs -f jupyter

# view logs for all services
docker compose -f infrastructure/docker-compose.spark.yml logs -f
```

---

## AWS SSO

Download the SSO config file from the link provided by your admin and paste the URL into your browser to complete authentication.
```bash
# Authenticate via AWS SSO
aws sso login --profile <your-profile-name>

# Verify your identity
aws sts get-caller-identity --profile <your-profile-name>
```