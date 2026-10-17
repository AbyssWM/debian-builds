# Abyss Debian builds

Experimental Debian source-package definitions for all 17 Abyss repositories.
Native sbuild/dpkg-buildpackage builds, lintian checks and installation tests are
**not yet validated**. This repository is not part of Debian's official archive.

`packages/NAME/debian/` contains control files, rules, source format and packaging
patches. Shared libraries use ABI-named binary packages and separate development
packages. Build dependency names were checked against Debian unstable's official
amd64 package index. Required versions must still be checked for the chosen release.

Prepare a source tree and deterministic orig archive:

```sh
python3 tools/prepare-source.py abyssutils --out out/abyssutils
```

The helper verifies each pinned source archive against `sources.json` before
extraction. The compositor adds the separately checksummed Glaze source under
`.deps/` and compiles its public default config. Target series are intentionally
`UNRELEASED`: choose a supported Debian release and verify its full dependency
set before building/signing or publishing. Use native dpkg-buildpackage/sbuild;
the assembly helper alone does not produce a validated .deb or signed upload.

No APT repository, signing key, Debian account or archive submission has been
created. LMDE compatibility depends on its actual Debian base and separate tests.

Maintainer: bb8TheRobot <bb8therobot85@gmail.com>. Packaging: 0BSD.
Original source license texts are retained in the copyright files. The upstream
attribution audit and packaging-policy review remain release prerequisites.

License scope and the retained upstream notices are described in [LICENSES.md](LICENSES.md).
