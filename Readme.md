## values.yaml
### General
```yaml
forward: 1
environment: machines
namespace:
  create: true
  env: false

domain: "example.com"
```
### Volumes

```yaml
volumes:
- name: htb-st
  claim: htb-cl
  path: /home/kali/storage
  target: kali
```
### Container

```yaml
containers:
  - name: kali
    image:
      name: oonray/kali
      version: latest
    priveleged: true
    pull: Always
    user: 1000
    ports:
      - name: ssh
        port: 22
        entrypoints:
          - ssh
        tcp: true
      - name: http
        port: 8000
        entrypoints:
          - web
          - websecure
        tcp: false
      - name: proxy
        port: 8080
        entrypoints:
          - web
          - websecure
        tcp: false
        protocol: http
      - name: https
        port: 8443
        entrypoints:
          - websecure
        tcp: false
    volumes:
      - path: /home/kali/storage
        name: htb-st


vpnFile: --set-file vpnFile=vpn.ovpn
config:
  dante:
    logoutput: stdout
    user:
      priveleged: root
      unpriveleged: nobody
    network:
      socks:
        method: none
        from: 0.0.0.0/0
        to: 0.0.0.0/0
      client:
        method: none
        from: 0.0.0.0/0
        to: 0.0.0.0/0
      internal:
        isNet: true
        interface:
        address: 0.0.0.0
        port: 1080
      external:
        isNet: false
        interface: eth0
        address:
```
