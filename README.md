# pkgbuild

- [Packaging](#packaging)
  - [Github and the `${pkgname}-${pkgver}.tar.gz::` source format](#github-and-the-pkgname-pkgvertargz-source-format)
  - [Commit id from Git source archives](#commit-id-from-git-source-archives)

## Packaging

### Github and the `${pkgname}-${pkgver}.tar.gz::` source format

Github supports the URL pattern `/org/project/archive/v1.2.3/project-v1.2.3.tar.gz`

Which means you can change `source` from this:

```bash
source=("${pkgname}-${pkgver}.tar.gz::${url}/archive/v${pkgver}.tar.gz")
```

to this:

```bash
source=("${url}/archive/v${pkgver}/${pkgname}-v${pkgver}.tar.gz")
```

**Credits to:**

- anthraxx @ [[aur-general] TU application: hashworks](https://lists.archlinux.org/pipermail/aur-general/2020-June/035805.html)

### Commit id from Git source archives

Archives created by [`git archive`](https://git-scm.com/docs/git-archive)
include the commit id. This applies to Github, Gitlab and most other Git
repository platforms. This comes in handy when the commit id is required for
building an application. Cloning the whole repository for the sole purpose of
having the commit id can take a very long time and a require lots of space,
and adjusting the commit id in the `PKGBUILD` on version-bumps can be easily forgotten.

Retrieve it from the archive using `bsdcat` and [`git get-tar-commit-id`](https://git-scm.com/docs/git-get-tar-commit-id).

```bash
makedepends=('git')
# ...

build() {
  # inside $srcdir
  _commit="$(bsdcat "${pkgname}-${pkgver}.tar.gz" | git get-tar-commit-id)"
  # _commit=b04f3df3c9a1e04a5e5c2b6065aea46ecd557bfe

  go build -ldflags "-X main.commit=${_commit}"
}
```
