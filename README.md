# CVE-2020-1472
Exploit Code for CVE-2020-1472 aka Zerologon

By default, will zeroing out the password of the domain controller account.
*NOTE:* It will break things in production (eg. DNS, communication with other DC, etc)

Zerologon original researh and writeup: (here)[https://www.secura.com/blog/zero-logon]

# Exploit

It attempts to perform the Netlogon authentication bypass. When a domain controller is patched, the detection 
script will give up after sending 2000 pairs of RPC calls, concludeing that the target is not vulnerable (with a 
false negative chance of 0.04%).

## Installation

Requires Python 3.7 or higher and Pip. Install dependencies as follows:

    pip install -r requirements.txt

It embeds a modified version of Impacket. (now unnecessary as it has been (merged)[https://github.com/SecureAuthCorp/impacket])

## Running the script

The script targets can be used to target a DC or backup DC. It likely also works against a read-only DC, but this has 
not been tested. Given a domain controller named `EXAMPLE-DC` and IP address `1.2.3.4`, run the script as follows:

+    ```./cve-2020-1472-exploit.py EXAMPLE-DC 1.2.3.4```

The DC name should be its NetBIOS computer name. If this name is not correct, the script will likely fail with a 
`STATUS_INVALID_COMPUTER_NAME` error.
