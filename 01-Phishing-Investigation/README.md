# Phishing Kit Investigation

## Objective

Investigate a phishing website and identify attacker infrastructure.

---

## Tools Used

- Wireshark
- CyberChef
- Linux
- SHA256

---

## Investigation

### Step 1

Located an exposed `/data` directory.

### Step 2

Downloaded the phishing kit archive.

### Step 3

Calculated SHA256 hash.

### Step 4

Extracted the ZIP archive.

### Step 5

Identified the attacker's email from `submit.php`.

### Step 6

Recovered the hidden flag.

---

## Indicators of Compromise

| IOC | Value |
|------|-------|
| SHA256 | ... |
| Attacker Email | ... |
| Archive | Update365.zip |

---

## MITRE ATT&CK

| Technique | Description |
|-----------|-------------|
| T1566 | Phishing |

---

## Lessons Learned

- Never expose sensitive directories.
- Disable directory listing.
- Validate uploaded files.
