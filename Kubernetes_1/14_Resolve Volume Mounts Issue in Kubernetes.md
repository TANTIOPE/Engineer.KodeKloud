# Task

We encountered an issue with our Nginx and PHP-FPM setup on the Kubernetes cluster this morning, which halted its functionality. Investigate and rectify the issue:

- **Pod Name**: `nginx-phpfpm`
- **ConfigMap Name**: `nginx-config`

**Objective**:
1. Identify and fix the problem.
2. Copy `/home/thor/index.php` file from the `jump_host` to the `nginx-container` within the Nginx document root.
3. Ensure the website is accessible.

**Note:** The `kubectl` utility on `jump_host` is configured to operate with the Kubernetes cluster.

# Steps and Solution

1. **Check Pod and ConfigMap Status**:

    Examine the pod and its associated ConfigMap to identify any potential issues.

    ```bash
    # Describe the pod to check its status and potential issues
    kubectl describe pod nginx-phpfpm

    # Describe the ConfigMap to ensure it's correctly configured
    kubectl describe configmap nginx-config
    ```

2. **Retrieve and Inspect Pod YAML**:

    Get the YAML definition of the pod to identify the mount path and verify the document root configuration.

    ```bash
    # Retrieve the YAML definition of the pod and save it to /tmp/nginx.yaml
    kubectl get pod nginx-phpfpm -o yaml > /tmp/nginx.yaml

    # Display the contents of the YAML file to inspect the mount path
    cat /tmp/nginx.yaml

    # Search for the mountPath in the YAML file
    cat /tmp/nginx.yaml | grep /usr/share/nginx/html
    ```

```yaml
    apiVersion: v1
kind: Pod
metadata:
  annotations:
    kubectl.kubernetes.io/last-applied-configuration: |
      {"apiVersion":"v1","kind":"Pod","metadata":{"annotations":{},"labels":{"app":"php-app"},"name":"nginx-phpfpm","namespace":"default"},"spec":{"containers":[{"image":"php:7.2-fpm-alpine","name":"php-fpm-container","volumeMounts":[{"mountPath":"/usr/share/nginx/html","name":"shared-files"}]},{"image":"nginx:latest","name":"nginx-container","volumeMounts":[{"mountPath":"/var/www/html","name":"shared-files"},{"mountPath":"/etc/nginx/nginx.conf","name":"nginx-config-volume","subPath":"nginx.conf"}]}],"volumes":[{"emptyDir":{},"name":"shared-files"},{"configMap":{"name":"nginx-config"},"name":"nginx-config-volume"}]}}
  creationTimestamp: "2024-08-23T05:59:33Z"
  labels:
    app: php-app
  name: nginx-phpfpm
  namespace: default
  resourceVersion: "1566"
  uid: a009f3a9-b955-4036-bb07-f977ae2455e7
spec:
  containers:
  - image: php:7.2-fpm-alpine
    imagePullPolicy: IfNotPresent
    name: php-fpm-container
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /usr/share/nginx/html
      name: shared-files
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-jlndl
      readOnly: true
  - image: nginx:latest
    imagePullPolicy: Always
    name: nginx-container
    resources: {}
    terminationMessagePath: /dev/termination-log
    terminationMessagePolicy: File
    volumeMounts:
    - mountPath: /var/www/html
      name: shared-files
    - mountPath: /etc/nginx/nginx.conf
      name: nginx-config-volume
      subPath: nginx.conf
    - mountPath: /var/run/secrets/kubernetes.io/serviceaccount
      name: kube-api-access-jlndl
      readOnly: true
  dnsPolicy: ClusterFirst
  enableServiceLinks: true
  nodeName: kodekloud-control-plane
  preemptionPolicy: PreemptLowerPriority
  priority: 0
  restartPolicy: Always
  schedulerName: default-scheduler
  securityContext: {}
  serviceAccount: default
  serviceAccountName: default
  terminationGracePeriodSeconds: 30
  tolerations:
  - effect: NoExecute
    key: node.kubernetes.io/not-ready
    operator: Exists
    tolerationSeconds: 300
  - effect: NoExecute
    key: node.kubernetes.io/unreachable
    operator: Exists
    tolerationSeconds: 300
  volumes:
  - emptyDir: {}
    name: shared-files
  - configMap:
      defaultMode: 420
      name: nginx-config
    name: nginx-config-volume
  - name: kube-api-access-jlndl
    projected:
      defaultMode: 420
      sources:
      - serviceAccountToken:
          expirationSeconds: 3607
          path: token
      - configMap:
          items:
          - key: ca.crt
            path: ca.crt
          name: kube-root-ca.crt
      - downwardAPI:
          items:
          - fieldRef:
              apiVersion: v1
              fieldPath: metadata.namespace
            path: namespace
status:
  conditions:
  - lastProbeTime: null
    lastTransitionTime: "2024-08-23T05:59:33Z"
    status: "True"
    type: Initialized
  - lastProbeTime: null
    lastTransitionTime: "2024-08-23T05:59:49Z"
    status: "True"
    type: Ready
  - lastProbeTime: null
    lastTransitionTime: "2024-08-23T05:59:49Z"
    status: "True"
    type: ContainersReady
  - lastProbeTime: null
    lastTransitionTime: "2024-08-23T05:59:33Z"
    status: "True"
    type: PodScheduled
  containerStatuses:
  - containerID: containerd://08fa24030fb5bf9258ef1d099247cc9b20fad813429e8430f680a4b68ad26988
    image: docker.io/library/nginx:latest
    imageID: docker.io/library/nginx@sha256:447a8665cc1dab95b1ca778e162215839ccbb9189104c79d7ec3a81e14577add
    lastState: {}
    name: nginx-container
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2024-08-23T05:59:48Z"
  - containerID: containerd://a8bd6637fd5b62270fb70c5742bf357ffc24121d7d4ce7f6cc1c10106b657630
    image: docker.io/library/php:7.2-fpm-alpine
    imageID: docker.io/library/php@sha256:2e2d92415f3fc552e9a62548d1235f852c864fcdc94bcf2905805d92baefc87f
    lastState: {}
    name: php-fpm-container
    ready: true
    restartCount: 0
    started: true
    state:
      running:
        startedAt: "2024-08-23T05:59:38Z"
  hostIP: 172.17.0.2
  phase: Running
  podIP: 10.244.0.5
  podIPs:
  - ip: 10.244.0.5
  qosClass: BestEffort
  startTime: "2024-08-23T05:59:33Z"
  ```

![image](https://github.com/user-attachments/assets/f485122d-1609-46dc-8ea8-157071230f39)

  Based on the provided information, the mount path for the Nginx container should be `/var/www/html`, and for the PHP-FPM container, it is `/usr/share/nginx/html`.

3. **Update the Pod Configuration**:

    Update the YAML file to ensure that the correct mount path is set in the ConfigMap. The Nginx configuration should use `/var/www/html` as the document root.

    ```bash
    # Edit the YAML file to change the mountPath if needed
    vi /tmp/nginx.yaml
    ```

    Update the YAML file if the `mountPath` is incorrect. For Nginx, ensure the `mountPath` is `/var/www/html` as shown in your output:

    ```yaml
    volumeMounts:
    - mountPath: /var/www/html
      name: shared-files
    ```

    Save the changes and replace the existing pod configuration.

    ```bash
    # Replace the pod configuration with the updated YAML file
    kubectl replace -f /tmp/nginx.yaml --force
    ```

4. **Copy the File to the Pod**:

    After fixing the mount path issue, copy the `/home/thor/index.php` file from the `jump_host` to the correct directory within the Nginx container.

    ```bash
    # Copy the index.php file to the Nginx container
    kubectl cp /home/thor/index.php nginx-phpfpm:/var/www/html -c nginx-container
    ```

5. **Validate the Setup**:

    Ensure the pod is running correctly and the Nginx container serves the `index.php` file.

    ```bash
    # Verify the pod status to ensure it is running
    kubectl get pods

    # Verify that the website is accessible by making a request to the pod
    kubectl exec -it nginx-phpfpm -c nginx-container -- curl -I http://localhost:8099
    ```
![image](https://github.com/user-attachments/assets/704c7902-efeb-4d52-9355-275827c4cd04)

![image](https://github.com/user-attachments/assets/fd6d62da-1f8b-4711-a283-34b7ce58922e)

