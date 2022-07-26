---
title: Getting Base Docker Image
description: Retrieving the exact imageID/imageName of the resulting image
cover_image: /assets/blog-img/1.first-post/ZiClJf-1920w.jpg
tags:
- tag-one
- tagtwo
date: 2022-07-08
dateHuman: 08 July, 2022
---

# ?Intro, problem description


# ?Possible solutions investigation
The Dockerfile for this article is a multistage file and I am interested in the final base image info - `nginx`
The first obvious thought was: 
> `docker images` command shows all the images on the machine, should be easy to retrieve the base image ID using `inspect` or `digest` commands output and find the image.

Lets prove this idea, `docker images` output:
```bash
TODO
> docker images
REPOSITORY   TAG              IMAGE ID       CREATED        SIZE
node         16.14.0-alpine   0e1547c0f4a4   5 months ago   110MB
node         14.19.0-alpine   755b96824e40   5 months ago   119MB
node         16.13.1-alpine   28fd30c24deb   6 months ago   110MB
```
Our target image: `TODO:tag ID`, the base image we are interested in: `TODO:16.13.1-alpine   28fd30c24deb`
Now `docker inspect TODO imageID` (the output is long and 'spoiler' - you won't find our base image ID)
```
TODO: collapsible code block element
```

Ok, maybe there is some internal ID which is different from the one we see in `docker images` output. Lets inspect our base image and find if there is *any* ID/hash we can use. 
```
TODO: collapsible code block: docker inspect base image
```

# ?Final solution


