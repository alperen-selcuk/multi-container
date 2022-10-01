# multi-container 

## sidecar



```
apiVersion: v1
kind: Pod
metadata:
  name: multi-container
spec:
  containers:
  - image: nginx
    name: main-container
    ports:
      - containerPort: 80
    volumeMounts:
    - name: var-logs
      mountPath: /usr/share/nginx/html
  - image: busybox
    command: ["/bin/sh"]
    args: ["-c", "while true; do echo echo $(date -u) 'Hi I am from Sidecar container' >> /var/log/index.html; sleep 5;done"]
    name: sidecar-container
    volumeMounts:
    - name: var-logs
      mountPath: /var/log
  volumes:
  - name: var-logs
    emptyDir: {}
  ```
