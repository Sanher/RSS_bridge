# Parent Scaffold

This directory contains the canonical add-on scaffold prepared for
the `rss_bridge` directory in the canonical parent add-on repository.

It is intentionally kept outside the parent repository because this workspace is
scoped to the child repository. The files here are ready to copy into the
parent add-on directory without introducing automatic child-to-parent sync.

Recommended manual application target:

- `<parent-addons-repo>/rss_bridge`

The scaffold follows the wrapper pattern:

- parent is the only published Home Assistant add-on source of truth
- child coordinates version and wrapper context
- parent keeps its canonical files locally
- upstream RSS-Bridge image ref is pinned manually in the parent Dockerfile

## Suggested application

Create the target directory in the parent repository and copy the scaffolded
files into place:

```bash
mkdir -p <parent-addons-repo>/rss_bridge
cp -R <child-repo>/parent-scaffold/<parent-addon-dir>/. <parent-addons-repo>/rss_bridge/
```

After copying, review the parent repository as usual and keep the parent as the
only canonical source of the published add-on files.
