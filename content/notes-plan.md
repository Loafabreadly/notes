+++
title = 'Note Taking Plans'
date = 2024-02-10T07:07:07-07:00
draft = false
+++
# Plan on how to host notes using Hugo + Pandoc + Docker/K8s

1. Create a repo of my personal notes, broken down by the folders matching the way I want Hugo to host said notes. ☑️
2. Write notes in the standard md format, keeping track using the private git repo ☑️
3. Setup a private docker repo ☑️
4. Create a GH Actions workflow which will
    1. Download the notes in MD format
    2. __Use pandoc to generate relevant HTML files__ Do I even need to do this?
    3. Install Hugo (& prereqs like themes)
    4. Set the entrypoint as the hugo host cmd, build the docker image
    5. Push said Docker image
5. Deploy the Docker image on my local host `http://savage.snurka.local:8123/`