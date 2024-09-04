FROM occlum/occlum:0.30.0-ubuntu20.04

# Install necessary tools to compile Bowtie2 from source
RUN apt-get update && apt-get install -y unzip g++

# Move to the /root directory
WORKDIR /root
# Create a folder named clone
RUN mkdir clone
# Move inside the clone folder
WORKDIR /root/clone
# Download the specified file using wget
RUN wget https://sourceforge.net/projects/bowtie-bio/files/bowtie2/2.5.4/bowtie2-2.5.4-source.zip
# Unzip the downloaded file into a folder named bowtie2
RUN unzip bowtie2-2.5.4-source.zip -d bowtie2
# Move to the bowtie2 folder
WORKDIR /root/clone/bowtie2/bowtie2-2.5.4/
# Perform the "make" command
RUN make
# Copy a directory from host to container directory
COPY bowtie_input_files/ /bowtie_input_files/

# Create the necessary directories and move files
RUN mkdir -p /root/demos/01-bow/results
RUN mkdir -p /root/demos/01-bow/ws
RUN cp /root/clone/bowtie2/bowtie2-2.5.4/bowtie2-align-s /root/demos/01-bow/bowtie2-align-s
COPY bow.yaml /root/demos/01-bow/bow.yaml

# Setup occlum workspace
WORKDIR /root/demos/01-bow/ws
RUN occlum init && rm -rf image
RUN copy_bom -f ../bow.yaml --root image --include-dir /opt/occlum/etc/template

# Example of run with 16 threads and EDMM enabled
COPY edmm.json /root/demos/01-bow/ws/Occlum.json
RUN ENABLE_EDMM=Y occlum build
RUN occlum run /bin/bowtie2-align-s -x "/bowtie_input_files/common/Homo_sapiens_assembly38" \
 -p "32" -1 "/bowtie_input_files/small/small1.fq.gz" \
 -2 "/bowtie_input_files/small/small1.fq.gz" -S "/host/sample.sam"