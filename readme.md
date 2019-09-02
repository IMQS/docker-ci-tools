# Docker CI Tools

This is a bunch of scripts that we use in Jenkins to reduce the amount of boiler-plate
that we need to include in every git repo, to run CI jobs.

For example, to run Go unit tests, you need quite a few lines in a Dockerfile to
setup the authorization so that "Go get" can fetch private repos from Github.

The aim of this repo is to provide scripts that we can re-use across different
projects, and make it easier to add CI jobs for them.