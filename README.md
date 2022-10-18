<img src="https://camo.githubusercontent.com/9e5a57075a5bb3bab4d34b1c3eed3009973bc15ddb6f168c7fbf475d8f0e967f/68747470733a2f2f64617964617975703636362e6574682e64646e732e736f2f697066732f516d586d64535152506d684d666870487a6831585a356955617236447951723844624a753734384b75756f727475" width="78" height="78" />
<!-- TOC depthFrom:1 depthTo:6 withLinks:1 orderedList:0 -->

- [API Overview](https://github.com/ddns-so/docs#api接口)
	- [API Overview1：Some The details of the eth/. dot domain name](https://github.com/ddns-so/docs#%E6%8E%A5%E5%8F%A31-%E6%9F%90%E4%B8%AAeth--dot-%E5%9F%9F%E5%90%8D%E7%9A%84%E8%AF%A6%E7%BB%86%E4%BF%A1%E6%81%AF)
	- [API Overview2：Reverse resolution (obtain the ens/pns domain name according to the ETH address)](https://github.com/ddns-so/docs#%E6%8E%A5%E5%8F%A32%E5%8F%8D%E5%90%91%E8%A7%A3%E6%9E%90%E6%A0%B9%E6%8D%AE-eth%E5%9C%B0%E5%9D%80-%E8%8E%B7%E5%BE%97-ens--pns-%E5%9F%9F%E5%90%8D)

<!-- /TOC -->

## API Overview

### API Overview1: Some The details of the eth/dot domain name

Initiate request:

GET request, the content of the request is as follows:

Form 1：[https://api.ddns.so/name/zzzzzzzzzzzzzzzzzzzzz.dot](https://api.ddns.so/name/zzzzzzzzzzzzzzzzzzzzz.dot)

Form 2：[https://api.ddns.so/name/zzzzzzzzzzzzzzzzzzzzz.dot?is_show_subdomains=yes](https://api.ddns.so/name/zzzzzzzzzzzzzzzzzzzzz.dot?subdomains=yes)

Form 3：[https://api.ddns.so/name/brantly.eth](https://api.ddns.so/name/brantly.eth?is_show_subdomains=yes)

Form 4：[https://api.ddns.so/name/brantly.eth?is_show_subdomains=yes](https://api.ddns.so/name/brantly.eth?is_show_subdomains=yes)

Example of returned results:

Form 1：[https://api.ddns.so/name/vitalik.eth](https://api.ddns.so/name/vitalik.eth)

Form 1 returns the following contents:

```jsx
{
  "result": "success",       // Flag of successful request
  "data": {                 // The following is the specific returned content
    "name": "vitalik.eth",    // Indicates the query domain name, including. eth/. dot
    "nameHash": "0xee6c4522aab0003e8d14cd40a6af439055fd2577951148c14b6cea9a53475835",           // nameHash
    "labelName": "vitalik",   // labelName，the name of the domain name, excluding. eth/. dot

    // labelhash
    "labelhash": "0xaf2caa1c2ca1d027f1ac823b529d0a67cd144264b2789fa2ea4d63a67c7103cc",
    // The owner of this domain name
    "owner": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
    // Lablehash of parent domain name
    "parent": "0x93cdeb708b7545dc668eb9280176169d1c33cfd8ed6f04690a0bcc88a93fc4ae",
    "subdomainCount": 0,  // Indicates the number of subdomains of the query domain name
    "ttl": null,  // ttl
    "cost": "0",  // cost
    "expiryDate": "2032-05-04 05:50:24 +0800",  // Indicates the expiration time of the query domain name
    "registrationDate": "2020-02-07 02:23:40 +0800",  // Indicates the registration time of the query domain name
    // The following records are all from screenshot 2
    "records": {
      // contenthash
      "contenthash": "0xe3010170122022fb6413aa794d5eb7a3906655f50f5ac41cbdd7933bc277f7192c9e2177c792",
      // Indicates the owner's ETH address
      "eth": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
      "dot": "",    // Indicates Polkadot address
      "btc": "",    // Indicates the btc address
      // These contents of the following text are from the screenshot 1
      "text": [
        "url",      // URL representing Twitter
        "avatar"    // The URL representing the avatar
      ],
      "pubkey": ""  // Represents a public key
    }
  }
}
```
[sreenshot 1](https://github.com/ddns-so/docs/blob/main/%E6%88%AA%E5%9B%BE1.png) [sreenshot 2](https://github.com/ddns-so/docs/blob/main/%E6%88%AA%E5%9B%BE2.png)

Form 2：[https://api.ddns.so/name/brantly.eth?is_show_subdomains=yes](https://api.ddns.so/name/brantly.eth?is_show_subdomains=yes)

(More subdomains are returned)

(On the basis of Form 1, add the parameter is_ show_ Subdomains. If it is equal to yes, the details of the subdomains of the domain name will be displayed. The result is as follows)

```jsx
{
  "result": "success",       // Flag of successful request
  "data": {                 // The following is the specific returned content
    "name": "vitalik.eth",    // Indicates the query domain name, including. eth/. dot
    "nameHash": "0xee6c4522aab0003e8d14cd40a6af439055fd2577951148c14b6cea9a53475835",           // nameHash
    "labelName": "vitalik",   // labelName，the name of the domain name, excluding. eth/. dot

    // labelhash
    "labelhash": "0xaf2caa1c2ca1d027f1ac823b529d0a67cd144264b2789fa2ea4d63a67c7103cc",
    // The owner of this domain name
    "owner": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
    // Lablehash of parent domain name
    "parent": "0x93cdeb708b7545dc668eb9280176169d1c33cfd8ed6f04690a0bcc88a93fc4ae",
    "subdomainCount": 0,  // Indicates the number of subdomains of the query domain name
    "ttl": null,  // ttl
    "cost": "0",  // cost
    "expiryDate": "2032-05-04 05:50:24 +0800",  // Indicates the expiration time of the query domain name
    "registrationDate": "2020-02-07 02:23:40 +0800",  // Indicates the registration time of the query domain name
    // The following records are all from screenshot 2
    "records": {
      // contenthash
      "contenthash": "0xe3010170122022fb6413aa794d5eb7a3906655f50f5ac41cbdd7933bc277f7192c9e2177c792",
      // Indicates the owner's ETH address
      "eth": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
      "dot": "",    // Indicates Polkadot address
      "btc": "",    // Indicates the btc address
      // These contents of the following text are from the screenshot 1
      "text": [
        "url",      // URL representing Twitter
        "avatar"    // The URL representing the avatar
      ],
      "pubkey": ""  // Represents a public key
    },
    // All subdomain names of the queried domain name, including the complete domain name, ID and sub domain name of each sub domain name
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
[screenshot 1](https://github.com/ddns-so/docs/blob/main/%E6%88%AA%E5%9B%BE1.png) [screenshot 2](https://github.com/ddns-so/docs/blob/main/%E6%88%AA%E5%9B%BE2.png)

Form 3：[https://api.ddns.so/name/zzzzzzzzzzzzzzzzzzzzz.dot](https://api.ddns.so/name/zzzzzzzzzzzzzzzzzzzzz.dot)

Form 3 returns the following contents:

```jsx
{
  "result": "success",     // Flag of successful request
  "data": {               // The following is the specific returned content
    "name": "zzzzzzzzzzzzzzzzzzzzz.dot",   // Indicates the query domain name, including .eth/.dot
    "namehash": "",         // nameHash
    "labelName": "zzzzzzzzzzzzzzzzzzzzz",  // labelName
    // labelhash
    "labelhash": "0xc40a066a5a14b7cf1a860b96cab9c3b5b945f77824de421109012bed498c151b",
    // Indicates the address of the owner of the query domain name
    "owner": "0x0b23e3588c906c3f723c58ef4d6baee7840a977c",
    // LabelHash representing the parent domain name of the query domain name
    "parent": "0x3fce7d1364a893e213bc4212792b517ffc88f5b13b86c8ef9c8d390c3a1370ce",
    // Indicates the expiration time of the query domain name
    "expiryDate": "2024-06-25 23:47:06 +0800",
    // Indicates the registration time of the query domain name
    "registrationDate": "2022-06-26 23:47:06 +0800",
    // Indicates the number of subdomains of the query domain name
    "subdomainCount": 12,

    // The following contents are all from screenshot 2
    "records": {
      "dot": "168EsqUaRF6teT9enPx9X6dbHR7JbWN5hDeNAKtHGUPh4RCy", // Indicates polkadot address
      "eth": "0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c",  // Indicates eth address
      "btc": "36b6xyDZzvUEJ7QfzqhPzFMKbwzHLZ5tFc",          // Indicates btc address
      "ipfs": "QmQhCuJqSk9fF58wU58oiaJ1qbZwQ1eQ8mVzNWe7tgLNiD",  // ipfs
      "email": "some@email1.com",  // Indicates email address
      "notice": "00302notice",     // Indicates notice address
      "twitter": "https://twitter.com/zou326865641",   // Indicates twitter address
      "github": "https://github.com/hebochang",        // Indicates github address
      "url": "https://twitter.com/zou32686564",        // Indicates twitter url
      "avatar": "0050103avatar",                       // Indicates avatar address
      "cname": "a.b.c.d.com"                           // Indicates cname address
    }
  }
}
```
[screenshot 1](https://github.com/ddns-so/docs/blob/main/%E6%88%AA%E5%9B%BE1.png) [screenshot 2](https://github.com/ddns-so/docs/blob/main/%E6%88%AA%E5%9B%BE2.png)

Form 4：[https://api.ddns.so/name/zzzzzzzzzzzzzzzzzzzzz.dot?is_show_subdomains=yes](https://api.ddns.so/name/zzzzzzzzzzzzzzzzzzzzz.dot?is_show_subdomains=yes)

(More subdomains are returned)

(On the basis of Form 3, add the parameter is_show_subdomains. If it is equal to yes, the details of the subdomains of the domain name will be displayed to get this result.)

```jsx
{
  "result": "success",     // Flag of successful request
  "data": {               // The following is the specific returned content
    "name": "zzzzzzzzzzzzzzzzzzzzz.dot",   // Indicates the query domain name, including .eth/.dot
    "namehash": "",         // nameHash
    "labelName": "zzzzzzzzzzzzzzzzzzzzz",  // labelName
    // labelhash
    "labelhash": "0xc40a066a5a14b7cf1a860b96cab9c3b5b945f77824de421109012bed498c151b",
    // Indicates the address of the owner of the query domain name
    "owner": "0x0b23e3588c906c3f723c58ef4d6baee7840a977c",
    // LabelHash representing the parent domain name of the query domain name
    "parent": "0x3fce7d1364a893e213bc4212792b517ffc88f5b13b86c8ef9c8d390c3a1370ce",
    // Indicates the expiration time of the query domain name
    "expiryDate": "2024-06-25 23:47:06 +0800",
    // Indicates the registration time of the query domain name
    "registrationDate": "2022-06-26 23:47:06 +0800",
    // Indicates the number of subdomains of the query domain name
    "subdomainCount": 12,

    // The following contents are all from screenshot 2
    "records": {
      "dot": "168EsqUaRF6teT9enPx9X6dbHR7JbWN5hDeNAKtHGUPh4RCy", // Indicates polkadot address
      "eth": "0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c",  // Indicates eth address
      "btc": "36b6xyDZzvUEJ7QfzqhPzFMKbwzHLZ5tFc",          // Indicates btc address
      "ipfs": "QmQhCuJqSk9fF58wU58oiaJ1qbZwQ1eQ8mVzNWe7tgLNiD",  // ipfs
      "email": "some@email1.com",  // Indicates email address
      "notice": "00302notice",     // Indicates notice address
      "twitter": "https://twitter.com/zou326865641",   // Indicates twitter address
      "github": "https://github.com/hebochang",        // Indicates github address
      "url": "https://twitter.com/zou32686564",        // Indicates twitter url
      "avatar": "0050103avatar",                       // Indicates avatar address
      "cname": "a.b.c.d.com"                           // Indicates cname address
    }
    // All subdomains of the queried domain name, including the complete domain name and the owner's address of each subdomain name
    "subdomains": [
      {
        "name": "zfd2.zzzzzzzzzzzzzzzzzzzzz.dot",
        "owner": "0x0b23e3588c906c3f723c58ef4d6baee7840a977c"
      },
      {
        "name": "zfd.zzzzzzzzzzzzzzzzzzzzz.dot",
        "owner": "0x0b23e3588c906c3f723c58ef4d6baee7840a977c"
      }
    ]
  }
}
```
[screenshot 1](https://github.com/ddns-so/docs/blob/main/%E6%88%AA%E5%9B%BE1.png) [screenshot 2](https://github.com/ddns-so/docs/blob/main/%E6%88%AA%E5%9B%BE2.png)

### Interface 2: Reverse parsing (obtaining the ens/pns domain name according to the ETH address)

Form 1：https://api.ddns.do/reverse/address?type=eth

All eth domain names of address will be returned

- [https://api.ddns.so/reverse/0x2db2145ec2d26a1809cb2cf8785c6da94f992d99?type=eth](https://api.ddns.so/reverse/0x2db2145ec2d26a1809cb2cf8785c6da94f992d99?type=eth)

The parameter type is equal to eth, and all ens domain names of address "0x2db2145ec2d26a1809cb2cf8785c6da94f992d99" will be displayed

```jsx
{
  "result": "success",     // Flag of successful request
  // Indicates the address of the query
  "address": "0x2db2145ec2d26a1809cb2cf8785c6da94f992d99",
  // The following is the specific returned content, including all eth domain names owned by the address
  "data": [
    "pomeriumfoundation.eth",
    "precede.eth"
  ]
}
```

Form 2：https://api.ddns.do/reverse/0xabcd?type=dot

All dot domain names of 0xabcd will be returned

- [https://api.ddns.so/reverse/0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c?type=dot](https://api.ddns.so/reverse/0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c?type=dot)

The parameter type is equal to dot, and all dot domain names of address' 0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c 'will be displayed

```jsx
{
  "result": "success",    // Flag of successful request
  // Indicates the address of the query
  "address": "0x0b23E3588c906C3F723C58Ef4d6baEe7840A977c",
  // The following is the specific returned content, including all dot domain names owned by the address
  "data": [
    "zfd2.zzzzzzzzzzzzzzzzzzzzz.dot",
    "zfd.zzzzzzzzzzzzzzzzzzzzz.dot"
  ]
}
```
![screenshot 1](https://github.com/ddns-so/docs/blob/main/%E6%88%AA%E5%9B%BE1.png)
screenshot 1
![screenshot 2](https://github.com/ddns-so/docs/blob/main/%E6%88%AA%E5%9B%BE2.png)
screenshot 2
