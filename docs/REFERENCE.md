# pythoncodeAWS source reference


Source reviewed: [`5f88a03edfd8`](https://github.com/noel-ult/pythoncodeAWS/commit/5f88a03edfd84a7fe6d35560c124c74205c159ef).

This reference records the checked-in source, scripts, configuration names, and route declarations. It is a navigation aid; service availability and successful test execution require separate verification.

## HTTP route declarations

Paths are **as declared in each source file**. Router/blueprint mount prefixes from the entry point must be prepended; the project guide describes the active entry point and common prefixes. Alternate entry points (such as SQLite) are listed separately by file. Authentication, request bodies, and response schemas live in the linked handlers/models.

| Source | Method | Declared path | Handler |
| --- | --- | --- | --- |
| [app.py](../app.py) | GET | `/` | `home` |
| [app.py](../app.py) | POST | `/register` | `register` |

## Existing documentation

Historical plans/reports describe their own revision; use current source when they disagree.

- [requirements.txt](../requirements.txt)

## Source and configuration map

Generated lockfiles, binary assets, compiled output, vendored dependencies, and cached bytecode are omitted. Test files remain listed so coverage can be located.

- [Dockerfile](../Dockerfile)
- [app.py](../app.py)
- [requirements.txt](../requirements.txt)
- [templates/index.html](../templates/index.html)
