### check api healthy
```
kubectl get --raw='/readyz?verbose'
```
- should print
  ```
  [+]ping ok
  [+]log ok
  [+]etcd ok
  [+]etcd-readiness ok
  ...
  readyz check passed
  ```
