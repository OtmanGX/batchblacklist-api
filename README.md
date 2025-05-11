# Batch BlackList API

[![RapidAPI Badge](https://img.shields.io/badge/Available%20on-RapidAPI-black?style=for-the-badge&logo=rapidapi)](https://rapidapi.com/osint-org-osint-org-default/api/batchblacklist)

## Table of Contents
- [Overview](#overview)
- [Supported Blacklists](#supported-blacklists)
- [API Endpoints](#check-endpoint)
- [Use Cases](#use-cases)
- [Pricing](#pricing)
- [Support](#support)

## Overview

**Batch BlackList** is an efficient API for evaluating the reputation of IP addresses and domain names, specifically for mail server and DNSBL (DNS-based Blackhole List) monitoring. It checks addresses against multiple widely-used spam and blacklist services to help identify potential issues with email deliverability or domain/IP reputation.

## Supported Blacklists

This API currently supports a wide range of blacklist zones, including but not limited to:

- SpamCop
- SpamHaus Zen
- BARRACUDA
- Abuse.ro
- 0spam DNSBL

## Check Endpoint

### **Endpoint**
```

POST /check

````

### **Description**

The `/check` endpoint verifies whether the provided IP addresses or domain names are listed in DNS or domain blacklists. The response includes additional metadata such as PTR and A records, and optionally, reputation scores.

---

### **Request Body**

The request body must be a JSON object with the following parameters:

| Field         | Type              | Required | Description |
|---------------|-------------------|----------|-------------|
| `addresses`   | array of strings  | Yes      | A list of IP addresses or domain names to check (max 100). |
| `zones`       | array of strings  | No       | Specific DNS blacklist zones to check. Uses defaults if omitted. |
| `domainZones` | array of strings  | No       | Specific domain blacklist zones to check. Uses defaults if omitted. |

#### **Example**
```json
{
  "addresses": ["1.1.1.1", "example.com"]
}
````

---

### **Response**

The response will be an array of results corresponding to each address in the request.

Each object includes:

| Field      | Type             | Description                             |
| ---------- | ---------------- | --------------------------------------- |
| `address`  | string           | The original address from the input.    |
| `isIP`     | boolean          | Indicates whether the address is an IP. |
| `bl`       | object           | DNSBL results (zone name → boolean).    |
| `ptr`      | string or null   | PTR record (if available).              |
| `a_record` | string or null   | A record (if available).                |
| `score`    | number or string | Score if applicable, or `"NA"`.         |

#### **Example**

```json
[
  {
    "address": "1.1.1.1",
    "isIP": true,
    "bl": {
      "SpamCop": false,
      "SpamHausZen": false,
      "BARRACUDA": false,
      "Abuse.ro": false,
      "0Spam": false
    },
    "ptr": "one.one.one.one",
    "a_record": "1.1.1.1",
    "score": "NA"
  },
  {
    "address": "example.com",
    "isIP": false,
    "bl": {
      "SURBL": false,
      "SPAMHAUSE": false,
      "0Spam": false
    },
    "ptr": "example.com",
    "a_record": "23.192.228.80",
    "score": "NA"
  }
]
```

---

## Use Cases

* Email service providers verifying sending IP/domain reputation.
* Cybersecurity analysts monitoring blacklists.
* IT admins maintaining domain/IP hygiene for mail servers.

---

 
## Pricing
Flexible plans available through [RapidAPI](https://rapidapi.com/osint-org-osint-org-default/api/batchblacklist/pricing).   
Free tier available for testing and low-volume usage.

## Support

For technical issues or enterprise inquiries:  
📧 <info@batchblacklist.com>

## Get Started

👉 Access the API directly on [RapidAPI](https://rapidapi.com/osint-org-osint-org-default/api/batchblacklist) to begin integrating blacklist checks into your application or infrastructure.   
🔗 Visit our website on [BatchBlackList](https://batchblacklist.com).
