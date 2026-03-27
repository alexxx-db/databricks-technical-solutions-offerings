# Archived offerings

This folder (`z-archive`) holds **retired** Specialist offerings that are **no longer indexed** for the Field Catalog or other internal tooling that syncs `catalog-listing.yml` files from the live domain trees.

The **`z-` prefix** sorts this directory **last** among top-level folders in the GitHub UI so casual browsers see active domains first.

## What “archived” means

- Content remains in this repository for **historical reference** and transparency.
- **`catalog-listing.yml` files under `/z-archive` must not be ingested** as active catalog entries. Downstream pipelines should exclude paths under `z-archive/` when discovering listings.
- Archived offerings are **not maintained** to the same bar as active contributions unless explicitly revived.

## Layout

Archived offerings keep the same **domain** structure as the rest of the repo, under `z-archive/<domain>/<offering-name>/`:

```
z-archive/
├── README.md                    # This file
├── data-warehousing/
│   ├── README.md                # Index of archived data warehousing offerings
│   └── <offering-name>/        # Retired offering (may include catalog-listing.yml)
...
```

## Git commands

Run these from the **repository root** on a feature branch (not directly on `main` unless your team allows it).

1. **Create the destination domain folder** under `z-archive/` if it does not exist yet (only needed the first time you archive something in that domain):

   ```bash
   mkdir -p z-archive/<domain>
   ```

   Replace `<domain>` with one of: `data-warehousing`, `data-engineering`, `gen-ai`, `cybersecurity`.

2. **Move the offering folder** (preserves history as a rename when Git detects it):

   ```bash
   git mv <domain>/<offering-name> z-archive/<domain>/<offering-name>
   ```

   Example:

   ```bash
   mkdir -p z-archive/data-warehousing
   git mv data-warehousing/finops-alerts z-archive/data-warehousing/finops-alerts
   ```

3. **Commit** the move with the rest of the retirement work (README updates, etc.).

## After the move

1. Add or update a short `README.md` inside the archived offering stating it is retired and linking to this file ([z-archive/README.md](README.md)).
2. Update the **live** domain README (e.g. `data-warehousing/README.md`) and the matching **`z-archive/<domain>/README.md`** index so tables of contents stay accurate.
3. Coordinate with owners of any **downstream pipeline** that discovers `catalog-listing.yml` files so paths under `z-archive/` stay excluded.

## Contributing

**Do not** add new offerings under `/z-archive`. New work belongs under the domain folders at the repository root (`data-warehousing`, `data-engineering`, `gen-ai`, `cybersecurity`). To retire an offering, follow [Git commands](#git-commands) and [After the move](#after-the-move) above. General contribution expectations are in [CONTRIBUTING.md](../CONTRIBUTING.md).
