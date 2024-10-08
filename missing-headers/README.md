# Templates for Missing HTTP Security Headers

Nuclei has this as a single finding, which isn't particularly helpful for the user - because it doesn't flag those headers that are missing. So we need to have our own templates for this.

I am basically breaking up this Nuclei template into separate templates for each header. This is because I want to be able to flag the specific header that is missing.

```yaml
id: http-missing-security-headers

info:
  name: HTTP Missing Security Headers
  author: socketz,geeknik,G4L1T0,convisoappsec,kurohost,dawid-czarnecki,forgedhallpass
  severity: info
  description: |
    This template searches for missing HTTP security headers. The impact of these missing headers can vary.
  tags: misconfig,headers,generic

requests:
  - method: GET
    path:
      - "{{BaseURL}}"

    host-redirects: true
    max-redirects: 3
    matchers-condition: or
    matchers:
      - type: dsl
        name: strict-transport-security
        dsl:
          - "!regex('(?i)strict-transport-security', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: content-security-policy
        dsl:
          - "!regex('(?i)content-security-policy', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: permissions-policy
        dsl:
          - "!regex('(?i)permissions-policy', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: x-frame-options
        dsl:
          - "!regex('(?i)x-frame-options', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: x-content-type-options
        dsl:
          - "!regex('(?i)x-content-type-options', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: x-permitted-cross-domain-policies
        dsl:
          - "!regex('(?i)x-permitted-cross-domain-policies', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: referrer-policy
        dsl:
          - "!regex('(?i)referrer-policy', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: clear-site-data
        dsl:
          - "!regex('(?i)clear-site-data', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: cross-origin-embedder-policy
        dsl:
          - "!regex('(?i)cross-origin-embedder-policy', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: cross-origin-opener-policy
        dsl:
          - "!regex('(?i)cross-origin-opener-policy', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: cross-origin-resource-policy
        dsl:
          - "!regex('(?i)cross-origin-resource-policy', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: access-control-allow-origin
        dsl:
          - "!regex('(?i)access-control-allow-origin', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: access-control-allow-credentials
        dsl:
          - "!regex('(?i)access-control-allow-credentials', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: access-control-expose-headers
        dsl:
          - "!regex('(?i)access-control-expose-headers', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: access-control-max-age
        dsl:
          - "!regex('(?i)access-control-max-age', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: access-control-allow-methods
        dsl:
          - "!regex('(?i)access-control-allow-methods', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and

      - type: dsl
        name: access-control-allow-headers
        dsl:
          - "!regex('(?i)access-control-allow-headers', all_headers)"
          - "status_code != 301 && status_code != 302 && status_code != 404"
        condition: and
```