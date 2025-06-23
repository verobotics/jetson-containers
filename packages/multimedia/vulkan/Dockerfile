#---
# name: vulkan
# group: multimedia
# depends: [build-essential, pip_cache, cmake, llvm]
#---
ARG BASE_IMAGE
FROM ${BASE_IMAGE}

ARG VULKAN_VERSION \
    FORCE_BUILD=off \
    TMP=/tmp/vulkan

COPY build.sh install.sh $TMP/
RUN apt-get update && \
    apt-get install -y --no-install-recommends \
        build-essential \
        cmake \
        ninja-build \
        bison \
        ocaml-core \
        xz-utils \
        pkg-config && \
    rm -rf /var/lib/apt/lists/* && \
    apt-get clean
RUN $TMP/install.sh || $TMP/build.sh || true

RUN if [ ! -f "$TMP/.vulkan" ]; then \
      echo "FAILED to install Vulkan SDK $VULKAN_VERSION"; \
      exit 1; \
    fi
