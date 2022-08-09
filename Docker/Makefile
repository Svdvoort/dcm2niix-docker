include envfile

build:
	docker build -t svdvoort/dcm2niix:$(VERSION) --build-arg VERSION=$(VERSION) - < Dockerfile

inspect:
	dive svdvoort/dcm2niix:$(VERSION)

run:
	docker run -it svdvoort/dcm2niix:$(VERSION)

push:
	docker push svdvoort/dcm2niix:$(VERSION)
