# Golang tasks

This Task is Golang task to validate Go projects.

## Install the tasks

```
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/master/golang/lint.yaml
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/master/golang/build.yaml
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/master/golang/tests.yaml
```

## `golangci-lint`

### Parameters

* **package**: base package under validation
* **flags**: flags to use for `golangci-lint` command (_default:_--verbose)
* **version**: golangci-lint version to use (_default:_ v1.16)
* **GOOS**: operating system target (_default:_ linux)
* **GOARCH**: architecture target (_default:_ amd64)
* **GO111MODULE**: value of module support (_default:_ auto)

### Workspaces

* **source**: A `git`-type `PipelineResource` specifying the location of the
  source to build.

## Usage

### `golangci-lint`

This TaskRun runs the Task to validate
[`tektoncd/pipeline`](https://github.com/tektoncd/pipeline) `pkg` package with
`golangci-lint`.

```yaml
apiVersion: tekton.dev/v1beta1
kind: TaskRun
metadata:
  name: lint-my-code
spec:
  taskRef:
    name: golangci-lint
  workspaces:
  - name: source
    persistentVolumeClaim:
      claimName: my-source
  params:
  - name: package
    value: github.com/tektoncd/pipeline
  - name: flags
    value: --verbose
```

