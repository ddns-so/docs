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

| Parameter           | values  | explain  |
|---------------------|---------|----------|
| \<DOMAIN-NAME\>       | string  | a ens or pns name, e.g. "vitalik.eth", "zzzzzzzzzzzzzzzzzzzzz.dot"  |
| is_show_subdomains  | [yes\|no]               | whether list its children domains or not. default is `no` |


### Example 1: query for `vitalik.eth`:

send request via `curl`:

`$ curl https://api.test-ddns.com/name/vitalik.eth`

response is:

```jsx
{
  // request success
  "result": "ok",

  // all the response data is here
  "data": {

    // the name you are querying
    "name": "vitalik.eth",

    // nameHash
    "nameHash": "0xee6c4522aab0003e8d14cd40a6af439055fd2577951148c14b6cea9a53475835",

    // domain label
    "labelName": "vitalik",

    // labelhash
    "labelhash": "0xaf2caa1c2ca1d027f1ac823b529d0a67cd144264b2789fa2ea4d63a67c7103cc",

    // domain's owner address
    "owner": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",

    // parent labelHash
    "parent": "0x93cdeb708b7545dc668eb9280176169d1c33cfd8ed6f04690a0bcc88a93fc4ae",

    // its sub-domains count
    "subdomainCount": 0,

    "ttl": null,
    "cost": "0",

    // when this domain expires
    "expiryDate": "2032-05-04 05:50:24 +0800",

    // when this domain is registered
    "registrationDate": "2020-02-07 02:23:40 +0800",

    // these records are set via ENS/PNS console by user.
    "records": {

      // content hash for ipfs
      "contenthash": "0xe3010170122022fb6413aa794d5eb7a3906655f50f5ac41cbdd7933bc277f7192c9e2177c792",

      // eth address
      "eth": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",

      // dot address
      "dot": "",

      // btc address
      "btc": "",

      // txt address
      "text": [
        "url",
        "avatar"
      ]
    }
  }
}
```

### Example 2: query for "vitalik.eth" with its children domians

send request via `curl`:

`curl https://api.test-ddns.com/name/vitalik.eth?is_show_subdomains=yes `


```jsx
{
  "result": "ok",
  "data": {
    // other contents
    // its subdomains:
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

## Reverse Parse

this method can reverse parse a ETH-address.

HTTP method: GET

URL pattern: `/reverse/<TYPE>/<ETH-ADDRESS>`

| Parameter           | values     | explain  |
|---------------------|------------|----------|
| \<TYPE\>              | [ens\|pns] | which type of result you want to get. e.g if you want ENS name, here should be `ens` |
| \<ETH-ADDRESS\>       | string     | an ETH address, e.g. `0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c` |


### Example 1

query for ens:

send request with `curl`:

`curl https://api.test-ddns.com/reverse/ens/0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c`

response:

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

### Example2

query for pns:

send request with `cur`:

`curl https://api.test-ddns.com/reverse/pns/0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c`

response:

```jsx
{
  // successfully got response
  "result": "ok",

  // the address which is being queried
  "address": "0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c",

  // reverse parsing result
  "data": "ttt112.dot"
}
`
