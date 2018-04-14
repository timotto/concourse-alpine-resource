# Alpine Package Resource for Concourse

Check and fetch packages of Alpine repositories from [Concourse](https://concourse.ci/).

## Installing

Add the resource type to your pipeline:

```yaml
resource_types:
- name: alpine
  type: docker-image
  source:
    repository: timotto/concourse-alpine-resource
```

## Source Configuration

* `key_url`: *Required.* URL to the PGP key used to sign the repository.
* `repository`: *Required.* Alpine repository URL.
* `package`: *Required.* Package name.

## Behavior

### `check`: Check for new releases

The latest version of the package available using the source.list line are returned.

### `in`: Not supported.

### `out`: Not supported.

## Example

### Trigger on new version

Define the resource:

```yaml
resources:
- name: freeradius
  type: alpine
  check_every: 24h
  source:
    branch: edge
    repository: main
    arch: s390x
    package: freeradius
```

Add to job:

```yaml
jobs:
  # ...
  plan:
  - get: freeradius
    trigger: true
```
