BASE_DIRECTORY:=$(shell git rev-parse --show-toplevel)
GIT_TAG:=$(shell cat GIT_TAG)
GOLANG_VERSION?="1.17"

APPMESH_VERSION:=$(shell cat APPMESH_VERSION)
IMAGE_BUILD_ARGS=APPMESH_VERSION

REPO=emissary
REPO_OWNER=emissary-ingress

EXCLUDE_FROM_STAGING_BUILDSPEC=true
BINARY_TARGET_FILES=busyambassador capabilities_wrapper example-envoy-metrics-sink k8sregistryctl kat-client kat-server
SOURCE_PATTERNS=./cmd/busyambassador ./cmd/capabilities_wrapper ./cmd/example-envoy-metrics-sink ./cmd/k8sregistryctl ./cmd/kat-client ./cmd/kat-server

EMISSARY_IMAGE_COMPONENT=emissary-ingress/emissary

IMAGE_NAMES=emissary
DOCKERFILE_FOLDER=./docker/linux/emissary-image

BASE_IMAGE_NAME?=eks-distro-minimal-base-python

HAS_HELM_CHART=true
HELM_DIRECTORY=charts/emissary-ingress
HELM_DESTINATION_REPOSITORY=emissary-ingress/emissary
HELM_IMAGE_LIST=emissary-ingress/emissary

AMBASSADOR_VERSION_TARGET=$(REPO)/python/ambassador.version

include $(BASE_DIRECTORY)/Common.mk


$(GO_MOD_DOWNLOAD_TARGETS): $(AMBASSADOR_VERSION_TARGET)

# do not pass our makeflags down to emissary make since there will be unncessary warnings
$(AMBASSADOR_VERSION_TARGET): MAKEFLAGS=
$(AMBASSADOR_VERSION_TARGET):
	@export VERSION="v3.0.0" && export CHART_VERSION=$(CHART_VERSION) && cd emissary && GOPATH=/var && make python/ambassador.version


########### DO NOT EDIT #############################
# To update call: make add-generated-help-block
# This is added to help document dynamic targets and support shell autocompletion
# Run make help for a formatted help block with all targets
include Help.mk
########### END GENERATED ###########################
