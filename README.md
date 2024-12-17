# flyio-cobalt-tools
 Hosting the https://cobalt.tools project on https://fly.io

 For secret management I wanted to use [SOPS](https://github.com/getsops/sops) but Cobalt's secret value is stored as a [key in a json map](https://github.com/imputnet/cobalt/blob/main/docs/run-an-instance.md#api-key-file-format) and SOPS only encrypts values.

## Tasks
### Deploy
```shell
fly deploy --ha=false
```

### Decrypt secrets
```shell
age --decrypt -i ~/.age/keys.txt -o keys.json keys.json.age
```

### Encrypt secrets
```shell
age --encrypt --armour -R recipients.txt -o keys.json.age keys.json
```

### Deploy secrets
```shell
fly secrets set KEYS=$(base64 keys.json)
```
