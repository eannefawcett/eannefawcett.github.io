---
layout: post
title:  "Comparison of Free App Deployment Platforms for Data Science Models"
date:   2020-06-19 23:21:52
categories: technical, data science, deployment
paginator: Comparison of Free App Deployment Platforms
---

This review talks about my experiences attempting to deploy a machine learning NLP model utilizing tensorflow, keras, and nltk. I built a neural network, trained it, and fitted it before saving the model using keras's inbuilt save_model function. I saved the model and weights together in the same h5 file. I wrote a couple of functions to initialize all of things that needed to be loaded, wrote up a function to do all of the preprocessing that needed to happen before being passed into my model and ultimately classified with a prediction function. This app runs quickly utilizing three functions and only two lines of active code. [See it here!][link1] Before I went to deploy the app I ensured that it worked using local Flask.

# Heruko

[Heruko][link2] was my first choice for deployment. With the local app up and running, there really isn't any other processing or coding that's needed if your app is already on github. Theoretically, it's as simple as connecting the accounts to be ready for deployment. However, heroku does not currently support nltk's library. I learned this hard way when my build succeeded, but the live page kept showing a 404 error. So, I moved to another popular option.

# PythonAnywhere

[PythonAnywhere][link3] was my next choice. PythonAnywhere takes a bit more set up than heroku does. It is definitely more similar to a workspace. PythonAnywhere offers many more features than just app deployment, which means it's a bit more tricky to navigate. I found PythonAnywhere's tutorial for app deployment to be both resourceful and honestly necessary for me to find any form of success. There are a lot more steps required, and more familiarity with software development seems to be a huge plus. I connected my github repo to PythonAnywhere, and started following the tutorial to get started. The first thing that I found was that I had to almost immediately switch to a paid version due to my file sizes being larger than the allowed limit for free accounts. The next thing that I found was setting up a virtual environment was required for my neural network. While this wasn't hard to do, thanks to the tutorial, it did mean I had to go and check exactly what versions were installed of every library I needed to use in my app. This looks like going to your IDE, for me this meant going back to the jupyter notebook where I had originally built the model, and:
```
import library
library.__version__
```
for every library I used.

There's a lot of information out there about PythonAnywhere and keras conflicts. There seems to be some issues sometimes with tensorflow. Again, I upped the amount I was paying to increase space to allow for the full install of the keras library in my virtual environment. This seemed to work, and the next hurtle for me was configuring the WSGI file. Here, there was a Flask interaction that proved problematic. Most of the flask apps call the py file where their app is located "app.py". This creates a conflict within the pathing used by PythonAnywhere. I fixed that, or at least thought I had. When I went and looked at the Files page, the file management tool used by PythonAnywhere, I didn't see the changes I had just pushed up to my github repo. At this moment, I learned what a webhook was, and how to set one up. A webhook in github allows a third party website, like PythonAnywhere to pull down the latest version of a branch from a github repository. To be used in PythonAnywhere, some code setting up the hook must be included somewhere. I couldn't find out where, either in the app's py file or in the WSGI file. (If you know the answer to this, please reach out to me in [github][link1], thank you!) So, I opted not to do this, and uploaded the changes manually. I also realized that heroku does this automatically during the initial github linking process. Finally, I got some leverage. My app was successfully communicating with the WSGI file. However, the app couldn't build the model. There seems to be some sort of conflict between the WSGI file and the keras library.

# Conclusions

It's really great to build a model that's useful. However, the more libraries you use and the more strenuous the computing requirements are can give rise to problems and delay successful deployment. Overall, I learned a lot about how to think about generating a useful model and some of the many requirements involved. Models that show that they work and models that actually do work look very different in practice. Additionally, even if you can run a model locally, you might not be able to deploy online. Different hosting sites support different types of code and require different types of configurations to set up. I didn't need to change my py file between heroku and PythonAnywhere, but I did need to build different environments in which they would exist.


[link1]: https://github.com/eannefawcett/lexile-determination-app
[link2]: https://heroku.com
[link3]: https://pythonanywhere.com
