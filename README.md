
# Python: Udvikler-opsætning og bruger-igangsætning

## Formål

### Formålet med dette dokument

At have en drejebog til intern instruktion i organisationens praksis.


### Formålet med instruktionen

At have gjort det klart for Python-programmører i organisationen, hvordan vi forventer, at koden skal struktureres, testes, dokumenteres, produceres og distribueres.

Det er antaget, at modtageren af dét, der bliver formidlet her, har basalt kendskab til Python, versionsstyringsværktøjet Git, samt platformen GitHub.


### Formålet med slutproduktet af instruktionen

Slutproduktet er dét materiale, der bliver udarbejdet under instruktionen og består i et versionsstyret filarkiv tilgængeligt på GitHub.

Formålet med dette er at have en Python-pakke, der kan bruges som eksempel på mappe-struktur med funktionel dokumentation, kildekode, tests, scripts, konfigurationer, samt automatisk, central test af kodebasen.

Det centrale spørgsmål, der bliver svaret på er følgende:

*   Hvad er minimumskravene til et projekts kodebase [kodearkiv, repositorium, *en.* repository, *en.* repo].

Specifikt illustrerer instruktionen og slutproduktet (med dets versionshistorik) både tankegang bag og struktur for et projekts kode, som gør det muligt for ophavspersonen, nye udviklere og ikke mindst brugeren/modtageren af det udførte arbejde at bruge det.


## Spørgsmål og svar

### Hvilket problem skal koden løse?

*   Hvis ikke dette er klart fra begyndelsen, så er der ikke noget grundlag for at skrive koden.


### Hvad er kode-arkivets formål i sig selv?

*   Alle relevante filer er samlet ét sted.
    -   også alle tidligere versioner af koden (versionsstyring og versionering) (versionshistorik).

*   Understøt videreudvikling og brug af programmel/kode/software (fremtidssikring).
    -   Udviklervendt dokumentation.

*   Understøt brugeren med vejledning og lyt til ændringsønsker
    -   Installationsvejledning
    -   Konkrete brugseksempler
    -   Vejled om tilbagemeldingsproces, eksempelvis i form af GitHub issues.


### Hvad er en god mappestruktur?

Budskab: Mappen med kodearkivet er roden til dit projekt. Alt skal med, og rod-mappen skal versionsstyres.

*   Konventionen for Python-pakker og anden software. (`src`-layout)


### Hvad er en god måde at dokumentere sit software-projekt på?

*   En god README-fil
*   Versionsstyret dokumentation:
    -   Dokumentation som skrives samtidig og gemmes sideløbende med den versionsstyrede kode.
    -   Dokumentation, som bygges automatisk, når en ny version af koden/dokumentationen kommer.


### Hvordan er sammenspillet mellem API og test?

Nøgleord: Refaktorisering, teknisk gæld

*   Refaktorisering: Alle (enheds)tests tester én ting. De er den første grund til at refaktorisere.


## Inden du bygger: Start med formål og behov

### Hvad skal vi bygge?

Du er ansat til at lave genbrugelig kode, der hjælper brugeren med at løse sine egne opgaver bedre, nemmere, hurtigere, etc.

Som udvikler har du ansvaret for, du selv kan arbejde effektivt med koden, samt at andre nemt kan arbejde videre med projektet.

Brugeren har ansvaret for at give dig en klar forståelse af det grundlæggende problem, som koden skal løse.

Samspillet mellem bruger og udvikler er altså væsentligt: Med din viden om mulige veje, man kan gå med design og byg af koden, har du ansvaret for, at bygge det efter bedste praksis, men også efter tid og egne evner, hvilket i praksis sætter grænser for, hvad brugeren kan ønske sig. Ofte skal brugeren bare hjælpes til at forstå sin egen problemstilling ud fra det softwareudviklingsmæssige perspektiv. Andre gange må man indse, at virkeligheden er kompleks, og derfor bliver løsningen også i en vis grad dérefter.

Det er med andre ord vigtigt at starte med en grundig afdækning af følgende:

*   Hvem er brugeren/aktøren? Rolle og ansvar.
*   Hvad er brugerens egen tekniske formåen?
*   Hvad er brugerens grundlæggende behov?
*   Hvad er minimumslravene til, at brugeren får opfyldt sine behov?
    -   Hvilke krav er unødvendige, irrelevante eller uden betydning?

### Eksempel

Slutprodukt: README.md

*   Projektbeskrivelse
*   Brugsscenarier
*   Evt. anvendelse

#### Projektbeskrivelse

Ønske:

> Jeg er træt af at regne ting ud i hånden med papir og blyant. Jeg vil have en Android-applikation, hvor jeg kan taste data ind, der skal kunne foretage elementære regneoperationer, måske også regne en vinkel i en trekant i ny og næ.

Mulig omformulering:

> Kommandolinieprogram til elementære regneoperationer:
> 
> * Som **måler** skal jeg kunne **addere, subtrahere og multiplicere tal**, så jeg **ikke længere skal gøre det i hånden**.
> 

Brugeren arbejder typisk med kommandolinjeværktøjer, så vi starter med en applikation, der har kernefunktionaliteten og anvendes gennem en terminal.

Bygger vi applikationen fornuftigt op, kan vi nemt udvide senere med andre grænseflader end en kommandolinje-funktion.

### Konklusion

Start med at beskrive (og dermed tænke over) funktionalitet og brugergrænseflade, inden du skriver noget kode.

Det kan tage relativt tid, men som regel ikke i forhold til at lave ændringer undervejs, fordi brugerens behov ikke har været klare fra begyndelsen.


## Som udvikler

Vi starter her, fordi software-udvikleren skal have nogle byggematerialer.

Som udvikler har du to primære modtagere:

*   dig selv og andre udviklere på projektet
*   brugeren / modtageren.

I kodebasen ligger der filer, som understøtter alt arbejde med kode, dokumentation, etc. For brugeren er kun produktet og den brugervendte dokumentation relevant.

I eksemplet, vi bygger op her, beder vi brugeren om at hente kodearkivet ned med Git. Her skal brugeren først checke koden ud og dernæst manuelt oprette et miljø og installere de pakker (Afhængigheder), som vores program skal bruge. Python er forudsat installeret hos brugeren, og det er antaget, at brugeren kan bruge det.

Man kan i ovenstående tilfælde distribuere koden til et pakke-arkiv som the Python Package Index (PyPI). For brugeren ville det derfor være væsentligt lettere at installere pakken i et arbitrært mamba-miljø.

Der kan være flere grunde til, at vi ikke distribuerer koden til et (globalt) Python-pakke-arkiv. Én årsag kan være, at vi kan have brug for, at brugeren tester en specifik version af koden, hvilket er nemt, hvis brugeren bare skal checke den givne version ud kortvarigt.


### Krav: Vores valg af Python-distrbution

Vi bruger Mamba Forge, der gør to ting nemmere for os:

*   Pakkestyringsværktøjet `mamba` er hurtigere end `conda`.
*   MambaForge bruger som standard kun det kuraterede pakke-arkiv `conda-forge`, som blandt andet giver os nogle bedre licensbetingelser, når vi bruger pakkerne herfra i vores egne løsninger.

**Installation**

*   Alle seneste versioner: https://github.com/conda-forge/miniforge/releases/latest
    -   Windows: Vælg `Mambaforge-Windows-x86_64.exe`
*   Direkte link til seneste Windows-version: https://github.com/conda-forge/miniforge/releases/latest/download/Mambaforge-Windows-x86_64.exe


### Krav: GitHub repository

Vi bruger GitHub til central versionsstyring og udviklingsserver. Herfra kan andre i organisationen læse/hente/dele kode. Platformen har også mulighed for automatisk at kvalitetssikre koden, når nye versioner bliver lagt op (skubbet), og vi kan nemt styre diskussioner, ændringsforslag og kodegennemgange fra ét og samme sted.

**Skridt**

På GitHub

*   Log ind
*   Opret nyt arkiv
    -   [x] Opret standard README-fil
    -   [x] Opret `.gitignore`
    -   [x] Opret LICENSE
*   Kopiér link til kodearkivet

På din lokale PC:

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

### Krav: Dokumentation: README

Skriv altid en ordentlig README

*   HUSK: Din README-fil læses ikke nødvendigvis på GitHub, så hav links, der peger tilbage til kilden (her Github).

Her er et eksempel:

```
<!-- README.md -->

# [Kalkulator](https://github.com/xidus/kalk)

Af [Joachim](https://github.com/xidus)

Kalkulator er et kommandolinjeprogram, der hjælper brugeren med at lave de elementære regneoperationer.

## Installation

Forudsætninger:

*   Som bruger har du allerede conda eller [mamba](https://github.com/conda-forge/miniforge/) installeret.

For at komme igang med at bruge programmet, skal du have Python installeret og dernæst installere programmet fra kommandolinjen:

    (base) $ git clone https://github.com/xidus/kalk
    (base) $ cd kalk
    (base) $ git checkout 1.0.1
    (base) $ mamba env create -f environment.yml
    (base) $ mamba activate kalk

    (kalk) $ python -m pip install -e .
    (kalk) $


## Kommandolinje-eksempler

Nu kan programmet anvendes på følgende måde:

**Sum**

    (kalk) $ kalk sum 1 2 3 4
    10

**Subtraktion**

    (kalk) $ kalk sub 1 2 3 4
    -8

**Multiplikation**

    (kalk) $ kalk mul 1 2 3 4
    24


---

## Bidrag

*   Fejl og ønsker kan oprettes som [GitHub issues](https://github.com/xidus/kalk/issues) på kodens adresse.
*   Kodeforslag kan oprettes gennem GitHubs forking- og pull-request-mekanisme:
    -   På kodearkivets side, vælg Fork
    -   Fra din egen fork, lav en by branch og foretag rettelserne i denne.
    -   Når du er klar, kan du oprette et pull-request fra den nye branch.

*   Andet? Se kontaktoplysninger nedenfor.

---

## Kontakt

*   Udvikler: <udvikler@example.com>
*   Kontor: <kontor@example.com>

```

*   Gem version.
*   Skub lokale ændringer til GitHub.
*   Se ændringerne træde i kraft på GitHub


### Klargør miljøet

*   Opret dev-miljø

```
> mamba create -n kalk-dev
> mamba activate kalk-dev
```

### Krav: Test: opsætning

*   Installér Pytest

```
> mamba install -y pytest
> mamba env export > environment-dev.yml
> git add environment.yml
> git commit -m "Tilføj mamba environment."
```

*   Kør pytest
    -   -> Pytest finder ingen tests

### Krav: Test: Opret tests

*   Opret mappe til tests

    ```
    kalk> mkdir tests
    kalk> cd tests
    kalk/tests> touch test_operations.py
    ```

*   Opret test-funktionalitet.
    -   Her tænker vi lidt over, hvordan pakkens API skal se ud.

    ```python
    # test_operations.py
    import kalk
    
    
    def test_sum():
        a, b = 1, 2
        expected = 3
        result = kalk.sum(a, b)
        assert result == expected, f'Expected {result!r} to be {expected!r}'
    
    ```

*   Kør pytest
    -   -> Fejl ... Vi mangler at installere `kalk`. Hvordan gør man dét?

*   Opret installationsprogram (`setup.py`) og lav en mappe til kildekoden (`__init__.py` og `version.py`):

    ```
    kalk> touch setup.py
    kalk> mkdir src
    kalk> cd src
    kalk/src> mkdir kalk
    kalk/src/kalk> touch __init__.py version.py
    ```

*   Tilføj dén version, vi arbejder på:

    ```python
    # version.py
    __version__ = '1.0.1'
    ```

*   Lav en relativt minimal installations-opsætning:

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

*   Installér pakken lokalt med flaget `-e` sat, så kode, der afhænger af pakken, bruger dét, der ligger i kodearkivet (og ikke en kopi gemt undet installationen).

    ```
    (kalk-dev) kalk> python -m pip install -e .
    ```

*   Kør pytest igen

    ```
    (kalk-dev) kalk> pytest
    ```

    -   -> Fejl: Vi mangler kernefunktionaliteten. Lad os skrive den.


### Krav: Kode: Byg uafhængig kernefunktionalitet

Pytest fejler, fordi `kalk` ikke har nogen funktionalitet endnu.

*   Tilføj koden:

    ```python
    # __init__.py
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

*   Kør Pytest igen
    -   -> Skulle gerne virke nu.

*   Gem arbejdet i Git.

*   Skub ændringerne til GitHub.


### Kode: Byg brugergrænseflade oven på kernefunktionalitet

Som nævnt skal brugeren kunne tilgå pakkens funktionalitet fra kommandolinjen på følgende måder:

```sh
kalk sum 1 2 3 4
10

kalk sub 1 2 3 4
-8

kalk mul 1 2 3 4
24
```

Dét implementerer vi med et tredjeparts-modul kaldet [`click`](https://palletsprojects.com/p/click/).

*   Installér click med Mamba

    ```
    (kalk-dev) kalk> mamba install -y click
    ```

*   Tilføj click til vores afhængigheder i miljøfilen:

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

*   Opret et ny modul, der afhænger af vores kernemodul (lige nu kaldet `__init__.py`, men det kunne hedde andre ting.)

    ```python
    # cli.py
    """
    Kommandolinje-modul til Kalkulator
    
    """
    
    import click
    
    import kalk
    
    
    @click.command()
    @click.argument('operation', type=str)
    @click.argument('arguments', nargs=-1, required=True, type=float)
    def main(operation: str, arguments: float):
        do = getattr(kalk, operation)
        result = do(*arguments)
        click.echo(result)
    

    # ---
    def alternative(operation: str, arguments: float):
        do = getattr(kalk, operation)
        result = do(*arguments)
        click.echo(result)


    arg_operation = click.argument('operation', type=str)
    arg_arguments = click.argument('arguments', nargs=-1, required=True, type=float)
    alternative = arg_arguments(alternative)
    alternative = arg_operation(alternative)
    alternative = click.command(alternative)
    # Then add alternative to entry points in setup.py

    
    # ---
    import sys
        
    def basic():
        assert len(sys.argv) > 3, f'Must have at least an operation and two numbers'
        operation, *arguments = sys.argv
        function = getattr(kalk, operation)
        numbers = [float(a) for a in arguments]
        print(function(numbers))


    if __name__ == '__main__':
        basic()


    ```

For at få kommandoen `kalk` installeret, skal vi rette i installationsprogrammet `setup.py`:

*   Udnyt `setuptools`s automatik til at lave en eksekvérbar kommando, når man installerer pakken:

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
    
        entry_points={                          # <==
            'console_scripts': [                # <==
                'kalk = kalk.cli:main',         # <==
            ],                                  # <==
        },                                      # <==
    )
    ```

*   Gem de nye og rettede filer lokalt i Git.

*   Skub ændringer til GitHub.


### Krav: Brugervendt installations-funktionalitet: Miljø-opsætning til brugeren

Som nævnt skal brugeren i dette scenarium selv hente koden med Git og installere afhængighederne og programmet.

*   Kopiér `environment-dev.yml` til `environment.yml` og gør følgende:
    -   Fjern de pakker, som brugeren ikke behøver at installere.
    -   Fjern `-dev` fra navnet, så der kun står `kalk`, så det passer med installationsvejledningen til brugeren.

    ```yaml
    # environment.yml
    name: kalk
    channels:
    - conda-forge
    - defaults
    dependencies:
    - click
    ```

*   Gem i Git
*   Skub til Github

---


## Hvis der er tid

```
kalk> mkdir docs
kalk> mamba install -y mkdocs-material
kalk> touch mkdocs.yml
kalk> mkdocs serve
```

Og

```
kalk> mkdir -p .github/workflows
kalk> touch .github/workflows/main.yaml
```

---

## Terminologi

*   Version:
    -   Kodeversion: En given version af koden. Eksempel: Et Git-commits SHA1-hash
    -   Udgivelsesversion: Et løbenummer på software, der markerer en distribueret løsning/pakke/applikation, som er færdig og udgør en forbedring af de tidligere udgivelser, enten ved at have løst fejl (*en* bugs) eller ved at introducere ny funktionalitet, og som i kraft heraf erstatter de tidligere softwareversioner. Eksempel: MS Windows 3.11 erstattede Windows 3.1.


## Referencer

*   Daniel D. Beck, Write the Readable README, [README Checklist](https://github.com/ddbeck/readme-checklist) | [video](https://www.youtube.com/watch?v=2dAK42B7qtw)
