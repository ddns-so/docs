<!-- TOC depthFrom:1 depthTo:6 withLinks:1 orderedList:0 -->
- [Servers](#servers)
- [API](#api-methods)
	- [Resolving Names for ENS/PNS/BIT/LENS](#resolving-names-for-enspnsbitlens)
  - [Reverse Resolution](#reverse-resolution)
  - [Resolving Domain Records](#resolving-domain-records)
- [response code](#response-code)

<!-- /TOC -->

# Server Endpoint

Production Server： https://api.ddns.so

# API Methods

## Resolving Names for ENS/PNS/BIT/LENS

HTTP method: GET

URL pattern: `/name/<DOMAIN-NAME>`

request:

| Request Parameter   | values  | explain  | is required |
|---------------------|---------|----------|-------------|
| \<DOMAIN-NAME\>       | string  | ens , pns, lens or bit name, e.g. "vitalik.eth", "web3player.dot", "jouni.lens", "phone.bit"  | required |
| subdomains  | [yes\|no]               | whether list its children domains or not. default is `no`.(Lens domain name does not support subdomain name) | optional |
| page | [1\|\2\|3\|..\|n]               | When querying the sub domain name, you can page up to 20 entries per page | optional |

response:

| field             |             explain |
|---------------------------------|------------------------------|
| name             | the name you are querying e.g. "vitalik.eth", "web3player.dot" |
| nameHash         | EIP137 namehash for the domain name |
| labelName        | domain label |
| labelHash        | labelhash |
| owner            | domain owner's address |
| parent           | parent namehash |
| subdomainCount   | subdomains count |
| ttl              | ttl |
| cost             | cost |
| expiryDate       | when this domain expires |
| registrationDate | when this domain is registered |
| records          | domain records |
| contenthash      | IPFS content hash |
| eth              | eth address |
| dot              | dot address |
| btc              | btc address |
| btc              | btc address |
| text             | txt address |
| avatar           | avatar url |


### Example: query for `vitalik.eth`:

send request via `curl`:

`$ curl https://api.ddns.so/name/vitalik.eth`

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

### Query "vitalik.eth" with subdomians and page

send request via `curl`:

`curl https://api.ddns.so/name/vitalik.eth?subdomains=yes&page=1`

response data is:

```jsx
{
  "result": "ok",
  "data": {
    // other contents...
    "page": 1,
    "per": 20,
    "subdomains": [
      {
        "id": "0x1bd80197873de285b67cc9dcf3b2bf196ec112b701f34e89dfc4bfc9fb17b0b2",
        "name": "[4da432f1ecd4c0ac028ebde3a3f78510a21d54087b161590a63080d33b702b8d].[68562fc74af4dcfac633a803c2f57c2b826827b47f797b6ab4e468dc8607b5d0].[4f5b812789fc606be1b3b16908db13fc7a9adf7ca72641f84d75b47069d3d7f0]",
        "subdomains": []
      }
    ]
  }
}
```

### Query "0x.bit" with subdomians and page

send request via `curl`:

`curl https://api.ddns.so/name/0x.bit?subdomains=yes&page=3`

response data is:

```jsx
{
  "result": "ok",
  "data": {
    // other contents...
    "page": 3,
    "per": 20,
    "subdomains": [
      {
        "name": "-077.0x.bit",
        "owner": "0x44ce40a40b38f00841dfb00d9cab3f4149c5250a"
      },
      {
        "name": "-080.0x.bit",
        "owner": "0x625dd3ae692d01d7674232720487729619991999"
      }
    ]
  }
}
```

## Reverse Resolution

This method can return reverse resolution records of an ETH address.

HTTP method: GET

URL pattern: `/reverse/<TYPE>/<ETH-ADDRESS>`

| Request parameter           | values     | explain  | is required |
|---------------------|------------|----------|-------------|
| \<TYPE\>              | [ens\|pns\|bit] | which type of result you want to get. e.g if you want to resolve an ENS name, here should be `ens`, `pns` for PNS domain namesor `bit` for BIT domain names | required |
| \<ETH-ADDRESS\>       | string     | an ETH address, e.g. `0xd8da6bf26964af9d7eed9e03e53415d37aa96045` | required |


response:

| field | explain |
|---------------------|---------|
| address | the address which is being queried |
| data    | reverse resolution result             |


### Example for ENS

query for ens:

send request with `curl`:

`curl https://api.ddns.so/reverse/ens/0xd8da6bf26964af9d7eed9e03e53415d37aa96045`

response data is:

```jsx
{
  // get response successfully
  "result": "ok",

  // the address which is being queried
  "address": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",

  // reverse resolution result
  "data": "daydayup666.eth"
}
```

### Example for PNS

query for pns:

send request with `curl`:

`curl https://api.ddns.so/reverse/pns/0xd8da6bf26964af9d7eed9e03e53415d37aa96045`

response data is:

```jsx
{
  // get response successfully
  "result": "ok",

  // the address which is being queried
  "address": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
  // reverse resolution result
  "data": "web3player.dot"
}
```

### Example for BIT

query for bit:

send request with `curl`:

`curl https://api.ddns.so/reverse/bit/0x9176acd39a3a9ae99dcb3922757f8af4f94cdf3c`

response data is:

```jsx
{
  // get response successfully
  "result": "ok",

  // the address which is being queried
  "address": "0x9176acd39a3a9ae99dcb3922757f8af4f94cdf3c",
  // reverse resolution result
  "data": "justing.bit"
}
```

## Resolving Domain Records

Query a domain's A, CNAME, TXT or IPFS record.

HTTP method: GET

URL pattern: `/domain/<DOMAIN-NAME>?type=<TYPE>`

| Request parameter   | values     | explain  | is required |
|---------------------|------------|----------|-------------|
| \<DOMAIN-NAME\>     | string     | the domain which record you want to query, e.g. pns.link  | required |
| \<TYPE\>            | [a\|cname\|txt\|ipfs]     | the record type  | optional, default is `a`|

response:

| field | explain |
|---------------------|---------|
| domain_name | the domain you are querying |
| value |  result |
| type | record type |


### Example

send request with `curl`:

`curl https://api.ddns.so/domain/pns.link`

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
| error       | something goes wrong |

