# Blocked-Suspicious-Outbound-Activity-via-Firewall-Real-Reconstructed-Incident-

**Note** : This incident is reconstructed from memory. No evidence was preserved, but indicators are presented at a high level, with assumptions clearly marked.

**Date** : May 2026

**Context** : Personal Windows Machine


## Summary 
This write-up documents a blocked suspicious outbound activity via Firewall (Portmaster Safing) on a possible infected Windows machine. The connections have been blocked, and the machine has successfully been prevented from any possible further infection.

## Root Cause

**Social Engineering** : user has accessed an ad from a legitimate website that redirected them to a fake domain, automatically downloading malware. The deception worked due to:
- Trust in the initial website and its ads
- Quickly closing the fake domain website, user thought nothing had happened
- Not checking for any suspicious downloads or connections

**Technical Level** : the malware executed itself locally, but communication to C2 had been blocked. The local execution worked given that:
- No Ad-Blocker or Anti-Trackers active on machine
- Autoplay/Plugins enabled which allows JavaScript or Flash to to execute automatically


## Observations
- Multiple connections in  'Time_Wait' state
- Repetead attempts to same destination (IP/Port)
- No new processes appeared

## Analysis
- The multiple connections in 'Time_Wait' suggest, but not confirme a potential C2 failed communication.
- The lack of persistence or processes may indicate blocked connections to C2. The malware executed itself locally, but in order to follow orders and harm the machine, it needs confirmation from C2.

## Behaviour Analysis
- After further analysis, multiple tools have detected malware on the machine (Trojan.PyengyLoader), which confirms that the malware executed itself locally and that it was active.
- However, the firewall (Portmaster Safing) has successfully blocked the connections to the C2 since:
      - In order for the communication to happen, a Web Protocol is needed ( a server). If between the infected machine and the attacker's machine a blockage or interruption occurs, the communication no longer persists and is ended.
      - Due to Portmaster Safing's DNS Blocking (uses filter lists to block requests to known tracker or malware domains), the outbound connections had been blocked.
      - Not only that, but Per-App Rules ( individual rules for each program to allow/block outbound traffic) and personalized rules have given essential help in blocking such connections.

## MITRE ATT&CK MAPPING
- Initial Compromise ( T1583.008 - Malvertising) : user accessed the fake domain ad.
- Execution ( T1189 - Drive-By Compromise) : malicious ads are paid for and served through legitimate ad providers
- Potential Command & Control communication (T1071.001 - Application Layer Protocol: Web Protocols, Blocked) : potential communication had been blocked.


## Response Actions
- Verified any suspicious/new processes and their pid or any startup processes
- Blocked all connections to the unknown IP
- Quarantined and deleted the detected malware

## Impact
- No confirmed compromise
- Potential C2 communication blocked with the help of a Firewall
- Possible malware multiplicating stopped

## Recommendations
- DNS filtering/ reputation checks
- Enable Ad-Blocker or Anti-Tracker
- Monitor alerts on high volume connections to an unknown IP
- Monitor for any possible reocurrences
- Autplay/Plugins disabled to block JavaScript or Flash from executing automatically

**Note** : Evidence from this incident was not preserved. This analysis is based on observations and technical understanding of Firewall and Network behaviour.

