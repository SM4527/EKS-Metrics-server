<p align="center">

![Kubernetes](https://img.shields.io/badge/kubernetes-%23326ce5.svg?style=for-the-badge&logo=kubernetes&logoColor=white) ![AWS](https://img.shields.io/badge/AWS-%23FF9900.svg?style=for-the-badge&logo=amazon-aws&logoColor=white) ![Terraform](https://img.shields.io/badge/terraform-%235835CC.svg?style=for-the-badge&logo=terraform&logoColor=white) ![Docker](https://img.shields.io/badge/docker-%230db7ed.svg?style=for-the-badge&logo=docker&logoColor=white) ![Shell Script](https://img.shields.io/badge/shell_script-%23121011.svg?style=for-the-badge&logo=gnu-bash&logoColor=white)

![Stars](https://img.shields.io/github/stars/SM4527/EKS-Metrics-server?style=for-the-badge) ![Forks](https://img.shields.io/github/forks/SM4527/EKS-Metrics-server?style=for-the-badge) ![Issues](https://img.shields.io/github/issues/SM4527/EKS-Metrics-server?style=for-the-badge) ![License](https://img.shields.io/github/license/SM4527/EKS-Metrics-server?style=for-the-badge)

</p>

# Project Title

EKS-Metrics-server [![Tweet](https://img.shields.io/twitter/url/http/shields.io.svg?style=social)](https://twitter.com/intent/tweet?text=EKS%20-%20Metrics%20-%20server&url=https://github.com/SM4527/EKS-Metrics-server)

## Description

Deploy Metrics server on an EKS cluster using Terraform and Helm.

<p align="center">

![image](https://user-images.githubusercontent.com/78129381/153617097-b79eb515-aadf-4a32-97cb-b1507c408e83.png)

</p>

## Getting Started

### Dependencies

* Docker
* AWS user with programmatic access and high privileges 
* Linux terminal
* Deploy an [EKS K8 Cluster](https://github.com/SM4527/EKS-Terraform) with Self managed Worker nodes on AWS using Terraform.

### Installing

* Clone the repository
* Set environment variable TF_VAR_AWS_PROFILE
* Review terraform variable values in variables.tf, locals.tf
* Override values in the Helm chart through the "chart_values.yaml" file
* Update kubernetes.tf with the AWS S3 bucket name and key name from the output of the [EKS K8 Cluster](https://github.com/SM4527/EKS-Terraform/blob/master/outputs.tf)

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

* metrics-server is unable to authenticate to apiserver

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
