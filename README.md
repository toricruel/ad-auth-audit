# AD Auth Audit (`ad_auth_audit.py`)

**Defensive Active Directory Authentication Configuration Audit Module**

* **Author:** Tarlan Guliev
* **Year:** 2026

## Overview

`ad_auth_audit.py` is a read-only defensive auditing CLI tool designed to identify risky Active Directory authentication configurations and validate SOC/SIEM detection rules.

## Key Features

* **`AS_REP_NO_PREAUTH`**: Identifies enabled user accounts with `DONT_REQUIRE_PREAUTH`.
* **`SPN_SERVICE_ACCOUNT`**: Identifies user accounts with registered `servicePrincipalName` (SPN) attributes and flags `adminCount` or `USE_DES_KEY_ONLY` risks.
* **Controlled SOC Testing (`--noisy`)**: Generates predictable, payload-free TCP connections to ports `88`, `389`, and `636` for Sysmon Event ID 3 and SIEM correlation testing.
* **SIEM/ELK Ready**: Outputs formatted `rich` console tables and structured JSON reports.

## Safety Constraints

* Does **NOT** perform AS-REP Roasting or Kerberoasting.
* Does **NOT** request Kerberos tickets (`AS-REQ` / `TGS-REQ`) or extract hashes.
* Operates strictly via read-only LDAP queries and requires `--i-confirm-authorization`.

## Installation & Usage

```bash
pip install -r requirements.txt
export AD_AUDIT_PASSWORD=Password123
python3 ad_auth_audit.py \
    --dc-ip 10.10.10.5 \
    --domain corp.local \
    --username svc_audit \
    --json audit.json \
    --noisy \
    --i-confirm-authorization
```
