# Hairpin NAT (NAT Reflection) in nftables



## The Issue

Internal services (e.g., `10.1.1.x`) cannot reach each other using their
external/DNAT'd IPs (e.g., `192.168.20.x`).



## The Cause

1. **Source** sends a packet to the DNAT IP (`192.168.20.x`).
2. **Host** translates destination to `10.1.1.x` and forwards it.
3. **Destination** sees a source IP on its own subnet (`10.1.1.x`) and replies
   **directly**, bypassing the host.
4. **Source** drops the packet because the reply comes from an unexpected IP
   (`10.1.1.x` instead of `192.168.20.x`).



## The Fix

Add a `masquerade` rule in the `postrouting` chain for traffic originating from
and destined for the same internal subnet. This forces the return traffic back
through the host.

```nftables
table ip nat {
    chain postrouting {
        type nat hook postrouting priority srcnat;
        
        # Enable Hairpin NAT
        ip saddr 10.1.1.0/24 ip daddr 10.1.1.0/24 masquerade
    }
}
```
