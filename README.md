<img src="https://camo.githubusercontent.com/9e5a57075a5bb3bab4d34b1c3eed3009973bc15ddb6f168c7fbf475d8f0e967f/68747470733a2f2f64617964617975703636362e6574682e64646e732e736f2f697066732f516d586d64535152506d684d666870487a6831585a356955617236447951723844624a753734384b75756f727475" width="78" height="78" />
<!-- TOC depthFrom:1 depthTo:6 withLinks:1 orderedList:0 -->

[中文版接口说明(Interface description in Chinese)](https://github.com/ddns-so/docs/blob/main/README.zn.CH.md)

- [API](https://github.com/ddns-so/docs#api)
	- [API Overview1：Some The details of the eth/. dot domain name](https://github.com/ddns-so/docs#api-1-some-the-details-of-the-ethdot-domain-name)

<!-- /TOC -->

# API

## API 1: Some The details of the eth/dot domain name

Initiate request:

GET request, the content of the request is as follows:

Form 1：/name/vitalik.eth

Form 2：/name/vitalik.eth?is_show_subdomains=yes

Form 3：/name/zzzzzzzzzzzzzzzzzzzzz.dot

Form 4：/name/zzzzzzzzzzzzzzzzzzzzz.dot?is_show_subdomains=yes


Example of returned results:

### Form 1：/name/vitalik.eth

Form 1 returns the following contents:

```jsx
{
  "result": "success",       // Flag of successful request
  "data": {                 // The following is the specific returned content
    "name": "vitalik.eth",    // Indicates the query domain name, including .eth
    "nameHash": "0xee6c4522aab0003e8d14cd40a6af439055fd2577951148c14b6cea9a53475835",           // nameHash
    "labelName": "vitalik",   // labelName，the name of the domain name, excluding .eth

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
    "records": {
      // contenthash
      "contenthash": "0xe3010170122022fb6413aa794d5eb7a3906655f50f5ac41cbdd7933bc277f7192c9e2177c792",
      // Indicates the owner's ETH address
      "eth": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
      "dot": "",    // Indicates Polkadot address
      "btc": "",    // Indicates the btc address
      "text": [
        "url",      // URL representing Twitter
        "avatar"    // The URL representing the avatar
      ],
      "pubkey": ""  // Represents a public key
    }
  }
}
```

### Form 2：/name/vitalik.eth?is_show_subdomains=yes

(On the basis of Form 1, add the parameter is_ show_ Subdomains. If it is equal to yes, the details of the subdomains of the domain name will be displayed. The result is as follows)

```jsx
{
  "result": "success",       // Flag of successful request
  "data": {                 // The following is the specific returned content
    "name": "vitalik.eth",    // Indicates the query domain name, including .eth
    "nameHash": "0xee6c4522aab0003e8d14cd40a6af439055fd2577951148c14b6cea9a53475835",           // nameHash
    "labelName": "vitalik",   // labelName，the name of the domain name, excluding .eth

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
    "records": {
      // contenthash
      "contenthash": "0xe3010170122022fb6413aa794d5eb7a3906655f50f5ac41cbdd7933bc277f7192c9e2177c792",
      // Indicates the owner's ETH address
      "eth": "0xd8da6bf26964af9d7eed9e03e53415d37aa96045",
      "dot": "",    // Indicates Polkadot address
      "btc": "",    // Indicates the btc address
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

### Form 3：/name/zzzzzzzzzzzzzzzzzzzzz.dot

Form 3 returns the following contents:

```jsx
{
  "result": "success",     // Flag of successful request
  "data": {               // The following is the specific returned content
    "name": "zzzzzzzzzzzzzzzzzzzzz.dot",   // Indicates the query domain name, including .dot
    "namehash": "0xe07a052cca727930eaed3b1f7551eaf3a9f2aa71122ad910db6776dd1aeb4681",         // nameHash
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

    // The following contents are all from image-dot.png
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
As shown in the figure 'image-dot.png', the setting interface of the DOT background
<p align="center"><img src="image-dot.png" /></p>
<p align="center">image-dot.png: the setting interface of the DOT background</p>

### Form 4：/name/zzzzzzzzzzzzzzzzzzzzz.dot?is_show_subdomains=yes

(On the basis of Form 3, add the parameter is_show_subdomains. If it is equal to yes, the details of the subdomains of the domain name will be displayed to get this result.)

```jsx
{
  "result": "success",     // Flag of successful request
  "data": {               // The following is the specific returned content
    "name": "zzzzzzzzzzzzzzzzzzzzz.dot",   // Indicates the query domain name, including .dot
    "namehash": "0xe07a052cca727930eaed3b1f7551eaf3a9f2aa71122ad910db6776dd1aeb4681",         // nameHash
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

    // The following contents are all from image-dot.png
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

As shown in the figure 'image dot. png', the setting interface of the DOT background
<p align="center"><img src="image-dot.png" /></p>
<p align="center">image-dot.png: the setting interface of the DOT background</p>
