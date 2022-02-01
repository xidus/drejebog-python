
# Python: Udvikler-opsætning og bruger-igangsætning

Modtager: En ny Python-programmør

## Formål

At have en Python-pakke, der kan bruges som eksempel på mappe-struktur med funktionel dokumentation, kildekode, tests, scripts, konfigurationer, samt automatisk, central test af kodebasen.

Hvad er en god mappestruktur?

*   Konventionen for Python-pakker og anden software. (`src`-layout)

Hvad er en god måde at dokumentere sit software-projekt på?

*   En god README-fil
*   Versionsstyret dokumentation:
    -   Dokumentation som skrives samtidig og gemmes sideløbende med den versionsstyrede kode.
    -   Dokumentation, som bygges automatisk, når en ny version af koden/dokumentationen kommer.


Hvad er kode-arkivets formål?

*   Understøt videreudvikling af programmel. Understøt softwareudvikling.
    -   Automatisk, central test af kodebasen.
    -   Én sandhed: den centrale udviklingsservers testresultater af den samlede kodebases hovedgren(e). -> Continuous Integration (CI)
    -   Udviklervendt dokumentation, der overordnet set fremtidssikrer kodebasen.
        +   Gamle udviklere/vedligeholdere husker, hvad procedurerne er.
        +   Nye udviklere/vedligeholdere lærer, hvad procedurerne er.
        +   Spørgsmål, udviklervendt dokumentationen kan besvare:
            *   Hvordan komemer jeg igang med at udvikle? (Opsætning, så kan teste lokalt, samt hente den rigtige version af koden, e.g. ved flere grene)
*   Understøt brugeren med vejledning og lyt til ændringsønsker
    -   Installationsvejledning
    -   Konkrete brugseksempler
    -   Tilbagemelding: proces.

```

```

## Inden du bygger: Start med formål og behov

Hvad skal vi bygge?

Du er ansat til at lave genbrugelig kode, der hjælper brugeren med at løse sine egne opgaver bedre, nemmere, hurtigere, etc.

Som udvikler har du ansvaret for, du selv kan arbejde effektivt med koden, samt at andre nemt kan arbejde videre med projektet.

Brugeren har ansvaret for at give dig en klar forståelse af det grundlæggende problem, som koden skal løse.

Samspillet mellem bruger og udvikler:

Med din viden om mulige veje, man kan gå med design og byg af koden, har du ansvaret for, at bygge det efter bedste praksis, men også efter tid og egne evner, hvilket i praksis sætter grænser for, hvad brugeren kan ønske sig. Ofte skal brugeren bare hjælpes til at forstå sin egen problemstilling ud fra det softwareudviklingsmæssige perspektiv. Andre gange må man indse, at virkeligheden er kompleks, og derfor bliver løsningen også i en vis grad dérefter.

### Eksempel

Slutprodukt: README.md

*   Projektbeskrivelse
*   Brugsscenarier
*   Evt. anvendelse

#### Projektbeskrivelse

Ønske:

> Jeg er træt af at regne ting ud i hånden med papir og blyant. Jeg vil have et program og klikke på et vindue, hvor jeg får en videnskabelig lommeregner frem, som jeg kan taste data ind, der skal kunne foretage elementære regneoperationer, måske også regne en vinkel i en trekant med tre kendte sidelængder.

Mulig omformulering:

> Som måler skal jeg nemt kunne addere, subtrahere og multiplicere tal, så jeg ikke længere skal gøre det i hånden.

Ovenstående nævnr ikke en grafisk brugergrænseflade, men brugeren kan godt noget med kommandolinjeværktøjer, så det er rimeligt, at vi starter med en applikation, der har kernefunktionaliteten og anvendes gennem en terminal. Vi kan udvide senere.


## Til udvikleren

Vi starter her, fordi software-udvikleren skal have nogle byggematerialer.


### Python-installation

Vi bruger MambaForge, der gør to ting nemmere for os:

*   Pakkestyringsværktøjet `mamba` er hurtigere end `conda`.
*   MambaForge bruger som standard kun det kuraterede pakke-arkiv `conda-forge`, som blandt andet giver os nogle bedre licensbetingelser, når vi bruger pakkerne herfra i vores egne løsninger.

**Installation**

*   Alle seneste versioner: https://github.com/conda-forge/miniforge/releases/latest
    -   Windows: Vælg `Mambaforge-Windows-x86_64.exe`
*   Direkte link til seneste Windows-version: https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-Windows-x86_64.exe

![Illustration af laptop med Python, MambaForge, GitHub, ]

### Opret kodearkiv (GitHub repository)

På GitHub

*   Log ind
*   Opret nyt arkiv
    -   [x] Opret README
    -   [x] Opret `.gitignore`
    -   [x] Opret LICENSE
*   Kopiér link til kodearkivet

På lokal PC:

*   Gå til en mappe, hvor du har git-kode

    ```
    > cd sti\til\git
    sti\til\git>
    ```

*   Klon arkivet

    ```
    sti\til\git> git clone git@github.com:xidus/kalk.git
    ```

*   Tilgå mappen

    ```
    sti\til\git> cd kalk
    sti\til\git\kalk>
    ```

### Dokumentation: README

*   Skriv en ordentlig README

    *   HUSK: Din README-fil læses ikke nødvendigvis på GitHub, så hav links, der peger tilbage til kilden (her Github).

Gem version.

Skub lokale ændringer til GitHub.

Se ændringerne træde i kraft på GitHub


### Klargør miljøet

Opret dev-miljø

```
> mamba create -n kalk-dev
> mamba activate kalk-dev
```

### Test: opsætning

Pytest-installation

```
> mamba install -y pytest
> mamba env export > environment-dev.yml
> git add environment.yml
> git commit -m "Tilføj mamba environment."
```

Kør pytest


### Test: Opret tests

```
kalk> mkdir tests
kalk> cd tests
kalk/tests> touch test_operations.py
```


```python
# test_operations.py
import kalk


def test_sum():
    a, b = 1, 2
    expected = 3
    result = kalk.sum(a, b)
    assert result == expected, f'Expected {result!r} to be {expected!r}'

```

Kør pytest

-> Fejl ... Vi mangler at installere `kalk`. Hvordan gør man dét?

```
kalk> touch setup.py
kalk> mkdir src
kalk> cd src
kalk/src> mkdir kalk
kalk/src/kalk> touch __init__.py version.py
```

```python
# version.py
version = '1.0.1'
```

```python
# setup.py
import os
from setuptools import (
    setup,
    find_packages,
)

with open(os.path.join('src', 'kalk', 'version.py')) as f:
    exec(f.read())


setup(
    name="kalk",
    version=__version__,
    description="Kalkulator for your sums, substractions and multiplications.",
    url="https://github.com/xidus/kalk",
    author="Joachim Mortensen",
    author_email="xidus@github.com",
    license="BSD-3",

    packages=find_packages(where='src'),
    package_dir={'': 'src'},
)
```

Terminal

```
(kalk-dev) kalk> python -m pip install -e .
```

Kør pytest

```
(kalk-dev) kalk> pytest
```

-> Fejl

### Kode: Byg kernefunktionalitet

Pytest fejler, fordi `kalk` ikke har nogen funktionalitet endnu.

Tilføj koden:

```python
"""
Kalkulator for your sums, substractions and multiplications.

"""

from typing import (
    Union,
    Iterable,
)
import builtins


_sum = builtins.sum


ArgumentType = Union[int, float]
ResultType = Union[int, float]


def sum(*args: Iterable[ArgumentType]) -> ResultType:
    """
    Returnerer summen af de givne argumenter.

    """
    return _sum(args)


def sub(*args: Iterable[ArgumentType]) -> ResultType:
    """
    Returnerer differencen mellem det første argument og de efterfølgende argumenter.

    """
    first, *remainders = args
    return first - sum(*remainders)


def mul(*args: Iterable[ArgumentType]) -> ResultType:
    """
    Returnerer produktet af de givne argumenter.

    """
    product = 1
    for factor in args:
        product *= factor
    return product

```

Kør Pytest igen

-> Skulle gerne virke nu.

Gem arbejdet.

### Kode: Byg brugergrænsefladen

Brugeren skal kunne tilgå pakkens funktionalitet fra kommandolinjen på følgende måder:

```sh
(kalk) $ kalk sum 1 2 3 4
10
(kalk) $ kalk sub 1 2 3 4
-9
(kalk) $ kalk mul 1 2 3 4
24
```

Dét implementerer vi med et tredjeparts-modul kaldet [`click`](https://palletsprojects.com/p/click/).

Installér click med Mamba

```
(kalk-dev) kalk> mamba install -y click
```

Tilføj click til vores afhængigheder i miljøfilen:

```yaml
# environment-dev.yml
name: kalk-dev
channels:
  - conda-forge
  - defaults
dependencies:
  - click
  - pytest
```

Opret et ny modul, der afhænger af vores kernemodul (lige nu kaldet `__init__.py`, men det kunne hedde andre ting.)

```python
# cli.py
"""
Kommandolinje-modul til Kalkulator

"""

from typing import Iterable

import click

import kalk


@click.command()
@click.argument('operation', type=str)
@click.argument('arguments', nargs=-1, required=True, type=float)
def main(operation: str, arguments: float):
    do = getattr(kalk, operation)
    result = do(*arguments)
    click.echo(result)

```

For at få kommandoen `kalk` installeret, skal vi rette i installationsprogrammet `setup.py`:

```python
# setup.py
import os
from setuptools import (
    setup,
    find_packages,
)

with open(os.path.join('src', 'kalk', 'version.py')) as f:
    exec(f.read())


setup(
    name="kalk",
    version=__version__,
    description="Kalkulator for your sums, substractions and multiplications.",
    url="https://github.com/xidus/kalk",
    author="Joachim Mortensen",
    author_email="xidus@github.com",
    license="BSD-3",

    packages=find_packages(where='src'),
    package_dir={'': 'src'},

    entry_points={
        'console_scripts': [
            'kalk = kalk.cli:main',
        ],
    },
)
```

Og lad os tilføje lidt mere dokumentation til brugeren (`cli.md`)

Gem de nye og rettede filer lokalt i Git.

```
git add ...
```

Skub ændringer til GitHub.

```
git push
```

### Kode: Miljø-opsætning til brugeren

Kopiér `environment-dev.yml` til `environment.yml` og gør følgende:

*   Fjern de pakker, som brugeren ikke behøver at installere.
*   Fjern `-dev` fra navnet, så der kun står `kalk`, så det passer med installationsvejledningen til brugeren.

```yaml
# environment.yml
name: kalk
channels:
  - conda-forge
  - defaults
dependencies:
  - click

```

Gem i Git

Skub til Github



## Dokumentation: Til brugeren

Skriv mere dokumentation, gerne i form af eksempler, som brugeren kan anvende med det samme for at få nogle resultater.

Opret en mappe til resten af projektets dokumentationen, herunder specifikke vejledninger og eksempler.

    ```
    kalk> mkdir docs
    ```

Skriv eventuelt uddybende dokumentation.


### Dokumentation: Sæt dokumentationsværktøjet op.

Installér `mkdocs-material`.

Tilføj pakken i `environment-dev.yml`

Tilføj filen `mkdocs.yml`

```yaml
# mkdocs.yml
# Project information
site_name: Kalkulator
site_description: 
site_author: Joachim Mortensen
docs_dir: docs/

# Repository
repo_name: kalk
repo_url: https://github.com/xidus/kalk

# Configuration
theme:
  name: material
  language: da
  palette:
    primary: green
    accent: green

# Plugins
plugins:
- search

# Navigation
nav:
- Introduktion: index.md
- Installation: installation.md
- CLI: cli.md
- API: api.md
```

Test dokumentationen lokalt med følgende kommando:

```
mkdocs serve
```

Gå til `localhost:8000` i browseren.

Ret eventuelt i dokumentations-indholdet.

Gem og se ændringerne opdateres live i browseren.

Gem ænderingerne i Git.

Skukb ændringerne til GitHub.

### Automatik: GitHub workflow til automatisk test



---



## Terminologi

*   Version:
    -   Kodeversion: En given version af koden. Eksempel: Et Git-commits SHA1-hash
    -   Udgivelsesversion: Et løbenummer på software, der markerer en distribueret løsning/pakke/applikation, som er færdig og udgør en forbedring af de tidligere udgivelser, enten ved at have løst fejl (*en* bugs) eller ved at introducere ny funktionalitet, og som i kraft heraf erstatter de tidligere softwareversioner. Eksempel: MS Windows 3.11 erstattede Windows 3.1.

## Appendiks

### Windows Terminal Preview


### busybox


## Kilder

*   Daniel D. Beck, Write the Readable README, [README Checklist](https://github.com/ddbeck/readme-checklist) | [video](https://www.youtube.com/watch?v=2dAK42B7qtw)
