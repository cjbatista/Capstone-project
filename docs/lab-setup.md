# Lab Setup: Dell PowerEdge R740

**Champlain College, Cybersecurity Capstone**
**Team:** CJ Batista, Connor Clune
**Last updated:** 15 Nov. 2026

This is the record of our lab server: the hardware, the Proxmox install, and how we reach it. Every value here was seen on the server, in its web pages, or on the MacBook we connect from. Anything we have not checked yet is listed under [Not recorded yet](#not-recorded-yet) instead of guessed.

## At a glance

| Item | Value |
|---|---|
| Server | Dell PowerEdge R740 |
| Hypervisor | Proxmox VE 9.2.2 |
| Proxmox node name | `aiwebhuntsrv` |
| Proxmox web UI | `https://192.168.0.121:8006` |
| Network port in use | NIC 4, bridged as `vmbr0` |
| How we reach it | One Ethernet cable from NIC 4 to a MacBook |
| Internet access | None |

## Change from the original plan

Our first plan used an old Alienware desktop as the Proxmox host. The Alienware is scrapped. The Dell PowerEdge R740 described here is our only lab host.

## Completed work

1. **Obtained the server.** A Dell PowerEdge R740.
2. **Power and first boot.** Connected the server to power and brought it online.
3. **Initial physical configuration.** Completed the first hardware setup on the server.
4. **Installed Proxmox VE.** Version 9.2.2, node name `aiwebhuntsrv`.
5. **Configured the network interface.** Proxmox's management bridge `vmbr0` uses NIC 4, with the address `192.168.0.121`.
6. **Found the problem.** The MacBook could not reach the server on any port. The server's physical network ports were disabled.
7. **Fixed it.** We enabled the physical ports, and Proxmox started answering on NIC 4.
8. **Direct cable to the MacBook.** NIC 4 is cabled straight to the MacBook's USB Ethernet adapter. No switch, no router.
9. **Offline access works.** On 14 Nov. 2026 we logged in to the Proxmox web UI from the MacBook with no internet connection on the server.

The full troubleshooting story for steps 6 and 7 is in [network-troubleshooting.md](network-troubleshooting.md).

## Hardware

| Item | Value | Where it came from |
|---|---|---|
| Model | Dell PowerEdge R740 (Dell 14th generation) | iDRAC system info, 14 Nov. 2026 |
| Remote management | iDRAC9, firmware 7.00.00.182, Enterprise license | iDRAC system info, 14 Nov. 2026 |
| CPU, memory, disks, RAID controller | Not recorded yet | |

iDRAC is Dell's built-in management controller. It has its own network port (marked with a wrench icon) and works even when the server's operating system is not running.

## Proxmox VE

| Item | Value |
|---|---|
| Version | Proxmox VE 9.2.2 |
| Node name | `aiwebhuntsrv` |
| Management address | `192.168.0.121` |
| Management bridge | `vmbr0`, on physical port NIC 4 |
| Web UI | `https://192.168.0.121:8006`, user `root`, realm Linux PAM |

`vmbr0` is a software bridge that Proxmox creates. It is not a physical port. Proxmox ties it to one real port, and on our server that port is NIC 4. To see which port a bridge uses, run this on the Proxmox console:

```bash
grep -A6 vmbr0 /etc/network/interfaces
```

The `bridge-ports` line names the physical port. To find that port on the back of the server, `ethtool -p <port name> 60` blinks its light for 60 seconds.

We installed Proxmox before writing down the hardware details or planning the disk layout. Those details are listed below so we can record them before building VMs.

## Network

```
                 Wi-Fi (internet, MacBook only)
                        |
   +--------------------+--------------------+
   |               MacBook                   |
   |  USB Ethernet adapter, 192.168.0.100/24 |
   |  no router, IP forwarding off           |
   +--------------------+--------------------+
                        |  one Ethernet cable
   +--------------------+--------------------+
   |           Dell PowerEdge R740            |
   |  NIC 4 -> vmbr0, 192.168.0.121           |
   |  Proxmox VE 9.2.2 (aiwebhuntsrv)         |
   |                                          |
   |  iDRAC port: not cabled right now        |
   +------------------------------------------+
```

| Device | Interface | Address | How it is set |
|---|---|---|---|
| R740 (Proxmox) | `vmbr0` on NIC 4 | `192.168.0.121` | Set on the server |
| MacBook | USB Ethernet adapter, added to the macOS "Thunderbolt Bridge" network service | `192.168.0.100`, mask `255.255.255.0`, no router | Manual, in macOS Network settings |
| R740 (iDRAC) | Dedicated iDRAC port | `10.10.10.2` while we tested it | A temporary DHCP lease from the MacBook on 14 Nov. 2026, not a fixed setting. See the troubleshooting doc. |

## Connecting from the MacBook

1. Plug the Ethernet cable into the MacBook's USB Ethernet adapter and into NIC 4 on the server.
2. On the MacBook, the adapter's network service needs a manual address in the same range as Proxmox, with the Router field left empty. Ours is `192.168.0.100`, mask `255.255.255.0`.
3. Check the Mac sends server traffic down the cable, not over Wi-Fi:
   ```bash
   route -n get 192.168.0.121 | grep interface
   ```
   It should name the cable's interface (`bridge0` on our Mac), not `en0` (Wi-Fi).
4. Open `https://192.168.0.121:8006` and accept the certificate warning. Proxmox uses a self-signed certificate.
5. Log in as `root` with realm Linux PAM.

## Why the server stays offline

- The server's only network cable goes to the MacBook.
- The MacBook does not pass traffic between its networks. IP forwarding is off and Internet Sharing is off. We checked forwarding with:
  ```bash
  sysctl -n net.inet.ip.forwarding
  ```
  `0` means off.
- The MacBook's own internet stays on Wi-Fi. Leaving the Router field empty on the cable means the Mac never sends internet traffic down it.

Keep Internet Sharing off on the MacBook (System Settings, General, Sharing). It is the one setting that would give the server internet access through the Mac.

Being offline also means software for our VMs (ISOs, packages, container images) has to be copied onto the server. It cannot be downloaded from the server. See the note at the end of [ai-tool-options.md](ai-tool-options.md#tip-for-whichever-tool-we-pick).

## Not recorded yet

Fill these in before Phase 3:

- [ ] Date we got the R740, and one line on why we scrapped the Alienware.
- [ ] CPU model and core count, memory size, disks, and the RAID controller and its mode. iDRAC (System, Storage) or the Proxmox node Summary page shows these.
- [ ] Proxmox install choices: install disk, filesystem (ext4, ZFS, or other), and the gateway and DNS typed into the installer.
- [ ] Where the network ports were disabled and the exact setting we changed to enable them.
- [ ] The Linux name of NIC 4 (for example `eno4`), from the `bridge-ports` line.
- [ ] iDRAC: whether we keep using it, its login status, and a fixed address if we do.
- [ ] Which device is the secondary device that manages the R740 and runs the attacks, per our Methodology paper ([#81](https://github.com/cjbatista/Capstone-project/issues/81)).
- [ ] Where the iDRAC and Proxmox passwords are kept. They go in a password manager, never in this repo.
