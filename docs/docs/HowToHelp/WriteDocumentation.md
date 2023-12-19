# Write Documentation

This project houses the FreeTakServer (FTS) documentation.
It is written in Markdown and mkdirs.

## Procedure

### Fork the Main Repository

You will need a `github` account.

Fork https://github.com/FreeTAKTeam/FreeTAKServer-User-Docs into your own account.
Clone your forked repository onto your development environment.

It will probably be useful to have two remotes,
one (upstream) for merging in upstream commits,
and one (origin) for your forked repository.

### Discuss on the FreeTAK Forum

FTS provides a Discord server where we can provide a consistent experience,
free from kindergarten dramas and with a lot of sense of humor
(keep in mind our tagline – "The parrot's not dead! It’s just resting").
You can join the FTS Discord Server here: https://discord.gg/m8cBzQM2te.
While Discord is cool for live interaction, it can be very inconsistent.
The forum is organized thematically, where it’s easier to stay on topic.
This will include a knowledge library of problems and solutions.
While other places may exist were enthusiast discuss our software,
the new platform is what we, the developers, will actively support.


### Make Changes

See Documentation Patterns below.


### Verify Processing

#### GitHub Action

The documentation is built via GitHub actions.
Here is the `.github/workflows/main.yml` action:
```yaml
{!../../../.github/workflows/main.yml!}
```
name
: The name of the workflow

on push branches main
: The event and branch which triggers this workflow

jobs deploy steps run
: Install dependencies and build the target


### Make a Pull Request (PR)

Once you are satisfied with your changes make a GitHub pull request.

Announce your PR on the discord `Development / doc-dev` channel.
(You have been discussing your changes there, right?)

Any changes you make to the branch associated with
the PR will be included until it is approved and merged.

## Working Locally

While you will ultimately verify your work as outlined above,
it will probably be useful to work locally.

### Dependencies

Here are the packages it uses:
These packages are available for `conda`.

```shell
mamba env create -y -f docs/docs/HowToHelp/fts-doc-env.yml
```
This environment includes the packages needed to construct the document products.
```yaml
{!HowToHelp/fts-doc-env.yml!}
```

### Preview Document

Start a service to view the resulting document.
```shell
mkdocs serve
```

## Documentation Patterns

### Mkdocs and Material Theme

The markdown files are coordinated and supplemented by `mkdocs` and its plugins.
Some of the more important features of those plugins are presented here.

`mkdocs` is configured via the `mkdocs.yml` file.

### Awesome Pages

Each document directory should contain a `.pages`.
These `.pages` distribute the `nav:` element across the document rather than collecting them in the `mkdocs.yml` file.
This implies that `mkdocs.yml` should not contain a `nav:` element.

### Markdown Includes

This file contains a typical example.
The `fts-doc-env.yml` file mentioned above is itself included using this facility.

i.e.  
\```yml  
{\!HowToHelp/fts-doc-env.yml\!}  
\```

### Mike (multi-version support)

The `fts_user/docs/versions.json` is used to define the versions.

TODO: Explain how this is to be used.
