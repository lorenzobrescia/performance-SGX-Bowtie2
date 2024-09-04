FROM gramineproject/gramine:stable-focal

# Install necessary tools to compile Bowtie2 from source
RUN apt-get update && apt-get install -y unzip wget g++ make libz-dev

# Move to the /root directory
WORKDIR /root
# Create a folder named clone
RUN mkdir clone
# Move inside the clone folder
WORKDIR /root/clone
# Download the specified file using wget and unzip suources
RUN wget https://sourceforge.net/projects/bowtie-bio/files/bowtie2/2.5.4/bowtie2-2.5.4-source.zip
RUN unzip bowtie2-2.5.4-source.zip -d bowtie2
# Move to the bowtie2 folder
WORKDIR /root/clone/bowtie2/bowtie2-2.5.4/
# Perform the "make" command
RUN make
# Copy bowtie2-align-s
RUN cp /root/clone/bowtie2/bowtie2-2.5.4/bowtie2-align-s /root/small/bowtie2-align-s

# Create the necessary directories
RUN mkdir -p /root/small/results
RUN mkdir -p /root/small/input/plain

# Copy files from host
WORKDIR /root
COPY Makefile /root/small/Makefile
COPY manifest /root/small/manifest.template
COPY bowtie_input_files/common/* /root/small/input/plain
COPY bowtie_input_files/small/* /root/small/input/plain

# Create the key for Gramine tools
RUN gramine-sgx-gen-private-key

# Example of run with 16 threads and EDMM enabled
WORKDIR /root/small
RUN make ths=16 edmm=1 
RUN gramine-sgx bow