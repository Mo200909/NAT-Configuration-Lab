# NAT Configuration Lab
## Network Topology

- **Internal network:** 192.168.1.0/24 (VInetPC1, VInetPC2)
- **Router:** VInetR1 (Cisco 1941)
- **External network:** 172.16.0.0/24 (WWW router)

---

## Configuration

**Set NAT inside and outside interfaces:**
```
interface g0/1
ip nat inside
exit
interface g0/0
ip nat outside
exit
```

**Create access list for inside network:**
```
access-list 1 permit 192.168.1.0 0.0.0.255
```

**Configure PAT overload:**
```
ip nat inside source list 1 interface g0/0 overload
```

**Save configuration:**
```
write
```

---

## Verification

Pinged the WWW router from both VInetPC1 and VInetPC2 — all 4 packets received with 0% loss confirming NAT is working.

Verified translations with:
```
show ip nat translations
```

Translation table showed private IPs (192.168.1.x) being mapped to the router's public interface (172.16.0.2).

---

## Screenshots

| Filename | Page | Content |
|----------|------|---------|
| `nat_access_list.png` | Page 1 | `access-list 1 permit 192.168.1.0 0.0.0.255` |
| `nat_cli_open.png` | Page 2 | Router CLI tab open in Packet Tracer |
| `nat_inside_outside.png` | Page 3 | `ip nat inside` and `ip nat outside` configured |
| `nat_translation_table.png` | Page 4 | `show ip nat translations` output |
| `nat_topology.png` | Page 5 | Network topology diagram |
| `nat_pat_save.png` | Page 6 | PAT overload + `write` config saved |
| `nat_ping_pc1.png` | Page 7 | Ping from PC1 successful |
| `nat_ping_pc2.png` | Page 8 | Ping from PC2 successful |

---

## What I Learned

- How to configure NAT and PAT on a Cisco router using Cisco IOS CLI
- How private IP addresses are translated to a public interface using overload
- How to verify NAT with the translation table

---

## Tools Used

- Cisco Packet Tracer
- Cisco IOS CLI (Cisco 1941 Router)

---

## Author

Mofolorunsho Adeleke — github.com/Mo200909
