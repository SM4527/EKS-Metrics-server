# Project Title

EKS-Metrics-server

## Description

Deploy Metrics server on an EKS cluster using Terraform and Helm.

## Getting Started

### Dependencies

* docker & docker-compose
* aws user with programmatic access and high privileges 
* linux terminal
* Deploy an [EKS K8 Cluster](https://github.com/SM4527/EKS-Terraform) with Self managed Worker nodes on AWS using Terraform.

### Installing

* clone the repository
* set environment variable TF_VAR_AWS_PROFILE
* review terraform variable values in variables.tf, locals.tf
* override values in the Helm chart through the "chart_values.yaml" file
* update kubernetes.tf with the AWS S3 bucket name and key name from the output of the [EKS K8 Cluster](https://github.com/SM4527/EKS-Terraform/blob/master/outputs.tf)

### Executing program

* Configure AWS user with AWS CLI.

```
docker-compose run --rm aws configure --profile $TF_VAR_AWS_PROFILE

docker-compose run --rm aws sts get-caller-identity
```

* Specify appropriate Terraform workspace.

```
docker-compose run --rm terraform workspace show

docker-compose run --rm terraform workspace select default
```

* Run Terraform apply to create the EKS cluster, k8 worker nodes and related AWS resources.

```
./run-docker-compose.sh terraform init

./run-docker-compose.sh terraform validate

./run-docker-compose.sh terraform plan

./run-docker-compose.sh terraform apply
```

* Verify kubectl calls and ensure Metrics server Pod is in Running status.

```
./run-docker-compose.sh kubectl get pods -A | grep -i metric
```

* Check out top nodes and pods by CPU & Memory consumption on the EKS cluster.

```
./run-docker-compose.sh kubectl top node

./run-docker-compose.sh kubectl top pod -A
```

## Help

* metrics-server unable to authenticate to apiserver

```
Issue: kubectl top node and pod shows unknown instead of perencentage. The pod log and event has the error: dial tcp ip_address: i/o timeout

Fix:
Check chart_values.yaml
```

Reference: https://github.com/kubernetes-sigs/metrics-server/issues/278

## Authors

[Sivanandam Manickavasagam](https://www.linkedin.com/in/sivanandammanickavasagam)

## Version History

* 0.1
    * Initial Release

## License

This project is licensed under the MIT License - see the LICENSE file for details

## Repo rosters

### Stargazers

[![Stargazers repo roster for @SM4527/EKS-Metrics-server](https://reporoster.com/stars/dark/SM4527/EKS-Metrics-server)](https://github.com/SM4527/EKS-Metrics-server/stargazers)
