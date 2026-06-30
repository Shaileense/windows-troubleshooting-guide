# Windows Troubleshooting Resources

A curated list of free tools and references used alongside this guide.

## Diagnostic Tools
- [Sysinternals Suite](https://learn.microsoft.com/en-us/sysinternals/) — Process Explorer, Autoruns, TCPView, and more. Essential for advanced troubleshooting.
- [CrystalDiskInfo](https://crystalmark.info/en/software/crystaldiskinfo/) — Check hard drive health and SMART data.
- [HWiNFO](https://www.hwinfo.com/) — Detailed hardware info, temps, and sensor readings.
- [Malwarebytes Free](https://www.malwarebytes.com/) — Quick malware scan when standard Defender scans come up clean.

## Built-in Windows Tools (Quick Reference)
| Tool | Command | Use |
|------|---------|-----|
| Event Viewer | `eventvwr.msc` | View system/app error logs |
| Reliability Monitor | `perfmon /rel` | Timeline of crashes and errors |
| Resource Monitor | `resmon` | Real-time CPU/RAM/disk/network per process |
| System File Checker | `sfc /scannow` | Repair corrupted system files |
| DISM Repair | `DISM /Online /Cleanup-Image /RestoreHealth` | Fix Windows image before SFC |

## Microsoft Documentation
- [Windows Commands Reference](https://learn.microsoft.com/en-us/windows-server/administration/windows-commands/windows-commands)
- [Windows 11 Troubleshooting](https://support.microsoft.com/en-us/windows)
- [Event ID Lookup](https://www.ultimatewindowssecurity.com/securitylog/encyclopedia/)

## Networking Tools
- [Wireshark](https://www.wireshark.org/) — Packet capture for network-level troubleshooting.
- [Advanced IP Scanner](https://www.advanced-ip-scanner.com/) — Fast LAN device discovery.
- [PuTTY](https://www.putty.org/) — SSH and serial console connections.
