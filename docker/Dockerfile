# Copyright (c) 2019-2021 VMware, Inc. All Rights Reserved.
# SPDX-License-Identifier: BSD-2-Clause

FROM python:3.9-slim-bullseye as base

FROM base as builder

RUN mkdir /install
WORKDIR /install

RUN pip install --no-warn-script-location --prefix=/install \
    tern

FROM base

RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    attr \
    findutils \
    fuse-overlayfs/bullseye \
    fuse3/bullseye \
    git \
    jq \
    skopeo \
    && rm -rf /var/lib/apt/lists/*

COPY --from=builder /install /usr/local

ENTRYPOINT ["tern"]
CMD ["--help"]
