# dockerproj
This is for a docker workflow

## AWS Cloud9
1. Left bar settings - show hidden files
1. Initialize in terminal - `ssh-keygen -t rsa`
Your public key has been saved in `/home/ec2-xxx/.xxx/xxx.pub`
1. Creates public SSH key `cat /home/ec2-xxx/.xxx/xxx.pub` copy and paste
1. Copy the key to github account - settings - SSH and GPG keys - New SSH key - "title" dockerproj, "key" secret key
1. clone with SSH on github repo
1. git clone into cloud9 terminal `git clone git@github.com:gyhou/dockerproj.git` - continue connect "yes"

## dockerproj
1. `cd dockerproj` get into directory
1. `touch Makefile`
1. `touch requirements.txt`
1. `touch Dockerfile`
1. `touch app.py`

## Set up 
1. Write code into Dockerfile, app.py
1. `chmod +x app.py` - change access permission
1. test app `python app.py`
1. `python app.py --help`
1. write code in Makefile - hadolint Dockerfile
1. download hadolint `sudo wget -O /bin/hadolint https://github.com/hadolint/hadolint/releases/download/v1.17.6/hadolint-Linux-x86_64 &&\ chmod +x /bin/hadolint`
    - Shouldn't need to use this since `sudo` added
      - `sudo !!` - use higher permission to run code
    - `sudo chmod +x /bin/hadolint`
    - `make lint`
1. add click, pylint in requirment.txt

## Virutal Environment
1. `python3 -m venv ~/.dockerproj`
1. `source ~/.dockerproj/bin/activate`
1. `make install`

## Docker
1. Pull down base container to allow changes `docker build --tag=app .`
1. `docker image ls` display images, including the app created
1. shell into the container created `docker run -it app bash`
    - `ls` will show files inside the container
    - `python app.py` will run the app inside the container
    
## CircleCI config
1. `mkdir .circleci`
1. `touch .circleci/config.yml`
1. write code into config.yml
1. set up in local manual download `cd /tmp`
    - `wget https://github.com/CircleCI-Public/circleci-cli/releases/download/v0.1.7868/circleci-cli_0.1.7868_linux_amd64.tar.gz`
    - `tar zxvf circleci-cli_0.1.7868_linux_amd64.tar.gz` unpack
    - `cd circleci-cli_0.1.7868_linux_amd64`
    - `./circleci` - CircleCI command locally allows us to similute some of the commands that CircleCI would do remotely. Good to test things out
    - `mv circleci ~/`
    - `mv circleci environment/`
    - `mv circleci dockerproj/` move to main environment
    - `cd dockerproj/`
    - `./circleci local execute`
    
## Git push
- `mv circleci /tmp`
- `git status`
- `git add .circleci/`
- `git add *`
- `git commit -m "adding in Docker project"`
- `git push`

## Set up in CircleCI
- https://app.circleci.com/projects/project-dashboard/github/gyhou
- set up project
- start building
