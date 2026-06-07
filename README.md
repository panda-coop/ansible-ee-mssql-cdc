# ansible-ee-mssql-cdc

Ansible **Execution Environment** for managing SQL Server **Change Data Capture**.
It bakes, into one OCI image, everything a CDC run needs:

- the [`mykola_kharchenko.mssql_cdc`](https://galaxy.ansible.com/ui/repo/published/mykola_kharchenko/mssql_cdc/) collection (`requirements.yml`)
- `pyodbc` (`requirements.txt`) + its build deps (`bindep.txt`)
- Microsoft **ODBC Driver 18** + unixODBC (installed from the MS repo in `execution-environment.yml`)

## Image

```
ghcr.io/panda-coop/ansible-ee-mssql-cdc:latest      # moved on every main push
ghcr.io/panda-coop/ansible-ee-mssql-cdc:<version>   # set by pushing a git tag vX.Y.Z
```

CI (`.github/workflows/build-ee.yml`) builds with `ansible-builder` and pushes to GHCR on push to
`main`, on `v*` tags, and on manual dispatch.

## Build locally

```bash
ansible-builder build --tag localhost/mssql-cdc-ee:latest \
  --container-runtime podman --verbosity 2
```

## Consumers

`ansible-navigator.yml` in the CDC project (now `panda-coop/fabric` → `ansible/`) points
`execution-environment.image` at the published tag above.
