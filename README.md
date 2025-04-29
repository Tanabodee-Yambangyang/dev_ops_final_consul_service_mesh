# 2025-DevOps and Microservices
## Service Mesh with HashiCorp Consul 

### 📂 terraform/
This folder contains Terraform configuration files for provisioning cloud infrastructure and managing settings.

- ```data.tf``` -> It retrieves a list of available AWS availability zones in the region configured in the provider block
  
- ```main.tf``` -> 	The main Terraform configuration file that defines infrastructure resources and modules, like VPC, EKS cluster, and more.

- ```providers.tf``` -> 	Specifies the cloud providers and tools (AWS, Helm, Kubernetes) Terraform will interact with, including authentication details.

- ```variables.tf``` -> Lists all variables and their optional default values that can be configured for the infrastructure setup.

### 📂 kubernetes/
This folder contains configuration files for deploying applications and services to your Kubernetes cluster, both with and without Consul service discovery.

- ```config.yaml```	Defines deployments and services for your online store application, without any Consul integration.
  
- ```config-consul.yaml```	Similar to config.yaml, but includes annotations for Consul service discovery, allowing Consul to track and manage these services.
  
- ```consul-values.yaml```	Configuration values used when installing Consul via a Helm chart. These values customize the Consul installation settings.
  
- ```consul-mesh-gateway.yaml```	A deployment definition for a Consul Mesh Gateway, enabling communication across multiple datacenters or Kubernetes clusters.
  
- ```exported-service.yaml```	Specifies a service that should be shared with other Consul datacenters or clusters for cross-cluster communication.
  
- ```service-resolver.yaml```	Configures how Consul should resolve a particular service name, such as defining fallback services if the primary one is unavailable.

### Demo project accompanying a [Consul crash course video](https://www.youtube.com/watch?v=s3I1kKKfjtQ) on YouTube


Terraform commands to execute the script

```sh
# initialise project & download providers
terraform init

# preview what will be created with apply & see if any errors
terraform plan

# exeucute with preview
terraform apply -var-file terraform.tfvars

# execute without preview
terraform apply -var-file terraform.tfvars -auto-approve

# destroy everything
terraform destroy

# show resources and components from current state
terraform state list
```

#### Get access to EKS cluster
```sh
# install and configure awscli with access creds
aws configure

# check existing clusters list
aws eks list-clusters --region eu-central-1 --output table --query 'clusters'

# check config of specific cluster - VPC config shows whether public access enabled on cluster API endpoint
aws eks describe-cluster --region eu-central-1 --name myapp-eks-cluster --query 'cluster.resourcesVpcConfig'

# create kubeconfig file for cluster in ~/.kube
aws eks update-kubeconfig --region eu-central-1 --name myapp-eks-cluster

# test configuration
kubectl get svc
```
