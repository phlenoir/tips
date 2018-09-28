# Continuous Integration

from https://christiangalsterer.wordpress.com/2015/04/23/continuous-integration-for-pull-requests-with-jenkins-and-stash/

## Workflow

Here the workflow we try to achieve:

-    Users creates a topic branch (e.g. feature, bugfix).
-    After completing his development work and pushing his changes to Stash the user creates a pull request.
-    In order to approve a pull request we require at least one successful Jenkins build. Thereby we would like to get not only the build result of the code checked in for the pull request but get the build status after the code has been merged with the target branch.
-    When a pull request is created/updated Jenkins shall be triggered automatically for real continuous integration.
-    The source of the pull request shall be automatically merged with the target branch.
-    Set the build description with the pull request ID and a link back to the Stash pull request.
-    The build result shall be reported back to Stash.
-    Only if the build was successful and the number of successful builds configured in Stash is reached the pull request shall be approved and merged.


## Design Criteria

The following design criteria and features are addressed by this solution:

-    Re-use existing plugins as much as possible
-    Keep configuration to a minimum
-    Clear responsibility split between Stash (PR management and notification) and Jenkins (Job management and configuration)
-    Automatic merge into the correct target branch
-    Support for different Jenkins job configurations (target branches) in parallel
-    Different jobs for regular continuous integration and pull request pre-merge builds.


## Ingredients
The following ingredients are necessary for above mentioned workflow (versions available at the time or writing):

-    Jenkins (1.609)
-    Jenkins Git Plugin (2.4.0)
--        Used to checkout the code from Stash and build the correct branch
-    Pre SCM Buildstep Plugin (0.3)
-    Jenkins Stash Notifier Plugin (1.8)
--        Used to report the build result back from Jenkins to Stash
-    Pull Request Notifier for Stash (1.15)
--        Used to automatically trigger Jenkins on Pull Request creation/update.
-    Jenkins Groovy Plugin (1.26)

## Step-by-Step Configuration
Here are the steps necessary to achieve the above mentioned workflow.

1.   Install and configure Pull Request Notifier for Stash
1.   Configure Pull Request Configuration in Stash
1.   Install and configure Jenkins Git Plugin
1.   Install and configure Jenkins Stash Notifier Plugin
1.   Create/Update Jenkins job


## Appendices
### Pull request
Pull requests let you tell others about changes you've pushed to a GitHub repository. Once a pull request is sent, interested parties can review the set of changes, discuss potential modifications, and even push follow-up commits if necessary.
There are 2 main workflows when dealing with pull requests:

1.    Pull Request from a forked repository
2.    Pull Request from a branch within a repository

### Stash pullrequest builder plugin
Atlassian Stash is now called Bitbucket Server
Jenkins Plugin that builds pull requests from an Atlassian Stash instance and will report the test results.
https://wiki.jenkins.io/display/JENKINS/Stash+pullrequest+builder+plugin
