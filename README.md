# Wget

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

GNU Wget is a free, open-source command-line utility for non-interactive downloading of files from the web using HTTP, HTTPS, FTP, and FTPS protocols. It supports recursive downloading, resuming aborted downloads, mirroring websites, proxy support, and can be run from scripts and cron jobs. Wget2 is the next-generation successor, written from scratch with multi-threading, HTTP/2, and a plugin API via libwget.

**Website:** https://www.gnu.org/software/wget/

## APIs

### Wget

GNU Wget is a free command-line utility for non-interactive downloading of files from the web using HTTP, HTTPS, FTP, and FTPS. It supports recursive downloading, resume of aborted downloads, website mirroring, HTTP proxies, cookies, and persistent connections.

- **Documentation:** https://www.gnu.org/software/wget/manual/
- **Getting Started:** https://www.gnu.org/software/wget/manual/wget.html
- **Download:** https://ftp.gnu.org/gnu/wget/
- **Source Code:** https://git.savannah.gnu.org/cgit/wget.git
- **Bug Tracker:** https://savannah.gnu.org/bugs/?group=wget

### Wget2

GNU Wget2 is the next-generation successor to GNU Wget, built from scratch around libwget. It is multi-threaded, supports HTTP/2, HTTP compression, parallel connections, If-Modified-Since headers, plugin APIs, RSS/Atom feed scanning, Sitemap XML support, and Metalink.

- **Documentation:** https://gnuwget.gitlab.io/wget2/reference/
- **Source Code:** https://gitlab.com/gnuwget/wget2
- **Plugin API:** https://gnuwget.gitlab.io/wget2/reference/group__libwget-plugin.html
- **Releases:** https://gitlab.com/gnuwget/wget2/-/releases

## JSON Schemas

| Schema | Description |
|---|---|
| [Wget Download Request](json-schema/wget-download-request-schema.json) | Schema for GNU Wget download request configuration |
| [Wget2 Plugin](json-schema/wget2-plugin-schema.json) | Schema for Wget2 plugin API structure via libwget |

## JSON Structures

| Structure | Description |
|---|---|
| [Wget Download Request](json-structure/wget-download-request-structure.json) | Structure of a Wget download request |
| [Wget2 Plugin](json-structure/wget2-plugin-structure.json) | Structure of a Wget2 plugin definition |

## JSON-LD Context

- [wget-context.jsonld](json-ld/wget-context.jsonld) — Linked data context mapping Wget vocabulary to schema.org and project-specific terms

## Vocabulary

- [wget-vocabulary.yml](vocabulary/wget-vocabulary.yml) — Domain vocabulary covering download operations, protocol support, plugin API concepts, and configuration

## Common Resources

| Type | URL |
|---|---|
| Website | https://www.gnu.org/software/wget/ |
| Documentation | https://www.gnu.org/software/wget/manual/ |
| Source Code | https://git.savannah.gnu.org/cgit/wget.git |
| GitLab Organization | https://gitlab.com/gnuwget |
| Mailing List | https://lists.gnu.org/mailman/listinfo/bug-wget |
| Bug Tracker | https://savannah.gnu.org/bugs/?group=wget |
| Download | https://ftp.gnu.org/gnu/wget/ |
| License | https://www.gnu.org/licenses/gpl-3.0.html |

**Maintainer:** Kin Lane (kin@apievangelist.com)
