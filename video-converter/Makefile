DEPLOYMENT_BUCKET_NAME := devopstar
DEPLOYMENT_BUCKET_PREFIX := resources/aws-ffmpeg-serverless-convert
STACK_NAME := ffmpeg-video-converter


SOURCES=$(shell find src/)

clean:
	rm -rf build

build/output.yml: cloudformation/template.yml $(SOURCES)
	mkdir -p build
	aws cloudformation package --template-file cloudformation/template.yml --output-template-file build/output.yml --s3-bucket $(DEPLOYMENT_BUCKET_NAME) --s3-prefix $(DEPLOYMENT_BUCKET_PREFIX)

deploy: build/output.yml
	aws cloudformation deploy --template-file build/output.yml --stack-name $(STACK_NAME) --capabilities CAPABILITY_IAM
	aws cloudformation describe-stacks --stack-name $(STACK_NAME) --query Stacks[].Outputs[].OutputValue --output text

