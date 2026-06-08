

# NAT Configuration Lab

Configured Network Address Translation (NAT/PAT) on a Cisco 1941 router in Cisco Packet Tracer to allow internal private network hosts to reach an external network through a single public interface.

---

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

The translation table showed private IPs (192.168.1.x) being mapped to the router's public interface (172.16.0.2).

---

## Screenshots

| File | Description |
|------|-------------|
| `nat_topology.png` | Network topology diagram |
| `nat_cli_open.png` | Router CLI open in Packet Tracer |
| `nat_inside_outside.png` | Inside and outside interfaces configured |
| `nat_access_list.png` | Access list created |
| `nat_pat_save.png` | PAT overload command and config saved |
| `nat_ping_pc1.png` | Ping from PC1 successful |
| `nat_ping_pc2.png` | Ping from PC2 successful |
| `nat_translation_table.png` | NAT translation table output |

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
