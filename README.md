# QA for Runwell

Each client's source of truth as checks and expectations, with test runs, issues and gates that keep work from done until it passes.

A plugin for [Runwell](https://github.com/Martin-Business-Consultants/runwellv2), the core of an
agency's project management. It owns its tables (`qa_*`), points at core records by id, and
extends Runwell only through its plugin hooks, so removing it leaves Runwell as it was.

## Install

In Runwell, **Settings > Plugins > Add a plugin**: press Install on QA, or enter
`Martin-Business-Consultants/runwell-qa`. Runwell downloads the latest release onto the server, restarts and creates the
plugin's tables. It starts off: switch it on in Settings > Plugins.

From the command line on the server: `bin/rails "plugins:install[Martin-Business-Consultants/runwell-qa]"`, then restart
Runwell.

Needs Runwell 2.1.0 or later. A plugin can use only the gems Runwell bundles.

## Updating

Settings > Plugins shows an Update button on the plugin when a newer release is out (it checks
nightly, or with Check for updates). The plugin updates only when someone presses it; if the new
release won't load, the previous one comes back.

## Loading checks from a file

`examples/acme_storage.yml` shows a client's checks and source of truth as YAML. On the server:
`bin/rails "qa:import[path/to/file.yml]"`.

## Developing

Clone this repository beside a Runwell checkout and link it in, from Runwell's directory:

```sh
bin/rails "plugins:link[../runwell-qa]"
bin/rails db:migrate
bin/dev
```

## Releasing

Bump `VERSION` in `lib/qa/version.rb`, commit, then tag and publish a GitHub release:

```sh
git tag v0.2.0 && git push origin main v0.2.0
gh release create v0.2.0 --generate-notes
```

Installs see it in Settings > Plugins.

## License

[FSL-1.1-MIT](LICENSE.md), like Runwell.
