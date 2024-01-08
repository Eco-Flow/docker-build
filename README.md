# docker-build


1. To build a docker container, first choose a template from the existing builds in this repo.

2. Then edit your conda.yml and or Dockerfile to add the programs you needs.

2i. Make sure to keep the procps line, as this is needed for nf-tower

3. Then build the container (don't forget the `.`):

`docker build -t my-image .`

4. Test your container 

`docker run -it my-image bash`

or (with directory mounted):

`docker run --volume $PWD:$PWD -it my-image bash`

<Make sure to `exit` the docker container>

5. Push your working repo to dockerhub

6. `docker login -u ecoflowucl`

Then use an access token to login.

7. Tag it, e.g.:
`docker tag my-image ecoflowucl/ncbi_download`

8. Push it:
`docker push ecoflowucl/ncbi_download`