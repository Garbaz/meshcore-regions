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

- Last sync: `2026-08-15T03:31:58Z`
- Roots: 252
- Total nodes: 1671
- Unsorted entries: 973

| when (UTC) | kind | path | note |
|---|---|---|---|
| 2026-08-13T04:45:57Z | sync | 61ef49f | Merge pull request #72 from marcelverdult/sync/auto |
| 2026-08-13T04:45:50Z | sync | 3e4fca9 | sync: 13 added, 37 resolved, 931 unsorted |
| 2026-08-11T12:39:06Z | manual | 93f3300 | Merge pull request #69 from marcelverdult/add/community-region-sync-2026-08-07 |
| 2026-08-11T04:13:31Z | sync | b3211ec | Merge pull request #71 from marcelverdult/sync/auto |
| 2026-08-11T04:13:25Z | sync | 9d172b5 | sync: 3 added, 48 resolved, 918 unsorted |
| 2026-08-10T04:24:27Z | sync | 3b5107c | Merge pull request #70 from marcelverdult/sync/auto |
| 2026-08-10T04:24:09Z | sync | 9d09356 | sync: 6 added, 48 resolved, 927 unsorted |
| 2026-08-09T15:22:01Z | manual | 30a48b1 | Merge main into add/community-region-sync-2026-08-07 |
| 2026-08-09T04:12:19Z | sync | 9b26dc6 | Merge pull request #68 from marcelverdult/sync/auto |
| 2026-08-09T04:12:12Z | sync | 8afe527 | sync: 3 added, 57 resolved, 914 unsorted |
| 2026-08-08T04:06:43Z | sync | 826e584 | Merge pull request #67 from marcelverdult/sync/auto |
| 2026-08-08T04:06:35Z | sync | 5c0b575 | sync: 3 added, 57 resolved, 920 unsorted |
| 2026-08-07T17:33:14Z | manual | af449ae | feat: add 255 region codes from community site survey |
| 2026-08-07T16:57:59Z | manual | fc38f64 | Merge pull request #66 from marcelverdult/add/community-region-sync-2026-08-07 |
| 2026-08-07T16:55:44Z | sync | 6d399a3 | feat: add 253 region codes from community site survey |
| 2026-08-07T04:49:57Z | sync | 6cb5b3e | Merge pull request #65 from marcelverdult/sync/auto |
| 2026-08-07T04:49:50Z | sync | 92c90f6 | sync: 1 added, 57 resolved, 665 unsorted |
| 2026-08-06T12:11:44Z | manual | 38d5394 | Merge pull request #64 from marcelverdult/sync/auto |
| 2026-08-06T05:40:54Z | sync | 7a005e0 | sync: 7 added, 57 resolved, 664 unsorted |
| 2026-08-05T05:39:30Z | sync | 69c14fd | Merge pull request #63 from marcelverdult/sync/auto |

<!-- regions:auto-status:end -->

## License

[CC0 1.0 Universal](LICENSE) — public-domain dedication. This catalog is
released with no rights reserved: copy, modify, redistribute, and embed it
(including in firmware) for any purpose, with no attribution required.
