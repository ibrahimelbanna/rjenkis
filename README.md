# jenkins



[![Project Status: Active – The project has reached a stable, usable state and is being actively developed.](http://www.repostatus.org/badges/latest/active.svg)](http://www.repostatus.org/#active)
[![Build Status](https://travis-ci.org/ropensci/jenkins.svg?branch=master)](https://travis-ci.org/ropensci/jenkins)
[![AppVeyor Build Status](https://ci.appveyor.com/api/projects/status/github/ropensci/jenkins?branch=master&svg=true)](https://ci.appveyor.com/project/jeroen/jenkins)
[![CRAN_Status_Badge](http://www.r-pkg.org/badges/version/jenkins)](http://cran.r-project.org/package=jenkins)
[![CRAN RStudio mirror downloads](http://cranlogs.r-pkg.org/badges/jenkins)](http://cran.r-project.org/web/packages/jenkins/index.html)

> Simple Jenkins Client for R

Manage jobs and builds on your Jenkins CI server <https://jenkins.io/>. 
Create and edit projects, trigger builds, manage build queues, download build
logs, and much more.
JENKINS_PAT=3858f62230ac3c915f300c664312c63f
```

Now you connect to your Jenkins server and do stuff:

```r
# Make a connection
jk <- jenkins(server = 'http://jenkins.ropensci.org', username = 'jeroen')

# Do stuff
jk$server_info()
jk$project_build('magick')

# It's now in the queue
jk$queue_list()

# Check build status
jk$build_info('magick')

# Get latest build log
jk$build_log('magick', build_id = 'lastCompletedBuild')
```
