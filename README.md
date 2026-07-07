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
