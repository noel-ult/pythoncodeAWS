# pythoncodeAWS: verification and operations

Reviewed against [default-branch commit f2a4cc7852d2](https://github.com/noel-ult/pythoncodeAWS/commit/f2a4cc7852d23adaf25511fd4aec741c944c8783) on 2026-10-28. Start with the [developer guide](../README.md) for installation and architecture, and the [source reference](REFERENCE.md) for exact scripts, configuration readers, routes, and source locations.

## S3 and MySQL flow

Use a disposable student and photo; verify both the database row and S3 object. Test a repeated filename and a database failure after upload to understand cleanup requirements.

These are acceptance scenarios for a maintainer to run in the documented environment. Their inclusion is not a claim that live integrations or production credentials were tested during this documentation update.

## Deployment and failure diagnosis

The database opens during import. Diagnose database connectivity before the HTTP port. S3 URL construction alone does not make an object public.

## Maintaining the contract

When behavior changes, update the guide and examples in the same PR. Check the entry point and working directory before copying commands. Use the linked source readers to distinguish build-time configuration from process environment. For failures, capture the first application error, runtime version, selected mode, and redacted configuration names before later proxy or port errors.

Keep changes tied to evidence: a declared command is not proof it passes, a process health response is not a successful end-to-end workflow, and a historical report describes its own revision. Record actual check results and any unavailable external services in the PR.
