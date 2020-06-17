# pkgbuild

PKGBUILDs for projects that are/were bin-blocked by other AUR maintainers.

[PKGBUILD templates](./.pkgbuild-templates)

## Packaging

### Github releases and the `${pkgname}-${pkgver}.tar.gz::` source format

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
