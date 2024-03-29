# Ubuntu Linux as the base image
FROM ubuntu:22.04

# Set UTF-8 encoding
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8

# Install Python
RUN apt-get -y update && \
    apt-get -y upgrade
# The following line ensures that the subsequent install doesn't expect user input
ENV DEBIAN_FRONTEND=noninteractive
RUN apt-get -y install python3-pip python3-dev

# Install spaCy
RUN pip3 install --upgrade pip
RUN pip3 install spacy
RUN python3 -m spacy download en_core_web_lg
RUN pip3 install torch torchvision torchaudio --extra-index-url https://download.pytorch.org/whl/cpu
RUN pip3 install transformers
RUN pip3 install sentencepiece
RUN pip3 install --upgrade protobuf==3.20.0

RUN pip3 install crosslingual-coreference
RUN pip3 install Pillow==9.0.0
RUN python3 -m spacy download en_core_web_sm

RUN pip3 install unidecode
RUN pip3 install autocorrect
RUN pip3 install nltk
RUN pip3 install datasets
RUN pip3 install pinecone-client
RUN pip3 install -U sentence-transformers

# Add the files into container, under QA folder, modify this based on your need
RUN mkdir /QA
ADD ask /QA
ADD answer /QA
ADD answer_other.py /QA
ADD to_pronoun.py /QA
ADD paraphrase.py /QA
ADD preprocess_qg.py /QA
ADD preprocess_qa.py /QA
ADD context_upsert.py /QA
ADD retriever /QA/retriever

# Change the permissions of programs
CMD ["chmod 777 /QA/*"]

# Set working dir as /QA
WORKDIR /QA
ENTRYPOINT ["/bin/bash", "-c"]
