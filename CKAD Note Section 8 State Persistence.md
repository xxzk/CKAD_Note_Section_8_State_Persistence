# CKAD Note Section 8 State Persistence

<br>

## 105. Volumes

<br>

### hostPath

<br>

這個範例 mount worker-node 的 `/data` 進 `pod` 裡面，並且 mapping 到 container 裡面的 `/test-pd`。\
實際上我們並不會這樣做，因為 worker-node 之間的資料並沒辦法同步，一般來說會使用 shared storage 例如: NFS, ClusterFS, Ceph, AWS EBS, AzureDisk ....

<br>

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: test-pd
spec:
  containers:
  - image: k8s.gcr.io/test-webserver
    name: test-container
    volumeMounts:
    - mountPath: /test-pd
      name: test-volume
  volumes:
  - name: test-volume
    hostPath:
      # directory location on host
      path: /data
      # this field is optional
      type: Directory
```