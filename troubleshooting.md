# Troubleshooting Guide

| Issue | Cause | Fix |
|-------|--------|-----|
| EC2 not reachable | Security group or subnet route missing | Check inbound rules, route table |
| NAT not working | NAT not attached to public subnet | Recheck NAT configuration |
| SSH timeout | Key permissions too open | Run `chmod 400 key.pem` |
| Private instance no internet | NAT or route misconfigured | Add route `0.0.0.0/0` → NAT Gateway |
