# build-harness-extensions

A collection of build-harness extensions

## Targets

```
  git/submodules-update               Update submodules
  jsonnet/diff                        Diff Jsonnet fils against expected golden 
  jsonnet/diff-help                   Help regarding Jsonnet diff
  jsonnet/gen-golden                  Generate expected golden files from Jsonnet
  jsonnet/test                        Run Jsonnet tests
  kind/create                         Start KinD local cluster
  kind/delete                         Delete KinD local cluster
  kind/up                             Install jsonnetfile.json with jsonnet-bundler
  opa/clone-policy                    Git clone policies (requires OPA_POLICIES_REPO argument)
  opa/conftest                        Validate manifests
  tanka/fmt                           Format Jsonnet files with tanka
  tanka/generate                      Generate manifests using tanka
  tanka/to-kustomize                  Generate kustomization for tanka-generated manifests
  ```