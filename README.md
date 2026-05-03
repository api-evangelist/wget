# Wget

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
