# salt-formula-designate
Designate provides DNSaaS services for OpenStack
## Sample pillars
```yaml
  designate:
    server:
      database:
        host: ${_param:database_vip_address}
      notification: true
      message_queue:
        members:
          - host: ${_param:messaging_node01_address}
          - host: ${_param:messaging_node02_address}
          - host: ${_param:messaging_node03_address}
      pool:
        pool_id: cae73b6f-95eb-4a7d-a567-099ae6176e08
        nameservers:
          - uuid: 690d7bc8-811b-404c-abcc-9cec54d87092
            host: ${_param:cluster_node01_address}
            port: 53
          - uuid: bc5ddcf0-8d95-4f87-b435-9ff831a4a14c
            host: ${_param:cluster_node02_address}
            port: 53
          - uuid: a43d5375-a5ec-4077-8c87-ec0b08fa3bd1
            host: ${_param:cluster_node03_address}
            port: 53
        targets:
          uuid: f26e0b32-736f-4f0a-831b-039a415c481e
          options: 'port: 53, host: 127.0.0.1'
          masters: 127.0.0.1:5354
          type:  bind9
```
## Usage
Create server
```bash
designate server-create --name ns.example.com.
```
Create domain
```bash
designate domain-create --name example.com. --email mail@example.com
```
Create record
```bash
designate record-create example.com. --name test.example.com. --type A --data 10.2.14.15
```
Test it
```bash
dig @127.0.0.1 test.example.com.
```
