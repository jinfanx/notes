## servicecenter高可用
```yaml
APPLICATION_ID: bmi
service_description:
  name: calculator
  version: 0.0.1
servicecomb:
  service:
    registry:
      address: 
        - http://127.0.0.1:30100
        - http://127.0.0.1:30101
        - http://127.0.0.1:30102
  rest:
    address: 0.0.0.0:7777
```