# Performance Analysis on DNA Alignment Workload with Intel SGX Multithreading
Our reference paper is [this](https://ceur-ws.org/Vol-3785/paper107.pdf), to cite us use the following:
```
@inproceedings{brescia2024performance,
  title={Performance analysis on DNA alignment workload with Intel SGX multithreading},
  author={Brescia, Lorenzo and Colonnelli, Iacopo and Aldinucci, Marco and others},
  booktitle={CEUR WORKSHOP PROCEEDINGS},
  volume={3785},
  pages={13--24},
  year={2024},
  organization={CEUR-WS}
}
```

The input files of Bowtie2 are confidential and so they are not public. Placeholders files were used within the various configurations, which can be replaced: small1.fq.gz, small2.fq.gz, and Homo_sapiens_assembly38_FILES

The Dockerfiles examples execute a single time; to obtain the results published in the reference paper, Bash scripts were used to automate the repetition of the various executions.

## Notes on Gramine Configuration
In the Dockerfile it is necessary to specify all files to copy from Host to the container.

In the Makefile the architecture library must be specified for the Gramine enclave. In our case (Rocky Linux) was "/lib/x86_64-linux-gnu/".

## Occlum Configuration
In the folder are specified two .json files (edmm.json and no_edmm.json). The default Dockerfile run an instance of Occlum with EDMM enabled. If you want to run without EDMM just change this line
`COPY edmm.json /root/demos/01-bow/ws/Occlum.json` with this `COPY no_edmm.json /root/demos/01-bow/ws/Occlum.json`
