<!-- TOC depthFrom:1 depthTo:6 withLinks:1 orderedList:0 -->
- [Servers](#servers)
- [API methods](#api-methods)
	- [query for ens/pns](#query-for-enspns)
	- [reverse parse](#reverse-parse)
  - [query for domain's A, CNAME, TXT, IPFS records](#query-for-domain-acnametxtipfs-recordsquery-for-records)
- [response code](#response-code)

<!-- /TOC -->

# Servers

Production Server： https://api.ddns.so

Test Server： https://api.test-ddns.com

# API Methods

## Query for ENS/PNS

HTTP method: GET

URL pattern: `/name/<DOMAIN-NAME>`

request:

| Request Parameter   | values  | explain  | is required |
|---------------------|---------|----------|-------------|
| \<DOMAIN-NAME\>       | string  | ens or pns name, e.g. "vitalik.eth", "zzzzzzzzzzzzzzzzzzzzz.dot"  | required |
| is_show_subdomains  | [yes\|no]               | whether list its children domains or not. default is `no` | optional |

response:

| Response JSON key            |             explain |
|---------------------------------|------------------------------|
| name             |  the name you are querying e.g. "vitalik.eth", "zzzzzzzzzzzzzzzzzzzzz.dot"  |
| nameHash         |      nameHash                                                               |
| labelName        |      domain label                                                           |
| labelHash        |     labelhash                                                               |
| owner            |      domain's owner address                                                 |
| parent           |     parent labelhash                                                        |
| subdomainCount   |     its sub-domains count                                                   |
| ttl              |     ttl                                                                     |
| cost             |     cost                                                                    |
| expiryDate       |     when this domain expires                                                |
| registrationDate |     when this domain is registered                                          |
| records          |     these records are set via ENS/PNS console by user                       |
| contenthash      |     content hash for ipfs                                                   |
| eth              |     eth address                                                             |
| dot              |     dot address                                                             |
| btc              |     btc address                                                             |
| btc              |     btc address                                                             |
| text             |     txt address                                                             |
| avatar           |     avatar url                                                              |


### Example 1: query for `vitalik.eth`:

send request via `curl`:

`$ curl https://api.test-ddns.com/name/vitalik.eth`

response data is:

```
{
  "result": "ok",
  "data": {
    "name": "vitalik.eth",
    "nameHash": "0xee6c4522aab0003e8d14cd40a6af439055fd2577951148c14b6cea9a53475835",
    "labelName": "vitalik",
    "labelHash": "0xaf2caa1c2ca1d027f1ac823b529d0a67cd144264b2789fa2ea4d63a67c7103cc",
    "owner": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
    "parent": "0x93cdeb708b7545dc668eb9280176169d1c33cfd8ed6f04690a0bcc88a93fc4ae",
    "subdomainCount": 0,
    "ttl": null,
    "cost": "3175364107234786",
    "expiryDate": "2034-05-04T09:28:48.000+00:00",
    "registrationDate": "2020-02-06T18:23:40.000+00:00",
    "records": {
      "contentHash": "0xe3010170122028dab11ef0c420d1e616f9ecdc59ad00a07049b636a6d94437b9cedce2fad7f2",
      "eth": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
      "dot": null,
      "btc": null,
      "text": null,
      "pubkey": null
    }
  }
}
```

### Example 2: query for "vitalik.eth" with its children domians

send request via `curl`:

`curl https://api.test-ddns.com/name/vitalik.eth?is_show_subdomains=yes `

response data is:

```jsx
{
  "result": "ok",
  "data": {
    // other contents
    // its subdomains:
    "subdomains": [
      {
        "id": "0x1bd80197873de285b67cc9dcf3b2bf196ec112b701f34e89dfc4bfc9fb17b0b2",
        "name": "[4da432f1ecd4c0ac028ebde3a3f78510a21d54087b161590a63080d33b702b8d].[68562fc74af4dcfac633a803c2f57c2b826827b47f797b6ab4e468dc8607b5d0].[4f5b812789fc606be1b3
b16908db13fc7a9adf7ca72641f84d75b47069d3d7f0]",
        "subdomains": []
      }
    ]
  }
}
```

## Reverse Parse

this method can reverse parse an ETH-address.

HTTP method: GET

URL pattern: `/reverse/<TYPE>/<ETH-ADDRESS>`

| Request parameter           | values     | explain  | is required |
|---------------------|------------|----------|-------------|
| \<TYPE\>              | [ens\|pns] | which type of result you want to get. e.g if you want ENS name, here should be `ens` | required |
| \<ETH-ADDRESS\>       | string     | an ETH address, e.g. `0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c` | required |


response:

| Response JSON key| explain |
|---------------------|---------|
| address | the address which is being queried |
| data    | reverse parsing result             |


### Example 1 for ENS

query for ens:

send request with `curl`:

`curl https://api.test-ddns.com/reverse/ens/0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c`

response data is:

```jsx
{
  // successfully got response
  "result": "ok",

  // the address which is being queried
  "address": "0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c",

  // reverse parsing result
  "data": "daydayup666.eth"
}
```

### Example2 for PNS

query for pns:

send request with `curl`:

`curl https://api.test-ddns.com/reverse/pns/0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c`

response data is:

```jsx
{
  // successfully got response
  "result": "ok",

  // the address which is being queried
  "address": "0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c",
  // reverse parsing result
  "data": "ttt112.dot"
}
```

## Query for domain A|CNAME|TXT|IPFS records](#query-for-records)

query for a domain's record

HTTP method: GET

URL pattern: `/domain/<DOMAIN-NAME>?type=<TYPE>`

| Request parameter   | values     | explain  | is required |
|---------------------|------------|----------|-------------|
| \<DOMAIN-NAME\>     | string     | the domain which record you want to query, e.g. pns.link  | required |
| \<TYPE\>            | string     | the record type, one of: [a|cname|txt|ipfs]  | optional, default is `a`|

response:

| Response JSON key| explain |
|---------------------|---------|
| domain_name | the domain you are querying |
| value |  result |
| type | record type |


### Example

send request with `curl`:

`curl https://api.test-ddns.com/domain/pns.link`

response data is:

```jsx
{
  "result": "ok",
  "data": {
    "domain_name": "pns.link",
    "value": "76.76.21.61",
    "type": "a"
  }
}
```

# response code

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

