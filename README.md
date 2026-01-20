# DNS-over-HTTPS (DoH) Blocklist for Pi-hole

A curated blocklist designed to **prevent devices, browsers, and applications from bypassing local DNS policy using DNS-over-HTTPS (DoH) or related encrypted DNS endpoints**.

This list is intended for **managed networks** (home, family, lab, or small-office environments) where DNS policy enforcement, content filtering, or network-wide ad/malware blocking is required.

---

## Why this list exists

Modern browsers, mobile OSes, and smart devices increasingly attempt to bypass local DNS resolvers by using **hardcoded DNS-over-HTTPS providers** such as Google, Cloudflare, Quad9, or NextDNS.

When DoH is enabled:
- Network-wide DNS filtering (Pi-hole, AdGuard Home, etc.) is bypassed
- Parental controls become ineffective
- Malware / phishing domain blocking can be silently avoided
- DNS visibility and control shift to third-party providers

This blocklist **restores DNS authority to your local resolver** by blocking known DoH bootstrap and resolver endpoints.

---

## What this list blocks

This list includes domains for major public DoH and DNS providers, including:

- Google Public DNS (DoH)
- Cloudflare DNS (DoH)
- Quad9
- AdGuard DNS
- OpenDNS / Cisco Umbrella DoH
- CleanBrowsing
- NextDNS
- dns.sb
- LibreDNS
- Other public DoH infrastructures

Blocking these endpoints forces clients to **fall back to system DNS**, which in a Pi-hole setup means:
```
Client → Pi-hole → Upstream DNS
```

---

## Intended use cases

This list is appropriate for:

- Home networks with Pi-hole
- Parental control setups
- Content filtering (adult, malware, tracking)
- Smart TVs, Android devices, and IoT environments
- Labs and learning environments
- Any network where DNS policy must be enforced

This list is **not intended** for:
- Public Wi-Fi hotspots
- Untrusted networks where encrypted DNS is required for privacy

---

## Recommended format

This repository provides the list in **hosts format**, which is compatible with:

- Pi-hole
- AdGuard Home
- Hosts-based blockers
- DNS firewalls that accept hosts syntax

---

## How to use with Pi-hole

1. Copy the **raw GitHub URL** of the blocklist file, for example:
   ```
   https://raw.githubusercontent.com/<your-username>/<repo>/main/doh-blocklist.hosts
   ```

2. In Pi-hole Admin:
   - Go to **Group Management → Adlists**
   - Add the raw URL
   - Save

3. Update Pi-hole:
   ```bash
   sudo pihole -g
   sudo pihole reloaddns
   ```

4. (Optional) Flush client DNS cache:
   - Windows:
     ```cmd
     ipconfig /flushdns
     ```
   - Restart browsers or devices if needed

---

## Expected behavior after enabling

- Browsers using Secure DNS / DoH will silently fall back to system DNS
- Pi-hole will regain full visibility and control over DNS traffic
- Network-wide ad blocking and category filtering will become enforceable
- No noticeable performance degradation for normal browsing

---

## Possible side effects

- Some browsers may report that “secure DNS” is unavailable
- A small number of apps may warn about DNS configuration (rare)
- DoH-only applications may stop resolving until they fall back

These effects are expected and intentional.

---

## Security and privacy considerations

Blocking DoH on a managed network:
- Improves enforceability of DNS-based security controls
- Reduces third-party DNS telemetry
- Aligns with enterprise and school network practices

This list **does not weaken encryption of web traffic (HTTPS)**.
It only controls how domain names are resolved.

---

## Disclaimer

No DNS blocklist is perfect or exhaustive.

New DoH endpoints may appear over time.
This list is maintained on a **best-effort basis** and should be used alongside:

- Pi-hole blocklists (ads, malware, NSFW)
- Safe search enforcement where applicable
- Browser-level controls when needed

---

## License

MIT License

---

## Contributions

Pull requests are welcome for:
- New DoH providers
- Corrections or removals
- Documentation improvements

Please avoid adding:
- Generic CDN domains
- Non-DNS-related services
- IP-only endpoints (Pi-hole is domain-based)

---

## Summary

This list exists to answer a simple question:

> *Who controls DNS on this network — the network owner, or the device vendor?*

This blocklist ensures the answer is **you**.
