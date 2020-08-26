# awx-ee-test
AWX execution environment personal test

Command from testing locally:

```
ansible-builder build -f input/execution-environment.yml --container-runtime=docker -c build_context --tag quay.io/alancoding/awx-ee:latest
```

Then attempting to put on build trigger with:

https://quay.io/repository/alancoding/awx-ee

This should demonstrate that once a build-context is produced, `ansible-builder`
will not be necessary because the build context and be reused.
The `build_context` folder here was programatically produced from the `-c`
option passed to `ansible-builder build`.

Content in the `input` folder are from the folder `tests/data/awx` in ansible-builder.

### Rebuilding

Say you do not have `ansible-builder` installed, nor do you want it.
You just want to build an image from what I already have.

```
docker build --rm=true -f build_context/Dockerfile --build-arg TAG=2.9 -t quay.io/alancoding/awx-ee:2.9 build_context
```

This will build a version with Ansible 2.9.
You may want to substitute your own quay.io account for alancoding.

### Using, testing

Okay, so now that an image has been built, let's make sure we pull that from
quay.io (not using a local copy) and test its function inside of ansible-runner.

```
docker rmi quay.io/alancoding/awx-ee
```

I duplicated some more test content in the `runner` folder.

```
ansible-runner run --playbook awx.yml runner -v
```

note specifically the contents of `runner/env/settings`, and how
it points to `quay.io/alancoding/awx-ee`, and will download the `latest` tag
when you run it.
