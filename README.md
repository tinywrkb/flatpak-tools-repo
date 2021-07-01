# Flatpak tools repo

Public Flatpak repository, mainaly for distributing flatpak-builder-tools as a Flatpak package.

## Setup

* Add the repository
```
$ flatpak remote-add --if-not-exists flatpak-tools https://github.com/tinywrkb/flatpak-tools-repo/raw/master/flatpak-tools.flatpakrepo
```
* Install flatpak-builder-tools
```
$ flatpak install flatpak-tools io.github.flatpak.flatpak-builder-tools
```

## Usage

### Python pip generator
```
flatpak run \
  --filesystem=$PWD \
  --command=flatpak-pip-generator \
  io.github.flatpak.flatpak-builder-tools \
  --requirements-file=requirements.txt \
  --output python-dependencies
```

### Perl CPAN generator

* Add a `perl-requirements.txt` with some Perl modules in it
```
Net::DBus
X11::Protocol
```
* Create a simple `update-perl-dependencies` script
```
#!/bin/bash

while read -r line; do
  perl_mods+=" $line"
done < perl-requirements.txt

flatpak run \
  --filesystem=$PWD \
  --command=flatpak-cpan-generator.pl \
  io.github.flatpak.flatpak-builder-tools \
  --output perl-dependencies-sources.json \
  $perl_mods
```
