# Network Troubleshooting: Reaching the R740 Over a Direct Cable

**Champlain College, Cybersecurity Capstone**
**Team:** CJ Batista, Connor Clune
**Date of the work:** 14 Nov. 2026

On 14 Nov. 2026 we cabled the R740 straight to a MacBook and could not reach it. The cause was that the server's physical network ports were disabled. Once we enabled them, Proxmox answered on NIC 4. This doc records what we tried, what each test showed, and what we learned. The current working setup is in [lab-setup.md](lab-setup.md).

## The goal

A direct link between one MacBook and the server, with no internet on the server. One Ethernet cable from the server to the MacBook's USB Ethernet adapter, no switch, no router.

## What we saw at the start

- The cable link was up on the MacBook at 1 Gbps full duplex, so the cable and both ports were fine at the electrical level.
- macOS showed "Self-assigned IP" (`169.254.75.198`) on the adapter. That means nothing on the cable handed out an address, and the adapter had no manual one.
- The MacBook saw no other device on the cable.

## What we tried

| Step | What we did | What it showed |
|---|---|---|
| 1 | Gave the MacBook adapter a manual address, `10.10.10.1/24`, no router, and pinged `10.10.10.2` | "Host is down." The Mac asked on the cable who had that address and nothing answered. |
| 2 | Moved the cable through every regular network port on the server | Nothing answered on any port, not even an IPv6 ping to all devices on the cable (`ping6 ff02::1%en5`). A running Proxmox on a live port answers that with no setup at all, so the operating system was not using any of those ports. |
| 3 | Moved the cable to the iDRAC port and added a second Mac address, `192.168.0.50/24`, to try iDRAC's factory address `192.168.0.120` and `192.168.0.121` | No answer. |
| 4 | Listened on the cable with `sudo tcpdump -i en5 -n -e -c 20` | A Dell device on the iDRAC port was asking for an address (DHCP request) every few seconds. Nobody was answering. |
| 5 | Ran macOS's built-in DHCP server (`bootpd`) on the cable only, handing out one address, `10.10.10.2`, with no router and no DNS | iDRAC took `10.10.10.2` and answered pings in about 1 ms. It reported itself as a PowerEdge R740 on iDRAC9 firmware 7.00.00.182. |
| 6 | Opened the iDRAC web page at `https://10.10.10.2` | The page loaded, but the login did not accept the credentials we tried. Not resolved in this record. |
| 7 | Looked at the Proxmox console | Proxmox's management bridge `vmbr0` sits on NIC 4. |
| 8 | Found and enabled the server's disabled physical network ports | Proxmox answered on NIC 4, and we logged in to the web UI from the MacBook. |

## Root cause

The server's physical network ports were disabled. With them off, nothing on the regular ports could answer, which is why steps 1 and 2 failed no matter which port we used. The iDRAC port works on its own, separate from the operating system, which is why it was the only thing we could find (steps 4 and 5).

We have not yet recorded where the ports were disabled or the exact setting we changed. That is on the list in [lab-setup.md](lab-setup.md#not-recorded-yet).

## Final setup

| Device | Address |
|---|---|
| Proxmox, `vmbr0` on NIC 4 | `192.168.0.121` |
| MacBook USB Ethernet adapter | `192.168.0.100/24`, no router |

The web UI is at `https://192.168.0.121:8006`. The MacBook has IP forwarding off and Internet Sharing off, so the server has no path to the internet.

## What we learned

- **A link light only proves the cable.** Both ends also need an address in the same range before they can talk.
- **Check which way the Mac sends a ping.** When the Mac has no address in a range, it sends traffic for that range out its default route, which was Wi-Fi. Some of our early pings to `192.168.0.121` never went down the cable at all. `route -n get <address>` shows which interface the Mac will use.
- **Listen before guessing.** `tcpdump` on the cable showed what the other end was actually doing (asking for an address) in under a minute.
- **`vmbr0` is not a port you can find on the back of the server.** It is a Proxmox software bridge. The `bridge-ports` line in `/etc/network/interfaces` names the real port, and `ethtool -p <port> 60` blinks it.
- **The iDRAC port is separate from the operating system.** It is useful for checking a server that does not answer on its regular ports.
- **Boot keys on the R740:** F2 is System Setup (BIOS and iDRAC settings), F10 is the Lifecycle Controller (firmware, RAID, OS install), F11 is the one-time boot menu.

## Cleanup still owed

- [ ] The MacBook still has the DHCP server config at `/etc/bootpd.plist` from step 5. Remove it with `sudo rm /etc/bootpd.plist` once we no longer need to give iDRAC a temporary address.
- [ ] The iDRAC lease from step 5 was temporary. If we keep using iDRAC, set a fixed address inside iDRAC and fix the login.
