# Doughnut Chart

## Formål

At omsætte en værdi i HTML til en visuel statistik med SVG, custom properties og typed `attr()`. Du skal forbinde tallet, ringens længde og en markør, så de reagerer på samme `data-value`.

## Ressourcer

- [MDN: SVG circle](https://developer.mozilla.org/en-US/docs/Web/SVG/Reference/Element/circle)
- [MDN: pathLength](https://developer.mozilla.org/en-US/docs/Web/SVG/Reference/Attribute/pathLength)
- [MDN: attr()](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Values/attr)
- [MDN: stroke-dasharray](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/stroke-dasharray)
- [MDN: stroke-dashoffset](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/stroke-dashoffset)
- [MDN: offset-path](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/offset-path)
- [MDN: offset-distance](https://developer.mozilla.org/en-US/docs/Web/CSS/Reference/Properties/offset-distance)

## Opgavebeskrivelse

Du får tre statistikker: **Consistency (85%)**, **Improvement (95%)** og **Branching (90%)**. Hver statistik har en `figure` med et `data-value`, en SVG og en billedtekst. Det er tre uafhængige procentværdier, ikke dele af en fælles sum på 100%.

Det færdige resultat skal vise en lys grå ring med en sort bue, der starter øverst og går med uret. Værdien står i midten, og en rød markør sidder ved buens slutning. Statistikken har sin label nedenunder. Alle tre figurer skal bruge de samme CSS-regler.

Starteren viser hele sorte ringe og værdier i billedteksterne. Det er med vilje: forbindelsen fra data til grafik er din opgave.

Projektet er almindelig HTML og CSS. Åbn `index.html` i browseren, eller brug Live Server.

Arbejd i `style.css`, og følg TODO-markeringerne.

### 1. Én værdi, tre typer

Læs `data-value` på `figure` med `attr()` som:

- `--value-string`: tekst til tallet i midten.
- `--value-number`: et tal til beregningen af buens længde.
- `--value-percent`: en procent til markørens position.

Behold værdierne lokalt på hver `figure`, så dens SVG-elementer kan arve dem. Du skal ikke skrive særskilte regler for 85, 95 og 90.

### 2. Fra cirkel til bue

SVG'en har et koordinatsystem på `100 × 100`. Sporet og buen har centrum i `(50, 50)` og radius `46`.

`pathLength="100"` normaliserer buens længde til 100 enheder, så du kan arbejde direkte med tal mellem 0 og 100 uden at beregne cirklens omkreds.

- Brug `stroke-dasharray` til at lave en streg, der dækker én omgang.
- Brug `stroke-dashoffset` til at skjule den del, der mangler op til 100. Hvor meget skal skjules ved værdien 85?
- Drej SVG'en, så starten ligger klokken 12.

**Hint:** Brug tal uden procenttegn til dash-egenskaberne. Procenter her måles ikke langs cirklens omkreds. Du kan afprøve `100.1` som dash-længde, som i undervisningseksemplet, for at undgå en lille samling ved en hel omgang.

### 3. Tallet i midten

Læg SVG'en og `figure::after` i det samme grid-område. Lad `figcaption` ligge under diagrammet.

Vis `--value-string` gennem `content`, og lad tallets størrelse følge figurens bredde med `30cqw`. Husk en inline-size-container på `figure`, så enheden har den rigtige reference.

### 4. Markøren følger værdien

Giv `.marker` en cirkulær `offset-path` med samme radius og centrum som ringen. Brug `--value-percent` som `offset-distance`, og gør markøren synlig.

Her er procenten netop en position langs stien. Kontrollér, at markøren følger buens slutning, når du ændrer værdien.

## Specifikke mål

- Forstå forskellen på en attribut læst som tekst, tal og procent.
- Bruge lokale custom properties til at forbinde flere dele af samme figur.
- Bruge `pathLength`, `stroke-dasharray` og `stroke-dashoffset` til at vise en værdi.
- Placere en markør med `offset-path` og `offset-distance`.
- Kombinere SVG, pseudo-elementer og containerenheder uden JavaScript.
- Bevare statistik som læsbar tekst ved siden af den visuelle fremstilling.

## Afprøv din løsning

- Test 0, 25, 50, 75 og 100. Markøren skal følge den forventede position rundt om ringen.
- Ved 0 kan runde stregender give en lille prik. Overvej at skjule `.progress` ved `data-value="0"`.
- Test en smal skærm og en længere label. Figurerne skal kunne wrappe uden vandret overflow.
- Kopiér en figur, og giv den en ny værdi. Den skal virke uden nye CSS-regler.
- Opdatér også teksten i `figcaption`, når du ændrer `data-value`: i denne statiske HTML-udgave står værdien begge steder.
- Slå CSS fra. Kan du stadig læse de tre statistikker?

> [!NOTE]
> Branchen inkluderer et CSS Reset via `resources/starter.css`. Typed `attr()` kræver browserunderstøttelse; se kompatibilitet i MDN-linket. Hvis ringen ikke reagerer, så test i en opdateret browser med understøttelse.

## Ekstra udfordring (valgfri)

Tilføj et fjerde kort, og afprøv fx `62.5`. Forklar, hvorfor både stregen og markøren kan følge samme værdi, selv om de bruger forskellige typer.

## Aflevering

Find linket til din løsning på Netlify, og aflever det på Fronter.

Link-struktur: **doughnut-chart--**[Dit unikke netlify link].netlify.app/
