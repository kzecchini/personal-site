+++
title = "We'll Do it Live!"
date = 2019-10-21T13:12:56-04:00
draft = false
+++

[We'll Do it Live: Updating Machine Learning Models on Flask/uWSGI with No Downtime](https://medium.com/ww-tech-blog/well-do-it-live-updating-machine-learning-models-on-flask-uwsgi-with-no-downtime-9de8b5ffdff8)

At WW, I implemented a lightfm recommender model for their in-app social media platform. Every night the model was retrained for each global region, and the live service was updated without any downtime. The live model service was written in Flask and was deployed via k8s. I wrote a medium blog post about this for WW, which is linked at the top of the page. The post is a bit dated now, but I'm pretty proud of the work I did.

Nowadays instead of Flask I recommend using FastAPI (or starlette) for backend python API services. There are even a lot of frameworks which abstract the service layer for you to host your model directly (VertexAI, SageMaker, MLEM). 

Even if you are self hosting an ML service via k8s, I think the easiest thing to do is to just have 1 process per replica, and manage the model updates entirely via a new k8s deployment config. This should spin down old replicas, and load up new replicas with the up to date model without needing you to worry about any code on the service. 

However, this blogpost and deployment pattern may still be relevant if you want a continually running process without needing to do ops work or worry about spinning up/down infrastructure.
