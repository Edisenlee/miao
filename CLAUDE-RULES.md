# Claude rule maintenance

Updated 2026-10-14. This ruleset prioritizes privacy: extra proxy coverage is acceptable, native client IP exposure is not. Claude.list is the reviewed Claude subset. Redirect.list embeds the same entries so existing myrules.ini subscriptions keep working without changing providers or groups.

## Sources

- Official required endpoints: https://code.claude.com/docs/en/network-config
- Official API inbound IPs: https://platform.claude.com/docs/en/api/ip-addresses
- Domain baseline: https://github.com/v2fly/domain-list-community/blob/2c892a618f4e23c549d28edd0f3f75407521b1aa/data/anthropic
- Recent comparison: https://github.com/VPSDance/ai-proxy-rules/commit/cc70f98b225e8f65b637df08e49040337610ee08 and https://github.com/inkzuji/Rules/commit/41ba407b65ac74aadb6a394d5dab80d8c54db954

The October updates add claude.dev. Official inbound addresses are IPv4 160.79.104.0/23 and IPv6 2607:6bc0::/48. Broader /21, /32 and AS399358 matches are deliberately retained as additional proxy protection. The /21 is official Anthropic outbound infrastructure, not the official API inbound range. Shared dependency suffixes and datadog/sentry/sift keywords intentionally proxy unrelated traffic too. Non-Claude sections remain unchanged.

## Applying and updating

Bind Claude traffic to a protected proxy group with no DIRECT fallback. Domain matches apply to both address families when the client has domain information; disabling IPv6 DNS alone does not enforce final server egress or block literal IPv6 connections. IPv6 capture, DNS routing, rule priority and fail-closed firewall behavior must be configured outside this list. A transparent router cannot reliably use a client PROCESS-NAME match. Explicit application HTTP proxying can retain hostnames before IP-based direct bypass rules.

Review official endpoints and upstream file changes, then update Claude.list and its embedded Redirect.list section together. Existing Redirect.list clients refresh the contents on their normal provider update. Full myrules.ini changes require configuration review before applying. No account-safety claim or automatic monitoring workflow is provided.
