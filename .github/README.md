# NAME

OverPAN-p5-patches - CPAN community patches for OverPAN

# DESCRIPTION

This GitHub repository contains a list of custom patches.

[OverPAN](https://github.com/next-cpan/OverPAN) provides the tools to create/edit these patches but also a mechanism to apply them during one installation.

You can use the customized [cpanminus client](https://raw.githubusercontent.com/next-cpan/cpanminus/overpan/App-cpanminus/cpanm) to install distributions with custom patches.

# HOW TO

## Install OverPAN

In order to create/edit patches, you first need to install [OverPAN](https://github.com/next-cpan/OverPAN)

```sh
git clone https://github.com/next-cpan/OverPAN.git
cd OverPAN
cpanm --installdeps --with-develop .
perl Makefile.PL
make
make test
make install
```

## Create / Update / Remove patches

In order to create/edit patches, you first need to install [OverPAN](https://github.com/next-cpan/OverPAN). (view section above)

OverPAN provides one `overpan` command line tool which can be used to edit patches.

```sh
# make sure you have a clone of existing OverPAN-p5-patches
git clone https://github.com/next-cpan/OverPAN-p5-patches
cd OverPAN-p5-patches

# create a patch for a distribution
overpan Simple::Accessor
# or use the distro name
overpan Simple-Accessor
# or set a custom version to patch [use the last one released as default]
overpan Simple-Accessor-1.12

# switch to a new Shell session in a Git repository
# where you can add/remove patches
# use git to create/edit patches

# then run
overpan commit
# to generate the updated patches

# note you can abort the existing session by either running 'exit' or
overpan abort
```

New patches are created in a directory like `S/Simple-Accessor/1.12`.
You then have to commit these new patches before submitting a Pull Request.

```sh
git add S/Simple-Accessor/1.12
git commit -m "Update patches for Simple-Accessor-1.12"
```

## Use custom cpanminus

This [GitHub Repository](https://github.com/next-cpan/cpanminus/tree/overpan) contains one experimental `overpan` branch where `OverPAN` is used if installed.

By default `OverPAN` is an opt-in option.

Which means if `OverPAN` is installed on your system it's going to try to use it to patch distributions.

You can disable `OverPAN` if needed using the `--no-overpan` option.
```sh
# use custom OverPAN patches if OverPAN is installed
cpanm Simple::Accessor
# do not use OverPAN patches
cpanm --no-overpan Simple::Accessor
```

You can also use a customize location for the patches to use using `--overpan-source=somewhere`

Samples:
```sh
cpanm --overpan-source=https://github.com/next-cpan/OverPAN-p5-patches Simple::Accessor
cpanm --overpan-source=/usr/local/OverPAN-p5-patches Simple::Accessor
```

# Permitted patches for 1.0

The only patches allowed at this stage are patches which address build/test/install issues related to changes to perl over the years.

Examples:

- `@INC` changes
- sort keys
- strict/warnings/features
- Module::Install problems.

If the module is passing on Perl7, no reasons to submit additional patches (maybe some exceptions).

## Patches should be submitted upstream

Ideally each patch submitted should be reported upstream.
A GitHub workflow could automatically submit patches upstream
and track previously tickets to keep them up to date.

# LICENSE

All contribution to this repository are performed under the Artistic License.

