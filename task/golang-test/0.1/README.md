# Golang tasks

This Task is Golang task to test Go projects.

## Install the tasks

```
kubectl apply -f https://raw.githubusercontent.com/tektoncd/catalog/master/golang/tests.yaml
```


## `golang-test`

### Parameters

* **package**: base package to build in
* **packages**: packages to test (_default:_ ./cmd/...)
* **version**: golang version to use for builds (_default:_ latest)
* **flags**: flags to use for `go test` command (_default:_ -race -cover -v)
* **GOOS**: operating system target (_default:_ linux)
* **GOARCH**: architecture target (_default:_ amd64)
* **GO111MODULE**: value of module support (_default:_ auto)

### Workspaces

* **source**: A `git`-type `PipelineResource` specifying the location of the
  source to build.

## Usage


### `golang-test`

This TaskRun runs the Task to run unit-tests on
[`tektoncd/pipeline`](https://github.com/tektoncd/pipeline).

```yaml
apiVersion: tekton.dev/v1beta1
kind: TaskRun
metadata:
  name: test-my-code
spec:
  taskRef:
    name: golang-test
  workspaces:
  - name: source
    persistentVolumeClaim:
      claimName: my-source
  params:
  - name: package
    value: github.com/tektoncd/pipeline
  - name: packages
    value: ./pkg/...
```

