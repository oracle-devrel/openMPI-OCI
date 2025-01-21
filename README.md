# openMPI-OCI

[![License: UPL](https://img.shields.io/badge/license-UPL-green)](https://img.shields.io/badge/license-UPL-green) [![Quality gate](https://sonarcloud.io/api/project_badges/quality_gate?project=oracle-devrel_openMPI-OCI)](https://sonarcloud.io/dashboard?id=oracle-devrel_openMPI-OCI)



## Introduction

Terraform script that helps you stand up an Ampere A1 parallel computing machine on OCI that can be used for parallel programming this repo also includes several test projects you can test the environment with


**OpenMPI** is used for parallel algorithm execution allowing for integration of multiple machines into a cluster, same script can be re-used to spin up more machines and connect them together throught the --hosts argument  
 

## Requirements
1. OCI account 


## Configuration

1. Log into cloud console 
2. run the following 
```
git clone https://github.com/badr42/openMPI-OCI
cd openMPI-OCI
export TF_VAR_tenancy_ocid='<tenancy-ocid>'
export TF_VAR_compartment_ocid='<comparment-ocid>'
export TF_VAR_region='<home-region>'
export TF_VAR_core_count='2'
<optional>
# Select Availability Domain, zero based, if not set it defaults to 0
export TF_VAR_AD_number='0'
```

3. Execute the script generate-keys.sh to generate private key to access the instance
```
sh generate-keys.sh
```


## Build
To build simply execute the next commands. 
```
terraform init
terraform plan
terraform apply
```


**After applying, the service will be ready in about 25 minutes** (it will install OS dependencies, as well as the packages needed to get openMPI to work)

## Post configuration

To test the app ssh to the machine and run one of the test algorithms pre-loaded to the environment 

```
ssh -i server.key ubuntu@<instance-public-ip>
cd ~/Desktop/sharedfolder
mpirun -np 2 ./mpi-prime
```


the result should look like :

```
ubuntu@openmpi:~/Desktop/sharedfolder$ mpirun -np 20 ./mpi-prime
20 November 2022 11:55:34 AM

PRIME_MPI
  C/MPI version

  An MPI example program to count the number of primes.
  The number of processes is 20

         N        Pi          Time

         1         0        0.009797
         2         1        0.000177
         4         2        0.000106
         8         4        0.000057
        16         6        0.000117
        32        11        0.000054
        64        18        0.000055
       128        31        0.000053
       256        54        0.000055
       512        97        0.000054
      1024       172        0.000056
      2048       309        0.000103
      4096       564        0.000338
      8192      1028        0.001200
     16384      1900        0.004490
     32768      3512        0.016233
     65536      6542        0.060947
    131072     12251        0.227687
    262144     23000        0.848808
    524288     43390        3.205449
   1048576     82025       12.120073

PRIME_MPI - Master process:
  Normal end of execution.
```


## Terminating the environment
When are done please run

```
terraform destroy

```


## Building a cluster

To build a cluster you can repeat this several times to build several nodes and then connect them together as shown here
https://feyziyev007.medium.com/how-to-install-openmpi-on-ubuntu-18-04-cluster-2fb3f03bdf61



## Contributing
This project is open source.  Please submit your contributions by forking this repository and submitting a pull request!  Oracle appreciates any contributions that are made by the open source community.

## License
Copyright (c) 2024 Oracle and/or its affiliates.

Licensed under the Universal Permissive License (UPL), Version 1.0.

See [LICENSE](LICENSE.txt) for more details.

ORACLE AND ITS AFFILIATES DO NOT PROVIDE ANY WARRANTY WHATSOEVER, EXPRESS OR IMPLIED, FOR ANY SOFTWARE, MATERIAL OR CONTENT OF ANY KIND CONTAINED OR PRODUCED WITHIN THIS REPOSITORY, AND IN PARTICULAR SPECIFICALLY DISCLAIM ANY AND ALL IMPLIED WARRANTIES OF TITLE, NON-INFRINGEMENT, MERCHANTABILITY, AND FITNESS FOR A PARTICULAR PURPOSE.  FURTHERMORE, ORACLE AND ITS AFFILIATES DO NOT REPRESENT THAT ANY CUSTOMARY SECURITY REVIEW HAS BEEN PERFORMED WITH RESPECT TO ANY SOFTWARE, MATERIAL OR CONTENT CONTAINED OR PRODUCED WITHIN THIS REPOSITORY. IN ADDITION, AND WITHOUT LIMITING THE FOREGOING, THIRD PARTIES MAY HAVE POSTED SOFTWARE, MATERIAL OR CONTENT TO THIS REPOSITORY WITHOUT ANY REVIEW. USE AT YOUR OWN RISK. 