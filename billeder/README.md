# Billeder

Denne mappe indeholder screenshots og andre billeder, der bruges i wiki-siderne (fx skærmbilleder fra Visual Studio eller JetBrains Rider).

## Navngivning

Brug små bogstaver og bindestreger, samt et emne-præfiks, så det er nemt at se hvor et billede hører til:

```
billeder/rider-debug-eksempel.png
billeder/vs-nuget-manager.png
billeder/csharp-oop-diagram.png
```

## Sådan bruges et billede på en side

Tilføj et almindeligt `<img>`-tag i indholdet, fx i `Rider.html`:

```html
<img src="billeder/rider-debug-eksempel.png" alt="Skærmbillede af debugger i JetBrains Rider" class="screenshot">
```

Tilføj denne CSS til sidens `<style>`-blok (samme mønster som `.callout`, `.command-list` osv.), hvis den ikke allerede er der:

```css
.screenshot {
    max-width: 100%;
    border: 1px solid #e3e3e8;
    border-radius: 8px;
    box-shadow: 0 4px 12px rgba(0,0,0,0.05);
    margin: 20px 0;
    display: block;
}
```

## Klik-for-at-forstørre (lightbox)

Billeder kan gøres klikbare, så de åbner i en forstørret visning med mørk baggrund — uden
JavaScript, kun med et CSS `:target`-trick. Se `Opdateringer.html` for et fungerende eksempel.
Mønsteret er: en `<a href="#unikt-id">` omkring miniaturebilledet, og et skjult
`<a id="unikt-id" class="lightbox-overlay">` med det store billede placeret et sted på siden (fx
lige efter det indhold, der bruger det). CSS'en for `.screenshot` og `.lightbox-overlay` skal være i
sidens `<style>`-blok — kopiér den fra `Opdateringer.html`, hvis den ikke allerede findes på siden.

## Sådan tilføjes et nyt billede

- Læg filen i denne mappe (lokalt, eller upload direkte via GitHub's webgrænseflade).
- Bed Claude om at indsætte det på den rigtige side, eller gør det selv med `<img>`-tagget ovenfor.
