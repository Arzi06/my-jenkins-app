account = $(shell aws sts get-caller-identity --query "Account" --output text)
stage = dev
include ../stages/$(stage)
image = $(account).dkr.ecr.us-east-1.amazonaws.com/data:$(version)


login:
	aws ecr get-login-password --region us-east-1 | docker login --username AWS --password-stdin $(account).dkr.ecr.us-east-1.amazonaws.com

build:
	@docker build -t $(image) .

push: login
	@# docker login is not here
	@docker push $(image)

deploy:
	@cat data-secret.yaml | sed "s|NAMESPACE|$(namespace)|g" | kubectl apply -f -
	@cat back-deployment.yaml | sed "s|IMAGEVERSION|$(version)|g;s|NAMESPACE|$(namespace)|g;s|ACCOUNT|$(account)|g" | kubectl apply -f -