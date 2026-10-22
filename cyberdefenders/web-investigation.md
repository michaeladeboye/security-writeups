## Summary
An attacker at `111.224.250.131` exploited a SQL injection flaw in search.php, pulled database info including the `customers` table, found the hidden `/admin/` page, logged in as admin, and uploaded a reverse shell (`NVri2vhp.php`). The shell failed to run, but customer data was already exposed.

## Evidence and tools
PCAP, Wireshark, CyberChef, iplocation.net

## Findings

### 1. Attacker identification
`111.224.250.131` had far more traffic with the server than any other host (Statistics > Conversations). It geolocates to Shijiazhuang, China.

### 2. SQL injection (T1190)
The attacker sent dozens of requests to search.php with SQL in the search parameter. I filtered with `ip.src == 111.224.250.131 && http.request` and decoded the URIs in CyberChef. The first injection attempt was: `/search.php?search=book and 1=1; -- -`

### 3. Database enumeration and data theft
The attacker used search.php to list the server's databases through `INFORMATION_SCHEMA.SCHEMATA`, then went after the `customers` table. I filtered with `http.request.uri contains "INFORMATION_SCHEMA"` and decoded the URI in CyberChef: `/search.php?search=book' UNION ALL SELECT NULL,CONCAT(0x7178766271,JSON_ARRAYAGG(CONCAT_WS(0x7a76676a636b,schema_name)),0x7176706a71) FROM INFORMATION_SCHEMA.SCHEMATA-- -`

### 4. Admin directory discovery (T1595.003)
A burst of requests from the attacker IP returned mostly 404s. `/admin/` was the hit.

### 5. Admin login (T1078)
4 login attempts to `/admin/login.php`. Frame 88699 used `admin` / `admin123!` in cleartext, and the next request went to the admin dashboard, so it worked.

### 6. Malicious file upload (T1105)
The attacker uploaded `NVri2vhp.php` through the admin upload form (frame 88757). It was a PHP reverse shell set to connect back to `111.224.250.131` on port 443. The attacker requested the file to trigger it, but the server returned a 500 error and no callback connection shows up, so the shell failed.

## IOCs
| Type | Value |
|---|---|
| Attacker IP | 111.224.250.131 |
| Vulnerable script | search.php |
| Uploaded file | NVri2vhp.php |
| Discovered directory | /admin/ |
| Compromised account | admin |

## How I'd detect it
- A Wazuh rule keyed on SQLi patterns in web logs like `UNION SELECT` and `INFORMATION_SCHEMA`.
- An alert on a high number of 404s from a single IP (directory brute force).
- File integrity monitoring on the web root, so a new .php file triggers an alert.

## How I'd prevent it
Parameterized queries, HTTPS, stronger admin credentials plus MFA, restrict upload file types.
