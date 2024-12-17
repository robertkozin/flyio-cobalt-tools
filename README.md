# flyio-cobalt-tools
 Hosting the https://cobalt.tools project on https://fly.io

## Secrets
I wanted to use https://github.com/getsops/sops but cobalt's secret value is stored as a [key in a json map](https://github.com/imputnet/cobalt/blob/main/docs/run-an-instance.md#api-key-file-format).

### Encrypt
`age --encrypt --armour -R recipients.txt -o keys.json.age keys.json`

### Decrypt
`age --decrypt -i ~/.age/key.txt -o keys.json keys.json.age`

### Encode and copy to clipboard
`base64 keys.json | pbcopy`

### Encode and set in flyctl
`fly secrets set KEYS=$(base64 keys.json)`
