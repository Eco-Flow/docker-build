# docker-build

### Automatically publish containers
Once a new Dockerfile has been pushed to this repository check if a workflow yml file already exists for it.
If so, go into the actions tab and choose the relevant workflow to run.
Select "Run workflow" and the image will be built and pushed to quay.io.

If a workflow yml doesn't exist there are a few steps needed.

Firstly, ensure that an empty repository with the appropriate name is created in quay.io. Then make sure the dockerbuild robot has write permissions to that new repository.

Once that is completed, you can create a new workflow yaml.

Copy an existing workflow yaml i.e. `cp push-jcvi.yml push-your_image_name.yml` and then edit the following lines:
* Replace `name: Build jcvi` with `name: Build your_image_name`
* Replace `IMAGE_NAME: jcvi` with `IMAGE_NAME: your_image_name`
* Replace `IMAGE_TAG: python-3.10_last-1522` with `IMAGE_TAG: your_image_tag`

### If you want to build containers manually and publish them to quay.io then log into GitPod and do the following:
1. Build the container (don't forget the `.`):

`docker build -t my-image .`

use flag `-f` to specifically choose a Dockerfile, else it will assume `Dockerfile`

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

with a tag that is appropriate `quay.io/ecoflowucl/my-image:v1.0`

and change my-image to an appropriate name, all in lower case.

5. Push the image:
   
`docker push quay.io/ecoflowucl/my-image`

6. Make repo public on Quay.io

Go to settings on the Quay webpage for ecoflow

7. Go to Quay.io settings, and allow robot account access to write to repo

<img width="814" alt="image" src="https://github.com/Eco-Flow/docker-build/assets/9978862/997f2e58-b601-4112-8405-1f512d1e890e">

8. Also you need to create a github action file for this repository. 

In `.github/workflows`.

Copy an example that exists for your container.

9. Go to Github and run the container build actions.

### Listed below are containers cannot be built with actions
pearrm - requires you buying software (free for academics) so uses local copy that can't be added to repo
