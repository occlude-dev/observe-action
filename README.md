# Occlude Observation recorder

**Pre-release, not for use.** This release exists to test the Action on GitHub-hosted runners. It makes no promise about what it records or sends, and it may be withdrawn.

## Use

Pin the Action by its full commit, never by a tag.

```yaml
name: Occlude Observation
on:
  workflow_dispatch:
    inputs:
      run-id:
        description: The Observation run id
        required: true
permissions:
  contents: read
jobs:
  observe:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@<commit>   # pin by commit
      - run: npm ci
      - run: sudo apt-get install -y strace
      - uses: occlude-dev/observe-action@@COMMIT@   # v0.0.0-rc.1
        env:
          OCCLUDE_RUN_TOKEN: ${{ secrets.OCCLUDE_RUN_TOKEN }}
        with:
          run-id: ${{ inputs.run-id }}
          cloud-url: <address>
          recorder: ptrace
```
