# MQTT Protocol Analyzer with Spicy

Compile Spicy source code to HILTI file.

```bash
root@zeek-ubuntu:~/spicy-mqtt/analyzer# spicyc -j -o mqtt.hlto mqtt.spicy
```

### Connect

```bash
root@zeek-ubuntu:~/spicy-mqtt# cat Traces/connect.dat | spicy-dump -J analyzer/mqtt.hlto | jq
{
  "connect": {
    "clean_session": true,
    "client_id": "user",
    "flags": [
      0,
      1,
      0,
      0,
      0,
      1,
      1
    ],
    "keep_alive": 60,
    "password": "",
    "password_string": "apple",
    "protocol_name": "MQTT",
    "username": "",
    "username_string": "user",
    "version": 4,
    "will_msg": "",
    "will_qos": 0,
    "will_retain": false,
    "will_topic": ""
  },
  "fixed_header": {
    "dup": false,
    "fixed_header_byte1": [
      "CONNECT",
      0
    ],
    "length": {
      "integer_array": [
        29
      ],
      "value": 29
    },
    "packet_type": "CONNECT",
    "qos": 0,
    "remaining_length": 29,
    "retain": false
  }
}
```

### Connack

```bash
root@zeek-ubuntu:~/spicy-mqtt# cat Traces/connack.dat | spicy-dump -J analyzer/mqtt.hlto | jq
{
  "connack": {
    "acknowledge_flags": [
      0,
      0
    ],
    "return_code": 0,
    "session_present": false
  },
  "fixed_header": {
    "dup": false,
    "fixed_header_byte1": [
      "CONNACK",
      0
    ],
    "length": {
      "integer_array": [
        2
      ],
      "value": 2
    },
    "packet_type": "CONNACK",
    "qos": 0,
    "remaining_length": 2,
    "retain": false
  }
}
```

### Publish

```bash
root@zeek-ubuntu:~/spicy-mqtt# cat Traces/publish.dat | spicy-dump -J analyzer/mqtt.hlto | jq
{
  "fixed_header": {
    "dup": false,
    "fixed_header_byte1": [
      "PUBLISH",
      1
    ],
    "length": {
      "integer_array": [
        44
      ],
      "value": 44
    },
    "packet_type": "PUBLISH",
    "qos": 0,
    "remaining_length": 44,
    "retain": true
  },
  "publish": {
    "dup": false,
    "msg_id": 0,
    "payload": "mosquitto version 1.6.9",
    "payload_len": 23,
    "qos": 0,
    "retain": true,
    "topic": "$SYS/broker/version",
    "topic_string": {
      "data": "$SYS/broker/version",
      "length": 19
    }
  }
}
```

### Subscribe

```bash
root@zeek-ubuntu:~/spicy-mqtt# cat Traces/subscribe.dat | spicy-dump -J analyzer/mqtt.hlto | jq
{
  "fixed_header": {
    "dup": false,
    "fixed_header_byte1": [
      "SUBSCRIBE",
      2
    ],
    "length": {
      "integer_array": [
        11
      ],
      "value": 11
    },
    "packet_type": "SUBSCRIBE",
    "qos": 1,
    "remaining_length": 11,
    "retain": false
  },
  "subscribe": {
    "msg_id": 2,
    "requested_qos": [
      0
    ],
    "topic_qos": [
      {
        "qos": [
          0,
          0
        ],
        "requested_qos": 0,
        "topic": "$SYS/#"
      }
    ],
    "topics": [
      "$SYS/#"
    ]
  }
}
```

### Suback

```bash
root@zeek-ubuntu:~/spicy-mqtt# cat Traces/suback.dat | spicy-dump -J analyzer/mqtt.hlto | jq
{
  "fixed_header": {
    "dup": false,
    "fixed_header_byte1": [
      "SUBACK",
      0
    ],
    "length": {
      "integer_array": [
        3
      ],
      "value": 3
    },
    "packet_type": "SUBACK",
    "qos": 0,
    "remaining_length": 3,
    "retain": false
  },
  "suback": {
    "msg_id": 2,
    "reason_code": [
      {
        "granted_qos": 0,
        "msg_id": 2
      }
    ]
  }
}
```

### Disconnect

```bash
root@zeek-ubuntu:~/spicy-mqtt# cat Traces/disconnect.dat | spicy-dump -J analyzer/mqtt.hlto | jq
{
  "fixed_header": {
    "dup": false,
    "fixed_header_byte1": [
      "DISCONNECT",
      0
    ],
    "length": {
      "integer_array": [
        0
      ],
      "value": 0
    },
    "packet_type": "DISCONNECT",
    "qos": 0,
    "remaining_length": 0,
    "retain": false
  }
}
```
