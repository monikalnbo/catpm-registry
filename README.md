# catpm-registry

Package registry for [catpm](https://github.com/monikalnbo/catpm) — the CatBase
dependency package manager. This repository IS the registry: an `index.json`
plus `.cpkg` package archives served over `raw.githubusercontent.com`.

## Use it

Put this line in your `package.where` (or use it as the only source):

```
https://raw.githubusercontent.com/monikalnbo/catpm-registry/main
```

then:

```bash
catpm add mathx        # or timex / randx / stringx / fmtx / loganx
```

## Packages

| name | versions | deps | description |
|---|---|---|---|
| mathx | 0.2.0, 0.3.0, 0.4.0 | stringx ^0.3.0 (0.2/0.3) | gcd/lcm/primality/fib/power/collatz |
| stringx | 0.3.0 | — | shout/pad/words/reverse |
| fmtx | 0.1.0 | stringx ^0.3.0 | banner/bracket formatting |
| loganx | 0.1.0 | — | tag/tri/toy helpers |
| timex | 0.1.0 | stringx ^0.3.0 | real UTC time via POSIX date; iso8601/epoch/stamp |
| randx | 0.1.0 | timex ^0.1.0 | seeded deterministic PRNG (tempered LCG), below/between/pick/die6 |

## Publish a package

```bash
cd mypackage && catpm pack && catpm publish <clone-of-this-repo>/
git add -A && git commit -m "publish mypackage x.y.z" && git push
```

sha256 integrity: every entry in `index.json` carries the archive hash; catpm
verifies it on every install (cache hits included).

## Layout

```
index.json            package index (path + sha256 + deps per version)
<name>/<name>-<ver>.cpkg   tar.gz archives (index.catc + catpm.json [+ files])
```

Protocol: see [PROTOCOL.md](https://github.com/monikalnbo/catpm/blob/main/PROTOCOL.md)
(four layers: manifest / resolution / packaging / source).
