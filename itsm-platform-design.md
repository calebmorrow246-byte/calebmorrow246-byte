# Self-hosted ITSM platform: design case study

**Status:** designed and evaluated; not deployed. This is an architecture write-up of work I did, with business and commercial details removed.

## The problem

A hosted IT service-management platform was serving the team, but reporting was thin for leadership visibility, and the data and automation roadmap depended on a vendor. The question I explored was whether a **self-hosted, open-source ITSM platform** could replace it, giving the team ownership of the platform and its data and a foundation for automation and AI on top.

## The design

**Platform:** GLPI (open source), on Ubuntu 24.04 LTS with Nginx, PHP 8.2+ and MySQL 8.0, hosted as a virtual machine on the existing hypervisor pool with scheduled snapshot backups.

**Sizing:** the vendor publishes no hardware requirements, so I took community guidance for a medium deployment (about 4 vCPU, 8 GB RAM, 100 GB disk) and doubled it for growth headroom: **8 vCPU, 16 GB RAM, 200 GB thin-provisioned disk**. The reasoning is documented so it can be revisited with real load data.

### Integrations

| Integration | Approach |
|---|---|
| **Single sign-on** | GLPI's OAuth2/SAML plugin against Entra ID, so agents sign in with their existing Microsoft 365 identity and there is no separate password to manage. |
| **HR system provisioning** | Preferred path: HR system → Entra ID inbound provisioning (native Microsoft connector) → GLPI SCIM plugin. Requirement noted: the SCIM endpoint must be reachable from Entra. Fallback: a PowerShell polling script against the HR system's REST API feeding the GLPI REST API. |
| **Directory** | No custom code needed. The identity-management tool provisions users into Active Directory, and GLPI's built-in LDAP connector syncs from AD, so the platform simply sees AD. |
| **Chat notifications** | Microsoft Teams webhooks for ticket notifications, SLA alerts and approvals, using GLPI's native webhook support. |
| **Email-to-ticket** | Exchange Online mailbox polling or push using standard GLPI mail configuration. |

### Migration plan (what moves, and how)

The key insight was that not everything exports the same way, so the plan is a data matrix rather than a single export:

| Data | Method |
|---|---|
| Tickets (basic fields) | Admin CSV export |
| Ticket conversations | API only, per ticket (not in the CSV) |
| Attachments | API download, per conversation |
| Requesters and agents | API, paginated |
| Knowledge base | Admin HTML export |
| SLA policies | Manual documentation (no API export) |
| Automation rules | Manual documentation (no API export) |
| Canned responses | Manual scrape (the API is read-only for these) |

Existing automation and the ITSM MCP integration would be ported to the new platform's REST API, with one-time migration utilities (such as duplicate-requester merging) run before cutover.

## What I'd highlight

- **Constraint-driven design:** choosing integrations that need the *least* custom code (native SSO, SCIM and LDAP) and keeping custom scripts only as documented fallbacks.
- **A realistic migration inventory:** identifying early which data has no export path, so manual work is planned instead of discovered at cutover.
- **Evidence-based sizing:** doubling a documented baseline instead of guessing, with the rationale written down.

## Outcome

The design was evaluated and not taken to deployment. The integration pattern, the migration matrix and the sizing method are reusable for any platform migration.
