# Debian Packaging Recipes (`distro/packages/`)

This directory contains Debian packaging metadata (`debian/control`, `debian/rules`, `debian/changelog`) used to package custom Sagar OS software from `src/` into standard `.deb` packages.

## Structure & Purpose
- Maintains clean separation: source code lives in `src/`, while distribution packaging metadata is tracked here.
- Enables building native Debian packages for:
  - `sagar-core`
  - `sagar-libraries`
  - `sagar-graphics`
  - `sagar-desktop`
  - `sagar-services`
  - `sagar-apps`
