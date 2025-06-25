# Résultat à obtenir

## Sensu

### Inspecter le réseau

```bash
docker network inspect sensu
```

```bash
[
    {
        "Name": "sensu",
        "Id": "545ae2592d6a503c73c197ce84797af400e47f1d1e83faf11b399e680ef40274",
        "Created": "2024-09-02T07:30:25.880626604Z",
        "Scope": "local",
        "Driver": "bridge",
        "EnableIPv6": false,
        "IPAM": {
            "Driver": "default",
            "Options": {},
            "Config": [
                {
                    "Subnet": "172.18.0.0/16",
                    "Gateway": "172.18.0.1"
                }
            ]
        },
        "Internal": false,
        "Attachable": false,
        "Ingress": false,
        "ConfigFrom": {
            "Network": ""
        },
        "ConfigOnly": false,
        "Containers": {
            "3569ae10ed5f435e890ddf0d0b314fb0f9a027368c2da899b8c41d126964e3f9": {
                "Name": "lucid_kare",
                "EndpointID": "e2914bc14be8f158b03c44077cf58fe9a1f305d35d4753da48dcfab0da22be09",
                "MacAddress": "02:42:ac:12:00:03",
                "IPv4Address": "172.18.0.3/16",
                "IPv6Address": ""
            },
            "6125af1af7af58a5e9e88ef73775799dd2d93aba07c54fdaa4fc752de642303e": {
                "Name": "sensu-backend",
                "EndpointID": "0e5b9d0ddbc82cd449018adc94454941b693b339b3d8e4ea7b9b4cdd8c0b4177",
                "MacAddress": "02:42:ac:12:00:02",
                "IPv4Address": "172.18.0.2/16",
                "IPv6Address": ""
            },
            "72fbac2cc604683230d9d5bddfe76c5e8373c69a2277fee5a36b1442335ef0e7": {
                "Name": "naughty_noether",
                "EndpointID": "3671992071becd15d3b5370fdd3bad8c3dcbc15e9deca282b1d9e651dad2879a",
                "MacAddress": "02:42:ac:12:00:04",
                "IPv4Address": "172.18.0.4/16",
                "IPv6Address": ""
            }
        },
        "Options": {},
        "Labels": {}
    }
]

```

### Obtenir les noms et adresses ip

```bash
docker network inspect sensu | jq -r ".[0].Containers[] | \"\(.Name) \(.IPv4Address)""
```

```bash
sensu-backend 172.18.0.2/16
sensu-agent 172.18.0.3/16
```
