# meshcore-regions

Canonical, community-editable catalog of MeshCore regions used worldwide.

## What this is

A simple JSON catalog of region identifiers used across the MeshCore ecosystem. Each region has a stable `code` (e.g. `de-hh-attraktor` or `hansemesh`), a human-readable `name` (the leaf label, e.g. `Attraktor`), and optional nested children. A region's `code` never changes once published, even if it gets re-nested under a different parent.

## How to consume

Two stable raw URLs:

- Full catalog (tree + flat lookup):
  `https://raw.githubusercontent.com/marcelverdult/meshcore-regions/main/index.json`
- One country at a time:
  `https://raw.githubusercontent.com/marcelverdult/meshcore-regions/main/regions/<code>.json`

Each region node has this shape:

```json
{
  "code": "de-hh-attraktor",
  "name": "Attraktor",
  "regions": [ /* same shape, optional */ ]
}
```

`code` is stable and unique across the catalog. It usually mirrors the path from the root (e.g. `de-hh-attraktor`), but named networks that span multiple parents may keep a standalone code (e.g. `hansemesh` nested under `de`). The `flat` array in `index.json` lists every node as `{ "path": "<code>", "name": "<name>" }` for quick lookups; `path` equals the node's `code`.

## How to contribute

Pull requests may only modify files matching:

- `regions/*.json`
- `unsorted/todo.json`

Anything else (scripts, workflows, schemas, `index.json`, `README.md`) is maintained by repository maintainers via direct commits.

Rules enforced automatically by CI:

- **No new country root files.** PRs may not add files to `regions/`. The 249 ISO country codes plus `sco` and `ioi` are already seeded; if you need another root, open an issue.
- **No deletions** in `regions/`. Once a region is in the tree, it stays.
- **Moves require approval.** If your PR moves a node from one parent to another, a maintainer adds the `approved-move` label before merge.
- **Subdivision additions and name edits are free.** Add subdivisions under existing parents, fix a display name — no label needed.
- Codes are lowercase ASCII letters, digits, and hyphens. Each hyphen-separated segment is capped at 29 characters to match the MeshCore firmware region-name buffer (`char name[31]` in `RegionMap.h`, minus one byte reserved for the implicit `#` prefix the firmware prepends when deriving auto-hashtag transport keys; see meshcore-dev/MeshCore#2434). A region's `code` is immutable — once published, it does not change, even if the node is re-nested under a different parent.
- Children of any node are sorted by `code`.

## How sync works

The catalog refreshes every night from the public MeshCore map at http://map.kiekr.app. Two ways to add a new region:

- Pin your repeater on the map with the KiekR App for Android or iOS (https://kiekr.app); your region appears here on the next sync.
- Open a pull request against this repository.

## Last updates

<!-- regions:auto-status:begin -->

- Last sync: `2026-08-04T05:41:10Z`
- Roots: 252
- Total nodes: 1568
- Unsorted entries: 657

| when (UTC) | kind | path | note |
|---|---|---|---|
| 2026-08-03T16:22:32Z | manual | c3aa965 | Merge pull request #53 from marcelverdult/add-de-bsmesh-rheinmain-trier |
| 2026-08-03T16:22:11Z | manual | f20dc24 | Merge pull request #61 from marcelverdult/sync/auto |
| 2026-08-03T06:13:01Z | sync | 5e4b8e7 | sync: 7 added, 54 resolved, 646 unsorted |
| 2026-08-02T05:49:09Z | sync | a17c381 | Merge pull request #60 from marcelverdult/sync/auto |
| 2026-08-02T05:48:50Z | sync | 5ff523c | sync: 1 added, 54 resolved, 646 unsorted |
| 2026-08-01T05:48:18Z | sync | 54c62f3 | Merge pull request #59 from marcelverdult/sync/auto |
| 2026-08-01T05:48:13Z | sync | a0767d9 | sync: 5 added, 54 resolved, 645 unsorted |
| 2026-07-31T05:59:10Z | sync | f4e28de | Merge pull request #58 from marcelverdult/sync/auto |
| 2026-07-31T05:58:53Z | sync | 004daf7 | sync: 21 added, 54 resolved, 642 unsorted |
| 2026-07-30T05:33:02Z | sync | 0a36631 | Merge pull request #57 from marcelverdult/sync/auto |
| 2026-07-30T05:32:54Z | sync | 912a961 | sync: 7 added, 47 resolved, 626 unsorted |
| 2026-07-29T05:44:19Z | sync | f43d1f8 | Merge pull request #56 from marcelverdult/sync/auto |
| 2026-07-29T05:44:14Z | sync | 201ceb9 | sync: 9 added, 46 resolved, 615 unsorted |
| 2026-07-27T06:20:50Z | sync | f932230 | Merge pull request #55 from marcelverdult/sync/auto |
| 2026-07-27T06:20:44Z | sync | 3ab9b9d | sync: 5 added, 46 resolved, 609 unsorted |
| 2026-07-25T05:36:43Z | sync | 5f58212 | Merge pull request #54 from marcelverdult/sync/auto |
| 2026-07-25T05:36:36Z | sync | 2b41d94 | sync: 11 added, 46 resolved, 599 unsorted |
| 2026-07-24T13:36:58Z | manual | 1da29fa | Add bsmesh, rhein-main and trier under de |
| 2026-07-24T05:42:50Z | sync | 8fc9223 | Merge pull request #52 from marcelverdult/sync/auto |
| 2026-07-24T05:42:45Z | sync | a34338a | sync: 2 added, 46 resolved, 598 unsorted |

<!-- regions:auto-status:end -->

## License

[CC0 1.0 Universal](LICENSE) — public-domain dedication. This catalog is
released with no rights reserved: copy, modify, redistribute, and embed it
(including in firmware) for any purpose, with no attribution required.
