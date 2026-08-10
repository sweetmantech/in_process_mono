# in_process_mono

An **organizing repo** for the In Process project. It is a thin shell whose only job is to pull the In Process codebases together as git submodules so they can be opened, searched, and reasoned about as a single workspace.

## Submodules

| Path        | Source repo                                                                 | Purpose                                  |
| ----------- | --------------------------------------------------------------------------- | ---------------------------------------- |
| `web/`      | [in_process](https://github.com/sweetmantech/in_process)                    | Client app                               |
| `api/`      | [In-Process-API](https://github.com/sweetmantech/In-Process-API)            | Backend API                              |
| `database/` | [in_process_database](https://github.com/sweetmantech/in_process_database)  | Supabase migrations & RPCs               |
| `indexer/`  | [Coins-Beneficiaries-Indexer](https://github.com/sweetmantech/Coins-Beneficiaries-Indexer) | Onchain indexer                         |
| `docs/`     | [docs](https://github.com/sweetmantech/docs)                                | Public documentation                     |
| `skills/`   | [in_process_skills](https://github.com/sweetmantech/in_process_skills)      | Agent skills for the In Process dev loop |

## How this repo is used

This monorepo exists so Claude Code (or any human) can open **every** In Process codebase at once. The main use cases:

- Cross-repo questions — e.g. _"What changed across In Process in the last 7 days?"_
- Cross-repo refactors where context from multiple codebases is needed to make a sound decision
- Onboarding — one clone gives a new developer the whole stack

The day-to-day code work does **not** happen here. It happens in the submodule repos.

## Where to open pull requests

| You want to...                                          | Open the PR in...                |
| ------------------------------------------------------- | -------------------------------- |
| Change the client app                                   | `sweetmantech/in_process`        |
| Change the API                                          | `sweetmantech/In-Process-API`    |
| Change the database schema                              | `sweetmantech/in_process_database` |
| Change the indexer                                      | `sweetmantech/Coins-Beneficiaries-Indexer` |
| Change the docs                                         | `sweetmantech/docs`              |
| Change an agent skill                                   | `sweetmantech/in_process_skills` |
| Add a new codebase to the workspace                     | **here** (`in_process_mono`)     |
| Bump a submodule pointer to a newer commit              | **here** (`in_process_mono`)     |

PRs against `in_process_mono` itself should be rare — **1–2 per year** is normal, **fewer than 10** in a year. The submodule repos, by contrast, see **1+ PRs per day**.

## Getting started

Clone with submodules:

```bash
git clone --recurse-submodules git@github.com:sweetmantech/in_process_mono.git
```

If you already cloned without `--recurse-submodules`:

```bash
git submodule update --init --recursive
```

Pull the latest from each submodule's tracked branch:

```bash
git submodule update --remote --merge
```

## Bumping a submodule pointer

When you want this monorepo to point at a newer commit of, say, the API:

```bash
cd api
git checkout main && git pull
cd ..
git add api
git commit -m "chore: bump api submodule"
git push origin main
```

That's one of the few situations where a PR (or direct push) against this repo is appropriate.
