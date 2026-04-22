# RSS Bridge Wrapper Source

Runtime wrapper source for the Home Assistant add-on that wraps RSS-Bridge.

This repository is not the final Home Assistant add-on repository. It only
holds the child-repository coordination artifacts for the wrapper pattern used
with the canonical parent add-on repository.

The published Home Assistant add-on metadata, build configuration, icons, and
Supervisor-facing files must remain in the parent repository.

## What lives here

- `README.md`: wrapper-source contract and coordination notes
- `CHANGELOG.md`: wrapper-source changelog
- `VERSION`: child version used for parent sync
- `wrapper-source.yaml`: small metadata file for upstream context
- `run.sh`: wrapper runtime reference kept here for coordination
- `.github/workflows/notify-parent-add-on-repo.yml`: required parent
  notification workflow

## What does not live here

- no `repository.yaml`
- no final `config.yaml`
- no final add-on `Dockerfile`
- no final add-on publication assets
- no automatic synchronization of canonical parent files

## Wrapper responsibilities

This wrapper-source repository coordinates:

- the visible wrapper version published by tag
- the wrapper context for RSS-Bridge as a third-party upstream application
- the runtime approach used by the parent add-on
- the changelog history that the parent can mirror

## Parent relationship

This add-on follows the wrapper pattern.

That means:

- the parent repository remains the single published Home Assistant add-on
- the child repository coordinates version and wrapper context
- the parent should synchronize the visible add-on version from the child tag
- the parent should synchronize `CHANGELOG.md` from the child release flow
- the parent must not auto-sync canonical add-on files from this child repo
- the parent must pin the upstream RSS-Bridge image or source reference
  manually when that upstream changes

## Upstream strategy

The recommended approach for this wrapper is to use the official upstream
container image and add only a thin Home Assistant wrapper on top:

- ingress as the primary access path for human use in Home Assistant
- additional direct local HTTP access for machine-to-machine consumers such as
  Feedreader or other backend integrations
- persistent storage under `/data/rss-bridge`
- generated `config.ini.php` for safe defaults
- clear startup logs
- no custom patching unless ingress testing later proves it is necessary

This keeps the add-on simpler than rebuilding RSS-Bridge from source while
still allowing the parent repository to remain the canonical add-on source of
truth.

## Access model

The child repository should describe the wrapper as supporting two complementary
access patterns:

- ingress remains the preferred path for human interaction with the RSS-Bridge
  UI inside Home Assistant
- direct local HTTP access remains available for integrations that need to
  consume feeds over the Home Assistant network without going through the human
  ingress flow

This repository documents that behavior as wrapper context only. The canonical
published add-on files that implement and expose that access model still belong
to the parent repository.

## Authentication behavior

The wrapper generates `config.ini.php` on each startup from add-on options.

- if `auth_token` is empty, the generated config keeps authentication disabled
- if `auth_token` has a value, the generated config enables token
  authentication and writes that token into the managed config

The wrapper does not claim token protection unless the option is actually set.
