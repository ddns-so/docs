<!-- TOC depthFrom:1 depthTo:6 withLinks:1 orderedList:0 -->
- [Servers](#servers)
- [API methods](#api-methods)
	- [query for ens/pns](#query-for-enspns)
	- [reverse parse](#reverse-parse)

<!-- /TOC -->

# Servers

Production Server： https://api.ddns.so

Test Server： https://api.test-ddns.com

# API Methods

## Query for ENS/PNS

HTTP method: GET

URL pattern: `/name/<DOMAIN-NAME>`

| Parameter           | values  | explain  | is required |
|---------------------|---------|----------|-------------|
| \<DOMAIN-NAME\>       | string  | a ens or pns name, e.g. "vitalik.eth", "zzzzzzzzzzzzzzzzzzzzz.dot"  | required |
| is_show_subdomains  | [yes\|no]               | whether list its children domains or not. default is `no` | optional |


### Example 1: query for `vitalik.eth`:

send request via `curl`:

`$ curl https://api.test-ddns.com/name/vitalik.eth`

response data is:

| Parameter           | explain |
|---------------------|---------|
| name |  the name you are querying e.g. "vitalik.eth", "zzzzzzzzzzzzzzzzzzzzz.dot"
| nameHash |  nameHash |
| labelName |  domain label |
| labelHash | labelhash |
| owner |  domain's owner address |
| parent | parent labelhash |
| subdomainCount | its sub-domains count |
| ttl | ttl |
| cost | cost |
| expiryDate | when this domain expires |
| registrationDate | when this domain is registered |
| records | these records are set via ENS/PNS console by user |
| contenthash | content hash for ipfs |
| eth | eth address |
| dot | dot address |
| btc | btc address |
| btc | btc address |
| text | txt address |
| url |  |
| avatar  | avatar url |


### Example 2: query for "vitalik.eth" with its children domians

send request via `curl`:

`curl https://api.test-ddns.com/name/vitalik.eth?is_show_subdomains=yes `


Other contents
| Its subdomains | explain  |
|---------------------|---------|
| id | nameHash |
| name | domain name |
| subdomains | subdomains |

## Reverse Parse

this method can reverse parse a ETH-address.

HTTP method: GET

URL pattern: `/reverse/<TYPE>/<ETH-ADDRESS>`

| Parameter           | values     | explain  | is required |
|---------------------|------------|----------|-------------|
| \<TYPE\>              | [ens\|pns] | which type of result you want to get. e.g if you want ENS name, here should be `ens` | required |
| \<ETH-ADDRESS\>       | string     | an ETH address, e.g. `0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c` | required |


### Example 1 for ENS

query for ens:

send request with `curl`:

`curl https://api.test-ddns.com/reverse/ens/0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c`

response:

| Parameter | explain  |
|---------------------|---------|
| address | the address which is being queried |
| data | reverse parsing result |


### Example2 for PNS

query for pns:

send request with `curl`:

`curl https://api.test-ddns.com/reverse/pns/0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c`

response:

| Parameter | explain  |
|---------------------|---------|
| address | the address which is being queried |
| data | reverse parsing result |


## response code

Every normal response (`200` http code) gets its `result` field, which looks like:

```
{
  "result": "ok",
  ...
}
```

Here is the response code table:

| result code | explain |
|-------------|---------|
| ok          | everything goes well in server |
| error       | something not good |

