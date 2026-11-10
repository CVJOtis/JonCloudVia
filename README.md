# JonCloudVia

Working repository for CloudVia Solutions client engagements (Litify / Salesforce).

## What this repo is

A workspace for retrieved metadata, in-progress work, manifests, and notes, kept **strictly separated by client org**. It is not a CI/CD source and nothing here deploys automatically.

## Layout

```
clients/
  gs/    nlg/    jf/    sor/
    sfdx-project.json   # that client's own SFDX project
    force-app/          # metadata for that org only
    manifest/           # package.xml files scoped to that org
    notes/              # requirements, design decisions, findings
shared/                 # org-agnostic reference material only
```

## Rules

1. **Run `sf` commands from inside a client folder.** There is intentionally no `sfdx-project.json` at the repo root, so commands run from the root will fail rather than target the wrong org.
2. **Keep each client's metadata in its own folder.** Never copy files between client folders without reviewing them for that org.
3. **`shared/` is reference only.** Snippets, patterns, and scripts there are not deployed. To use one in an org, copy it into that client's `force-app/` and adapt it.
4. **No credentials in the repo.** Org auth lives in the local `sf` CLI keychain. `.gitignore` blocks `.sf/`, `.sfdx/`, keys, and env files.

## Working with a client org

```bash
cd clients/<client>
sf org login web --alias <client>-<env>        # e.g. gs-prod, gs-uat
sf project retrieve start --manifest manifest/package.xml --target-org <client>-<env>
```

Use a `<client>-<env>` alias convention so the target org is always explicit in every command.
