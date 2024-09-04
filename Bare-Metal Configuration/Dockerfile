FROM ubuntu:focal

# Install necessary tools to compile Bowtie2 from source
RUN apt-get update && apt-get install -y unzip wget g++ make libz-dev

# Move to the /root directory
WORKDIR /root
# Create a folder named clone
RUN mkdir clone
# Move inside the clone folder
WORKDIR /root/clone
# Download the specified file using wget and unzip sources
RUN wget https://sourceforge.net/projects/bowtie-bio/files/bowtie2/2.5.4/bowtie2-2.5.4-source.zip
RUN unzip bowtie2-2.5.4-source.zip -d bowtie2
# Move to the bowtie2 folder
WORKDIR /root/clone/bowtie2/bowtie2-2.5.4/
# Perform the "make" command
RUN make
# Copy bowtie2-align-s
RUN cp bowtie2-align-s /root/bowtie2-align-s

# Move to the /root directory
WORKDIR /root
# Copy your Bowtie2 input files
COPY bowtie_input_files/ /bowtie_input_files/

# Example of run with 16 threads
RUN ./bowtie2-align-s -S "out.sam" -x "/bowtie_input_files/common/Homo_sapiens_assembly38" \
-1 "/bowtie_input_files/small/small1.fq.gz" -2 "/bowtie_input_files/small/small2.fq.gz" -p 16