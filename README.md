# windows-troubleshooting-guide

A collection of common Windows troubleshooting steps, fixes, and IT support documentation.

## Table of Contents
- [Topics Covered](#topics-covered)
- [Common Command Prompt Commands](#common-command-prompt-commands)
  - [Check IP Configuration](#check-ip-configuration)
  - [Ping Test](#ping-test)
  - [System File Checker](#system-file-checker)
- [Performance Issues](#performance-issues)
  - [High CPU Usage: WMI Provider Host (WmiPrvSE.exe)](#high-cpu-usage-wmi-provider-host-wmiprvseexe)
  - [Websites Won't Load but Ping Works (DNS Resolution Failure)](#websites-wont-load-but-ping-works-dns-resolution-failure)
- [Networking Issues](#networking-issues)
  -  [Wi-Fi Keeps Dropping or Running Slow](#wi-fi-keeps-dropping-or-running-slow)

## Topics Covered
- Slow PC performance
- WiFi connectivity issues
- Printer troubleshooting
- Windows update problems
- Basic command prompt tools
- Startup issues
- Blue screen troubleshooting

---

## Common Command Prompt Commands

### Check IP Configuration
```bash
ipconfig
```

### Ping Test
```bash
ping google.com
```

### System File Checker
```bash
sfc /scannow
```

## Performance Issues

### High CPU Usage: WMI Provider Host (WmiPrvSE.exe)

**Symptom:** CPU spikes to 50–100%, WmiPrvSE.exe is the culprit in Task Manager.

**Steps to diagnose:**
1. Open Event Viewer → Applications and Services Logs → Microsoft → Windows → WMI-Activity → Operational
2. Look for Error events — note the `ClientProcessId` in the details pane
3. Cross-reference the PID in Task Manager (enable PID column in Details tab) to find which app is triggering WMI queries

**Common fixes:**
- Restart the WMI service: `net stop winmgmt && net start winmgmt`
- If a specific app is causing it, update or reinstall that app
- Run WMI repair: `winmgmt /resetrepository` (requires admin; reboot after)
- For persistent issues: use WMI Diagnosis Utility (Microsoft) to rebuild the repository

### Websites Won't Load but Ping Works (DNS Resolution Failure)

**Symptoms:** Browser shows "This site can't be reached" or "DNS_PROBE_FINISHED_NXDOMAIN," but `ping 8.8.8.8` succeeds — meaning the connection itself is fine, only name resolution is broken.

**Steps to resolve:**
1. Flush the local DNS cache:
```bash
ipconfig /flushdns
```
2. Confirm DNS servers are set correctly:
```bash
ipconfig /all
```
Look for the "DNS Servers" line under your active adapter.
3. Try a public DNS server (Google 8.8.8.8 / 8.8.4.4 or Cloudflare 1.1.1.1) via Network Adapter settings → IPv4 Properties.
4. Test resolution directly with `nslookup github.com` — if this fails but `ping 8.8.8.8` works, it confirms a pure DNS issue (not a general network outage).
5. Restart the DNS Client service:
```bash
net stop dnscache
net start dnscache
```

**Root cause:** Usually a stale DNS cache, a misconfigured or unreachable DNS server, or a VPN/security software conflict.

## Networking Issues

### Wi-Fi Keeps Dropping or Running Slow

**Symptoms:** Wi-Fi disconnects intermittently, reconnects on its own, or throughput is far below the expected speed, even close to the router.

**Steps to diagnose and fix:**

**Check adapter power management** (a common silent culprit): Device Manager, then Network adapters, then your Wi-Fi adapter, then Properties, then the Power Management tab. Uncheck "Allow the computer to turn off this device to save power."

**Update or roll back the Wi-Fi driver:** Device Manager, right-click the adapter, Update driver. If problems started after a recent update, try "Roll Back Driver" instead.

**Flush DNS and renew the IP lease** (rules out a DNS/DHCP-side cause):
```bash
ipconfig /flushdns
ipconfig /release
ipconfig /renew
```

**Run the built-in network troubleshooter:** Settings, then Network & Internet, then Network troubleshooter.

**Check for channel congestion** if near other networks; switching the router to a less crowded channel (5GHz vs 2.4GHz) can help if adjustable.

**Root cause:** Most often adapter power-saving settings or an outdated driver; less commonly a DNS/DHCP issue or Wi-Fi channel interference.
