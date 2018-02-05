# IPython on BlueMix

Deploys a throw-away data analysis environment on BlueMix including IPython Notebook, numpy, pandas, and matplotlib. See the quickstart below or [the developerWorks article](http://www.ibm.com/developerworks/cloud/library/cl-ipython-app/index.html) for details.

# Quickstart

First, get Cloud Foundry Command Line tools (cf) for your machine. Then,

```
# get the code
git clone https://github.com/AbhishekGhosh/Bluemix-Jupyter-Notebook.git
cd Bluemix-Jupyter-Notebook
# Update the buildpack in manifest.yml to:
# https://github.com/cloudfoundry/python-buildpack.git
# login to bluemix
cf api https://api.ng.bluemix.net
cf login
# push the app, but don't start it
cf push --no-start
# set a password in the app environment if you need
# cf set-env ipython PASSWORD $( echo -n "Password: " && read -s PASSWORD && echo $PASSWORD )
# In windows the above fails, use:
# cf set-env ipython PASSWORD recent ipython
# build, deploy, and start the app
cf start ipython
# Confirm that the notebook server is running properly by querying its status:
cf app ipython
# The output provides the URL where the notebook is running. 
```

When the buildpack finishes running, note the route assigned to your instance and visit it in your browser via https://your-instance.nb.bluemix.net. Enter your password when prompted.

# Troubleshooting

Sometimes the buildpack takes too long to execute. Though it completes and the app runs, it surfaces as a staging error. If you see this error, run:

```
cf stop
cf start
```

# License

Copyright (c) 2014 IBM Corporation under the MIT license. See License.txt for details.
