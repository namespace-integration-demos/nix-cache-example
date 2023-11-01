# Cached Nix Builds in GitHub Actions

This example demonstrates how to run Nix builds in GitHub Actions with Namespace.

Namespace dramatically speeds up the build performance by offering:

- higher performance per runner core
- flexible runner shapes (vCPU, RAM)
- local, high-performance [Cache Volumes](https://cloud.namespace.so/docs/features/faster-github-actions#cross-invocation-caching)

In the example, we [configure the Namespace runner](https://cloud.namespace.so/docs/features/faster-github-actions#configuring-a-runner) with the following block:

```yaml
    runs-on:
      - nscloud-ubuntu-22.04-amd64-4x16-with-cache
      - nscloud-cache-size-60gb
      - nscloud-cache-tag-cache-nix
```

Given this configuration, our workflow will run on a machine with 4 vCPU and 16 GB of RAM.
Also, we mount a local, high-performance cache with 60 GB size at mount point `/cache`.

Next, we bind mount `/nix` to `/cache/nix` so that Nix artifacts are fully cached between runs.

Finally, we build `netperf` with Nix.
