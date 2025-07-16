---
name: Bug Report
about: Create a report to help us improve
title: '[BUG] '
labels: bug
assignees: ''

---

**Describe the bug**
A clear and concise description of what the bug is.

**To Reproduce**
Steps to reproduce the behavior:
1. Go to '...'
2. Click on '....'
3. Scroll down to '....'
4. See error

**Expected behavior**
A clear and concise description of what you expected to happen.

**Action Configuration**
```yaml
- name: Connect to VPN
  uses: jworford/github-openvpn-windows-action@v1
  with:
    config: ${{ secrets.OPENVPN_CONFIG }}
    username: ${{ secrets.OPENVPN_USERNAME }}
    password: ${{ secrets.OPENVPN_PASSWORD }}
    # ... other inputs
```

**Environment:**
 - OS: [e.g. Windows Server 2019, Windows Server 2022]
 - Runner: [e.g. windows-latest, windows-2019]
 - OpenVPN version: [if known]

**Logs**
If applicable, add action logs to help explain your problem. Please remove any sensitive information.

**Additional context**
Add any other context about the problem here.
