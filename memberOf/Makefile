IMAGE = kanboard/openldap
TAG = memberOf
CONTAINER = ldap-memberOf

image:
	@ docker build -t $(IMAGE):$(TAG) .

push:
	@ docker push $(IMAGE):$(TAG)

run:
	@ docker run --rm --name $(CONTAINER) -p 4389:389 -t $(IMAGE):$(TAG)

destroy:
	@ docker rm -f $(CONTAINER)
	@ docker rmi $(IMAGE):$(TAG)

all:
	destroy image push
