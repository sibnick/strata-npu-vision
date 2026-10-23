# strata-npu-vision (container image)

Publishes `ghcr.io/sibnick/strata-npu-vision`: the Strata Intel NPU picture
reader in a container, so a Core Ultra owner can try picture processing on
their NPU without building anything.  It is an experimental artifact tied to
[pull-request preparation branch `npu-vision-reader` of sibnick/Strata](https://github.com/sibnick/Strata/tree/npu-vision-reader)
and to the discussion in [Niko1221/Strata#678](https://github.com/Niko1221/Strata/issues/678),
not a release component of Strata.

```sh
podman pull ghcr.io/sibnick/strata-npu-vision:latest    # or: docker pull
```

Run it with the NPU: the README of
[container/npu-vision](https://github.com/sibnick/Strata/tree/npu-vision-reader/container/npu-vision)
in that branch carries the health check, the stdin/stdout protocol session, the
cache volume and the `vision.exe` shim.  The image contains Intel's published
driver packages for Ubuntu 24.04 (version `1.10.1.20241220-12430270326`) and
`openvino==2026.4.1`; everything else comes from Ubuntu and PyPI.

Validation honesty: GitHub runners have no NPU.  The workflow here only builds
and publishes; the image recipe was validated by hand on a Core Ultra 5 125H
with the driver pinned above, exactly as the linked README describes
(2026-10-24).  If you run the published image and the NPU shows up
(`npu_health.py` says `devices: ['CPU', 'NPU']`), that is the same check.

This repo contains only the workflow that builds and publishes; the image
recipe is built from the Strata branch above so there is one source of truth.
