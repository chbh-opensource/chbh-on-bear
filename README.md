# CHBH-on-BEAR Documentation
<!-- markdownlint-disable -->
<!-- ALL-CONTRIBUTORS-BADGE:START - Do not remove or modify this section -->
[![All Contributors](https://img.shields.io/badge/all_contributors-5-orange.svg?style=flat-square)](#contributors-)
<!-- ALL-CONTRIBUTORS-BADGE:END -->
<!-- markdownlint-restore -->

This documentation describes running CHBH-on-BEAR workflows on the University of Birmingham's BlueBEAR HPC system.

## Contributors

Many thanks to our contributors - please open an issue if you're missing from this list.

<!-- ALL-CONTRIBUTORS-LIST:START - Do not remove or modify this section -->
<!-- prettier-ignore-start -->
<!-- markdownlint-disable -->
<table>
  <tbody>
    <tr>
      <td align="center" valign="top" width="14.28%"><a href="https://gitlab.com/ajquinn"><img src="https://avatars.githubusercontent.com/u/13739055?v=4?s=100" width="100px;" alt="ajquinn"/><br /><sub><b>ajquinn</b></sub></a><br /><a href="#maintenance-ajquinn" title="Maintenance">🚧</a> <a href="#content-ajquinn" title="Content">🖋</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/orbsmiv"><img src="https://avatars.githubusercontent.com/u/19799678?v=4?s=100" width="100px;" alt="James Carpenter"/><br /><sub><b>James Carpenter</b></sub></a><br /><a href="#maintenance-orbsmiv" title="Maintenance">🚧</a> <a href="#content-orbsmiv" title="Content">🖋</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/Bingram22"><img src="https://avatars.githubusercontent.com/u/9869628?v=4?s=100" width="100px;" alt="Brandon Ingram"/><br /><sub><b>Brandon Ingram</b></sub></a><br /><a href="#content-Bingram22" title="Content">🖋</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://sites.google.com/site/arkadykonovalov/"><img src="https://avatars.githubusercontent.com/u/14971990?v=4?s=100" width="100px;" alt="Arkady Konovalov"/><br /><sub><b>Arkady Konovalov</b></sub></a><br /><a href="#content-arkadykonovalov" title="Content">🖋</a></td>
      <td align="center" valign="top" width="14.28%"><a href="https://github.com/benjaminGriffiths"><img src="https://avatars.githubusercontent.com/u/24454976?v=4?s=100" width="100px;" alt="Ben Griffiths"/><br /><sub><b>Ben Griffiths</b></sub></a><br /><a href="#content-benjaminGriffiths" title="Content">🖋</a></td>
    </tr>
  </tbody>
</table>

<!-- markdownlint-restore -->
<!-- prettier-ignore-end -->

<!-- ALL-CONTRIBUTORS-LIST:END -->

## Publishing

The documentation is automatically built and published to <https://ajquinn.github.io/chbh-on-bear> on every push to the `main` branch of this repository.

This is taken care of by the [`deploy` GitHub Actions workflow](https://github.com/AJQuinn/chbh-on-bear/tree/main/.github/workflows/deploy.yml).

## Using `mkdocs`

### Creating a Development Environment and Installing `mkdocs`

To install all the required `mkdocs` Python packages, use the provided [requirements.txt](https://github.com/AJQuinn/chbh-on-bear/tree/main/requirements.txt) file. The recommendation for development is to do this inside a dedicated virtual environment:

```shell
git clone https://github.com/AJQuinn/chbh-on-bear
cd chbh-on-bear
python -m venv ./.venv
source ./.venv/bin/activate
pip install -r requirements.txt
```

### Building

To build the documentation, use:

```shell
mkdocs build
```

### Testing

To test whether the documentation is building correctly, and whether all (internal) links are correct, use:

```shell
mkdocs build --strict
```

This command will exit with a non-zero exit code if `mkdocs` produces any errors or warnings.

### Previewing

To see a local preview of the rendered documentation in your browser, use

```shell
mkdocs serve
```

and click the link that is provided, for example:

```shell
INFO     -  Documentation built in 0.24 seconds
INFO     -  [17:52:07] Watching paths for changes: 'docs', 'mkdocs.yml'
INFO     -  [17:52:07] Serving on http://127.0.0.1:8000/
```

This preview of the rendered documentation will automatically refresh when the documentation sources are updated!
