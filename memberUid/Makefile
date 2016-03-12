IMAGE = kanboard/openldap
TAG = memberUid
CONTAINER = ldap-memberUid

image:
	@ docker build -t $(IMAGE):$(TAG) .

push:
	@ docker push $(IMAGE):$(TAG)

run:
	@ docker run --rm --name $(CONTAINER) -p 3389:389 -t $(IMAGE):$(TAG)

destroy:
	@ docker rm -f $(CONTAINER)
	@ docker rmi $(IMAGE):$(TAG)

all:
	destroy image push
