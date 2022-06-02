# gitlab-ci Build & Push Docker images to AWS_ECR

Gitlab CI:Build & Push Docker Images to AWS ECR

aws console ecr

Repo-name 

aws cli 

aws ecr get-login-password 

aws iam user = ecr_user (programetic access)
attch policies = amazon ec2 conatiner reg poweruser

accces_key
secret_key

git lab > settings > ci-cd > variables

key = AWS_ACCESS_KEY_ID
value = (acces_key)

key = AWS_SECRET_ACCESS_KEY
value = (secret-key)




gitlab-ci.yaml
   
variables:
  DOCKER_REGISTRY: (ECR-REG)
  AWS_DEFAULT_REGION: ap-south-1 
  APP_NAME: mywebsite
  DOCKER_HOST: tcp://docker:2375

publish:
  image: 
    name: amazon/aws-cli
    entrypoint: [""]
  services:
    - docker:dind
  before_script:
    - amazon-linux-extras install docker
    - aws --version
    - docker --version 
  script:
    - docker build -t $DOCKER_REGISTRY/$APP_NAME:$CI_PIPELINE_IID .
    - aws ecr get-login-password | docker login -- useraname admin --password-stdin $DOCKER_REGISTRY
    - docker push $DOCKER_REGISTRY/$APP_NAME:$CI_PIPELINE_IID
