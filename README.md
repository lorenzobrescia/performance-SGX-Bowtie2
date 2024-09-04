# Performance Analysis on DNA Alignment Workload with Intel SGX Multithreading
In this repository there are all the configurations used in the paper:
[Waiting for full record name]

The input files of Bowtie2 are confidential and so they are not public. Placeholders files were used within the various configurations, which can be replaced: small1.fq.gz, small2.fq.gz, and Homo_sapiens_assembly38_FILES

The Dockerfiles examples execute a single time; to obtain the results published in the reference paper, Bash scripts were used to automate the repetition of the various executions.

## Notes on Gramine Configuration
In the Dockerfile it is necessary to specify all files to copy from Host to the container.

In the Makefile the architecture library must be specified for the Gramine enclave. In our case (Rocky Linux) was "/lib/x86_64-linux-gnu/".

## Occlum Configuration
In the folder are specified two .json files (edmm.json and no_edmm.json). The default Dockerfile run an instance of Occlum with EDMM enabled. If you want to run without EDMM just change this line
`COPY edmm.json /root/demos/01-bow/ws/Occlum.json` with this `COPY no_edmm.json /root/demos/01-bow/ws/Occlum.json`