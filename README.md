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
