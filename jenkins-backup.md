#!/bin/bash

# curl --user piotrkowzan:mypassword123 -O http://127.0.0.1:8080/job/Build_docker_image_from_source_code_and_push_to_dockerhub/config.xml

joblist=(
Build_docker_image_from_source_code_and_push_to_dockerhub
)

for i in "${joblist[@]}"
  do
    curl --user username:password http://127.0.0.1:8080/job/$i/config.xml -o $i.xml
  done