# Docker CI Tools

## WARNING! This repo is public.

All secrets must live in Jenkins, and pass in through command-line parameters.

## Do not embed secrets in these scripts.

---

This is a bunch of scripts that we use in Jenkins to reduce the amount of boiler-plate that we need to include in every git repo, to run CI jobs.

For example, to run Go unit tests, you need quite a few lines in a Dockerfile to setup the authorization so that "Go get" can fetch private repos from Github.

The aim of this repo is to provide scripts that we can re-use across different projects, and make it easier to add CI jobs for them.

# Jenkins Recipes

## Run Go Tests
* Enable `Use secret texts(s) or files(s)`, and add the SSH Private Key `imqs-deploybot`, and name the variable `SSH_KEY`
```bash
wget -O run-go-tests https://raw.githubusercontent.com/IMQS/docker-ci-tools/master/run-go-tests
bash ./run-go-tests "$(cat $SSH_KEY)" go test -v github.com/IMQS/package/name
```
* The `-v` flag for `go test` is essential, but you can also add any other flags that you might need, such as `-cpu 2`, or `-race`.
* In post-build settings, consume JUnit test output from `test-output/*.xml`