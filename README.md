# docker-build

### Automatically publish containers
Once a new Dockerfile has been pushed to this repository check if a workflow yml file already exists for it.
If so, go into the actions tab and choose the relevant workflow to run.
Select "Run workflow" and the image will be built and pushed to quay.io.

If a workflow yml doesn't exist, copy an existing one i.e. `cp push-jcvi.yml push-your_image_name.yml` and then edit the following lines:
* Replace `name: Build jcvi` with `name: Build your_image_name`
* Replace `IMAGE_NAME: jcvi` with `IMAGE_NAME: your_image_name`
* Replace `IMAGE_TAG: python-3.10_last-1522` with `IMAGE_TAG: your_image_tag`

### If you want to build containers manually and publish them to quay.io then log into GitPod and do the following:
1. Build the container (don't forget the `.`):

`docker build -t my-image .`

2. Test the container 

`docker run --rm -it my-image bash`

or (with directory mounted):

`docker run --rm -it --volume $PWD:$PWD my-image bash`

<Make sure to `exit` the docker container>

3. Log in with your quay.io account

`docker login -u your-username quay.io`

and use your access token as the password.

4. Tag the image:
   
`docker tag my-image quay.io/ecoflowucl/my-image`

5. Push the image:
   
`docker push quay.io/ecoflowucl/my-image`
