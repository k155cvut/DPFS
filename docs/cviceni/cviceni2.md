---
icon: material/numeric-2-box
title: Cvičení 2
---

# Vektorová data, prostorové dotazy, prostorové funkce (geoprocessing)

## Cíl cvičení

- Vysvětlení rozdílu mezi vektorovými a rastrovými GIS daty
- Selekce prvků na základě vzájemných prostorových vztahů
- Seznámení se se základními geoprocessingovými nástroji

<hr class="level-1">

## Vektorová a rastrová prostorová data

<div class="grid cards" markdown>

-   :material-vector-polyline:{ .lg .middle } __Vektorová data__

    ---

    Tvořena __vrcholy__ (Vertices) a __cestami__ (Paths) – ty jsou určeny skutečnými souřadnicemi

    Podrobnost je určena __podrobností souřadnic vrcholů__

    Vhodné pro __diskrétně rozložená data__ (např. poloha bodů, kategorie pokrytí půdy)

    Možné problémy s __topologií__ (mezery a překryvy)


-   :material-grid:{ .lg .middle } __Rastrová data__<span style="font-size:60%;font-style:italic;vertical-align:10%;margin-left:15px;color:#888">součástí budoucích cvičení</span>

    ---

    Tvořena pravidelnou mřížkou __pixelů__ – ty jsou určeny pixelovými souřadnicemi (pořadí řádku/sloupce)

    Podrobnost je určena __velikostí pixelu__ (v metrech)

    Vhodné pro jevy měnící se __spojitě__ (např. model terénu, znečištění ovzduší) i __diskrétně__, dále pak __obrazová data__ (např. satelitní)

</div>

<hr class="level-1">

## Prostorové dotazy

__Prostorový dotaz__ (Spatial Query) je metoda výběru/filtrace prvků jedné vrstvy __na základě vzájemné polohy s prvky druhé vrstvy__. Funkce využívá jako vstup `vrstvu vybíraných prvků`, `vrstvu pro překryvnou analýzu` a `vztah pro překryvnou analýzu`.

![](../assets/cviceni2/img_01.svg){ .no-filter }
![](../assets/cviceni2/img_02.svg){ .no-filter }
{: .process_container}

<div class="table_headerless table_small_padding table_centered centered_tab_labels" markdown> <!-- trik: vlastnosti tabulky pro vsechny podrizene -->

=== "Výběr BODŮ..."

    === "...v překrytu s BODY"

        ![](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/GUID-1ECFFABC-3608-4BB4-86A8-FD6FA0F16C13-web.gif){ style="filter:none !important;" }
        {: align=center}

        <table style="width:unset;">
            <tr><td>Intersect</td><td>A</td></tr>
            <tr><td>Intersect (DBMS)</td><td>A</td></tr>
            <tr><td>Contains</td><td>A</td></tr>
            <tr><td>Contains Clementini</td><td>A</td></tr>
            <tr><td>Within</td><td>A</td></tr>
            <tr><td>Within Clementini</td><td>A</td></tr>
            <tr><td>Are identical to</td><td>A</td></tr>
            <tr><td>Have their center in</td><td>A</td></tr>
        </table>

    === "...v překrytu s LINIEMI"

        ![](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/GUID-171AD80E-550B-4017-AEB7-1A681D722F60-web.gif){ style="filter:none !important;" }
        {: align=center}

        <table id="small_table_padding" style="width:unset;">
            <tr><td>Intersect</td><td>A, C</td></tr>
            <tr><td>Intersect (DBMS)</td><td>A, C</td></tr>
            <tr><td>Within</td><td>A, C</td></tr>
            <tr><td>Completely within</td><td>A</td></tr>
            <tr><td>Within Clementini</td><td>A</td></tr>
            <tr><td>Have their center in</td><td>A, C</td></tr>
            <tr><td>Boundary touches</td><td>C</td></tr>
        </table>

    === "...v překrytu s POLYGONY"

        ![](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/GUID-12153063-E9B3-42E5-A786-E3FAF6BB004E-web.gif){ style="filter:none !important;" }
        {: align=center}

        <table id="small_table_padding" style="width:unset;">
          <tr><td>Intersect</td><td>A, C</td></tr>
          <tr><td>Intersect (DBMS)</td><td>A, C</td></tr>
          <tr><td>Within</td><td>A, C</td></tr>
          <tr><td>Completely within</td><td>A</td></tr>
          <tr><td>Within Clementini</td><td>A</td></tr>
          <tr><td>Have their center in</td><td>A, C</td></tr>
          <tr><td>Boundary touches</td><td>C</td></tr>
        </table>

=== "Výběr LINIÍ..."


    === "...v překrytu s BODY"

        ![](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/GUID-FD60FA73-31CD-4BD7-B03C-06806851BC9E-web.gif){ style="filter:none !important;" }
        {: align=center}

        <table id="small_table_padding" style="width:unset;">
          <tr><td>Intersect</td><td>A, C, D</td></tr>
          <tr><td>Intersect (DBMS)</td><td>A, C, D</td></tr>
          <tr><td>Contains</td><td>A, C, D</td></tr>
          <tr><td>Completely contains</td><td>A, D</td></tr>
          <tr><td>Contains Clementini</td><td>A, D</td></tr>
          <tr><td>Have their center in</td><td>D</td></tr>
          <tr><td>Boundary touches</td><td>C</td></tr>
        </table>

    === "...v překrytu s LINIEMI"

        ![](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/GUID-09D6FB47-31A3-47C3-A8B8-19BB659EBA8A-web.gif){ style="filter:none !important;" }
        {: align=center}

        <table id="small_table_padding" style="width:unset;">
          <tr><td>Intersect</td><td>A, C, D, E, F, G, H, I, J</td></tr>
          <tr><td>Intersect (DBMS)</td><td>A, C, D, E, F, G, H, I, J</td></tr>
          <tr><td>Contains</td><td>G, H</td></tr>
          <tr><td>Completely contains</td><td>G</td></tr>
          <tr><td>Contains Clementini</td><td>G, H</td></tr>
          <tr><td>Within</td><td>F, H</td></tr>
          <tr><td>Completely within</td><td>F</td></tr>
          <tr><td>Within Clementini</td><td>F, H</td></tr>
          <tr><td>Are identical to</td><td>H</td></tr>
          <tr><td>Boundary touches</td><td>C, E</td></tr>
          <tr><td>Share a line segment with</td><td>F, G, H, I, J</td></tr>
        </table>

    === "...v překrytu s POLYGONY"

        ![](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/GUID-54663F11-5B47-46A5-82C1-37FD1FDDC835-web.gif){ style="filter:none !important;" }
        {: align=center}

        <table id="small_table_padding" style="width:unset;">
          <tr><td>Intersect</td><td>A, C, D, E, F, G, H, I, J, K, L, M, N, O</td></tr>
          <tr><td>Intersect (DBMS)</td><td>A, C, D, E, F, G, H, I, J, K, L, M, N, O</td></tr>
          <tr><td>Within</td><td>A, D, G, H, I, O</td></tr>
          <tr><td>Completely within</td><td>A</td></tr>
          <tr><td>Within Clementini</td><td>A, D, G, H, I</td></tr>
          <tr><td>Boundary touches</td><td>F, G, H, I, K, L, M, N, O</td></tr>
          <tr><td>Share a line segment with</td><td>G, I, J, K, M, O</td></tr>
          <tr><td>Crossed by the outline of</td><td>C, E, H, L, N</td></tr>
          <tr><td>Have their center in</td><td>A, C, D, E, G, H, I, J, O</td></tr>
        </table>

=== "Výběr POLYGONŮ..."


    === "...v překrytu s BODY"

        ![](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/GUID-0973BB65-5DAE-461A-8B84-E58332CDA443-web.gif){ style="filter:none !important;" }
        {: align=center}

        <table id="small_table_padding" style="width:unset;">
          <tr><td>Intersect</td><td>A, B</td></tr>
          <tr><td>Intersect (DBMS)</td><td>A, B</td></tr>
          <tr><td>Contains</td><td>A, B</td></tr>
          <tr><td>Completely contains</td><td>A</td></tr>
          <tr><td>Contains Clementini</td><td>A</td></tr>
          <tr><td>Have their center in</td><td>A, D</td></tr>
          <tr><td>Boundary touches</td><td>B</td></tr>
        </table>

    === "...v překrytu s LINIEMI"

        ![](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/GUID-EFDE4E93-532E-4D6E-BB29-9BBFC783CEC7-web.gif){ style="filter:none !important;" }
        {: align=center}

        <table id="small_table_padding" style="width:unset;">
          <tr><td>Intersect</td><td>A, C, D, E, F, G, H, I, J, K, L, M, N, O</td></tr>
          <tr><td>Intersect (DBMS)</td><td>A, C, D, E, F, G, H, I, J, K, L, M, N, O</td></tr>
          <tr><td>Contains</td><td>A, D, G, H, I, O</td></tr>
          <tr><td>Completely contains</td><td>A</td></tr>
          <tr><td>Contains Clementini</td><td>A, D, G, H, I</td></tr>
          <tr><td>Boundary touches</td><td>F, G, H, I, K, L, M, N, O</td></tr>
          <tr><td>Share a line segment with</td><td>G, I, J, K, M, O</td></tr>
          <tr><td>Crossed by the outline of</td><td>C, E, H, L, N</td></tr>
          <tr><td>Have their center in</td><td>E, I, L</td></tr>
        </table>

    === "...v překrytu s POLYGONY"

        ![](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/GUID-7802EBC1-8E73-4071-AE12-4445AB1C24B5-web.gif){ style="filter:none !important;" }
        {: align=center}

        <table id="small_table_padding" style="width:unset;">
          <tr><td>Intersect</td><td>A, C, D, E, F, G, H, I, J, K, M</td></tr>
          <tr><td>Intersect (DBMS)</td><td>A, C, D, E, F, G, H, I, J, K, M</td></tr>
          <tr><td>Contains</td><td>C, E, H, M</td></tr>
          <tr><td>Completely contains</td><td>C</td></tr>
          <tr><td>Contains Clementini</td><td>C, E, H, M</td></tr>
          <tr><td>Within</td><td>F, G, H, M</td></tr>
          <tr><td>Completely within</td><td>F</td></tr>
          <tr><td>Within Clementini</td><td>F, G, H, M</td></tr>
          <tr><td>Are identical to</td><td>H, M</td></tr>
          <tr><td>Boundary touches</td><td>D, E, G, H, I, J, M</td></tr>
          <tr><td>Share a line segment with</td><td>D, H, I, M</td></tr>
          <tr><td>Crossed by the outline of</td><td>A, E, G, J, K</td></tr>
          <tr><td>Have their center in</td><td>C, E, F, G, H, K, L</td></tr>
        </table>
        
</div>

<figcaption markdown>zdroj: [Select By Location graphic examples](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/select-by-location-graphical-examples.htm)</figcaption>


[:material-open-in-new: Select features by location](https://pro.arcgis.com/en/pro-app/latest/help/mapping/navigation/select-features-by-location.htm){ .md-button .md-button--primary .button_smaller target="\_blank"}
[:material-open-in-new: Select Layer By Location (Data Management)](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/select-layer-by-location.htm){ .md-button .md-button--primary .button_smaller target="\_blank"}
[:material-open-in-new: Select By Location graphic examples](https://pro.arcgis.com/en/pro-app/latest/tool-reference/data-management/select-by-location-graphical-examples.htm){ .md-button .md-button--primary .button_smaller target="\_blank"}
{: align=center style="display:flex; justify-content:center; align-items:center; column-gap:20px; row-gap:10px; flex-wrap:wrap;"}

<hr class="level-1">

## Úlohy k procvičení

!!! task-fg-color "Úlohy k prostorovým dotazům"

    K řešení následujích úloh použijte datovou sadu [ArcČR
    500](../../data/#arccr-500) verzi 3.3 dostupnou na disku *S* ve složče
    ``K155\Public\data\GIS\ArcCR500 3.3``. Zde také najdete souboru s
    popisem dat ve formátu PDF.

    1. Existuje v ČR letiště, jehož reprezentační bod leží v lese? Jak se jmenuje?

    2. Kolika obcemi v ČR neprochází žádná silnice?

    3. Kolik obcí leží na hranici ČR?

    4. Vyberte silnice, které kříží vodní toky. Kolik procent z těchto
       silnic tvoří silnice první třídy?

    5. Kolik procent rybníků z celkového počtu leží celou svojí plochou na
       území Jihočeského kraje?

    6. Na kolika mapových listech Základní mapy 1:25 000 leží alespoň
       částečně okres Litoměřice. Kolik mapových listů potom leží v tomto
       okresu celou svojí plochou?

    7. Kolik železničních stanic leží v lese a zároveň jejich název
       nezačíná na písmeno 'L'?

    8. Které silnice (uveďte jejich číslo) druhé třídy procházejí oblastí
       bažin a rašelinišť?

    9. Jaká je průměrná nadmořská výška výškových kót na území
       Středočeského kraje?

    10. Kolik vodních ploch leží alespoň částí své plochy ve vzdálenosti
        do 10 km od poledníku se zeměpisnou délkou 15°?

    11. Kolik obcí se dotýká alespoň jedním liniovým segmentem hranice kraje?

    12. Vyberte katastrální území, ve kterých leží alespoň částečně jedna
        vodní plocha, seskupte tyto území podle kódu NUTS (LAU1). Uveďte
        jaký kód NUTS má největší výměru a z kolika katastrálních území se
        skládá?

    13. Uveďte souřadnice reprezentačního bodu (centroidu) největší vodní
        nádrže v Libereckém kraji. O jakou vodní nádrž se jedná?

    14. Kolik obcí leží celou svojí plochou na mapovém listu "Pardubice"
        ZM 1<nowiki>:</nowiki>25 000. Do kolika ORP tyto obce patří a
        které to jsou?

    15. Kolik obcí v ČR leží svoji plochou alespoň na dvou mapových
        listech Základní mapy 1:50 000?

 <hr class="level-1">

## Prostorové funkce (geoprocessing)

## Základní pojmy

- [**buffer**](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/buffer.htm): Vytváří zóny okolo vstupních geografických prvků ve specifikované vzdálenosti. Tyto zóny mohou být využity například k analýze vlivu určitého objektu na své okolí.
- [**clip**](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/clip.htm): Vyřezává část jednoho datasetu na základě hranic jiného. Výsledkem je nový dataset obsahující pouze oblasti uvnitř klipu.
- [**select**](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/select.htm): Umožňuje vybrat prvky z datasetu, které splňují zadané podmínky, například atributové dotazy nebo prostorové kritérium.
- [**intersect**](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/intersect.htm): Kombinuje dvě nebo více vstupních vrstev a vytváří nové prvky v místech, kde se jejich geometrie překrývají.
- [**dissolve**](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/dissolve.htm): Agreguje prvky podle specifického atributu, čímž redukuje počet prvků a vytváří větší jednotky (např. sloučení polygonů stejného typu).
- [**spatial join**](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/spatial-join.htm): Kombinuje atributy dvou geografických vrstev na základě jejich prostorového vztahu (např. připojení údajů bodů k blízkým polygonům).
- [**erase**](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/erase.htm): Odstraňuje části jedné vrstvy, které se překrývají s druhou vstupní vrstvou, a ponechává zbytek geometrie.
- [**union**](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/union.htm): Kombinuje geometrie a atributy dvou nebo více vrstev do nové vrstvy. Výsledkem jsou oblasti, které reprezentují kombinaci všech vstupů.
- [**remove overlap**](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/remove-overlap-multiple.htm): Identifikuje a odstraňuje překrývající se oblasti mezi prvky v jedné vrstvě nebo mezi více vrstvami.
- [**symmetrical difference**](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/symmetrical-difference.htm): Vytváří novou vrstvu obsahující prvky, které jsou v jedné nebo druhé vstupní vrstvě, ale ne v jejich překryvu.
- [**count overlapping features**](https://pro.arcgis.com/en/pro-app/latest/tool-reference/analysis/count-overlapping-features.htm): Počítá počet prvků, které se překrývají, a výsledek ukládá do nové vrstvy nebo atributové tabulky.

<hr class="level-1">

Následující přehled ukazuje nejpoužívanější nástroje prostorových funkcí v ArcGIS Pro.

<figure markdown>
  ![Prostorové funkce](../assets/cviceni3/prost_funkce_srovnani.png "Prostorové funkce")
  <figcaption>Srovnání vstupních vrstev a výsledků operace pro různé nástroje prostorových funkcí</figcaption>
</figure>

<hr class="level-1">

## Úlohy k procvičení

!!! task-fg-color "Úlohy"

    K řešení **následujích** úloh použijte datovou sadu [ArcČR
    500](../../data/#arccr-500) verzi 3.3 dostupnou na disku *S* ve složče
    ``K155\Public\data\GIS\ArcCR500 3.3``. Zde také **najdete** souboru s
    popisem dat ve formátu PDF.

    1. Jaká je výměra (v ha) bažin a rašelinišť ležících v lese. Kolik to
       je procent z celkové výměry bažin a rašelinišť?
       
    2. Jaká je výměra (v km^2^) území omezeného pouze na ČR do 100 m od dálnic?

    3. Kolik obcí v ČR leží celou svojí plochou do vzdálenosti 10 km od
       řeky Labe. Jaký je celkový počet obyvatel těchto obcí?

    4. Na kolika místech kříží dálnice, rychlostní silnice či silnice
       1.třídy s železnicí. Kolik z těchto křížení leží do vzdálenosti 1km
       od nejbližší železniční stanice?

    5. Jaká je výměra území (v ha), na kterých leží les či vodní
       plocha. Existuje území, které by odpovídalo současně oběma
       podmínkám?

    6. Vytvořte společnou datovou vrstvu pro letiště a železniční
       stanice. Kolik objektů tato vrstva obsahuje?

    7. Kolik procent z celkové výměry ČR činí uzemí, která jsou vzdálená
       od nejbližšího rybníku více než 25 km?

    8. Jaká je výměra uzemí ČR (v km^2^), která leží dále než 5 km od
       nejbližší silnice a zároveň dále než 10 km od nejbližší železniční
       stanice? Na území kterých obcí leží největší z hledaných lokalit?

    9. Kolik procent území Jihočeského kraje tvoří vodní plochy?

<hr class="level-1">

## Úloha: Pobočky pošty

Představte si, že pracujete jako GIS analytik pro Českou poštu a vaším úkolem je z důvodu úspor navrhnout řešení snížení počtu poboček. Snahou tohoto kroku je však i minimalizace negativních dopadů na obyvatele, proto bylo rozhodnuto o následujících podmínkách, které musíte ve svém návrhu dodržet:

1. Rušení poboček nebude probíhat v obcích s méně než 2500 obyvateli.
2. V obcích nad 2500 obyvatel neklesne počet poboček pod 1.
3. Vzájemná vzdálenost poboček v jedné obci nebude nižší než 3 km vzdušnou čarou.

Jakou finanční úsporu jste schopni svým návrhem zajistit, pokud by provoz jedné pobočky vycházel ročně na 2,5 milionu CZK? Pro zjednodušení budete úlohu řešit pouze v rámci Plzeňského kraje a ke každé pobočce přistupovat rovnocenně.

## Použité datové podklady

- [Pobočky](../assets/cviceni3/PobockyCP_PlzenskyKraj.zip) České pošty v Plzeňském kraji (bodová vrstva)
- Obce ČR ([ArcČR 500](../../data/#arccr-500), polygonová vrstva)

## Pracovní postup

**1.** Výběr obcí v Plzeňském kraji s více než 2500 obyvateli (atributový dotaz) a tvorba samostatné vrstvy selektovaných prvků.

<figure markdown>
  ![Select](../assets/cviceni3/SELECT_obce.png "Select obce")
  <figcaption>Atributový dotaz na vrstvu obcí</figcaption>
</figure>

**2.** Výběr typu pobočky zavedením *Definition Query* (výraz: ZKRNAZ_DRU = 'pošta').

<figure markdown>
  ![DQ](../assets/cviceni3/DQ_posta.png "Definition Query pošty")
  <figcaption>Definition Query pro vrstvu poboček pošty</figcaption>
</figure>

<figure markdown>
  ![Map 1](../assets/cviceni3/MAP_pred-spatial-join.png "Mapa 1")
  <figcaption>Vizualizace stavu nad podkladovou mapou</figcaption>
</figure>

**3.** Spatial join: k výběru obcí připojíme pobočky na základě jejich polohy. Zároveň přidáme nový atribut POCET_POBOCEK, který bude určen na základě sumy libovolného ze stávajících atributů vrstvy poboček (např. count(GmIID)).

<figure markdown>
  ![Spatial join](../assets/cviceni3/SPATIALJOIN_obce-pobocky.png "Spatial join")
  <figcaption>Spatial join</figcaption>
</figure>

**4**. Následně zadáme atributový dotaz na vrstvu obcí, který vybere prvky s více než 1 pobočkou (POCET_POBOCEK *is greater than* 1).

<figure markdown>
  ![Select by attribute](../assets/cviceni3/SELECT_pocet-pobocek.png "Atributový dotaz")
  <figcaption>Atributový dotaz na vrstvu obcí</figcaption>
</figure>

**5**. V dalším kroku použijeme nástroj *CLIP* a vytvoříme novou vrstvu obsahující takové pobočky pošty, které se nacházejí v obcích s více než 1 pobočkou. Tím, že v předchozím kroku byla provedena selekce pouze některých prvků z vrstvy obcí, do funkce *CLIP* vstoupí pouze tento aktivní výběr.

<figure markdown>
  ![Clip features](../assets/cviceni3/CLIP_pobocky.png "Clip")
  <figcaption>Oříznutí vrstvy poboček aktivními prvky ve vrstvě obcí.</figcaption>
</figure>

<figure markdown>
  ![Map 2](../assets/cviceni3/MAP_spatial-join-plus-dq.png "Mapa 2")
  <figcaption>Vizualizace stavu po ořezu.</figcaption>
</figure>

**6**. S využitím nástroje *BUFFER* vytvoříme obalovou zónu kolem každé pobočky o poloměru 3 km.

<figure markdown>
  ![Buffer](../assets/cviceni3/BUFFER_pobocky.png "Buffer")
  <figcaption>Parametry nástroje BUFFER pro tvorbu obalové zóny (rádius 3 km)</figcaption>
</figure>

**7**. Nyní přistoupíme k vizuálnímu vyhodnocení poboček vhodných ke zrušení. Např. v Klatovech lze při dodržení zadaných kritérií zrušit právě 2 pobočky České pošty (zvýrazněné včetně svých obalových zón), resp. zachovat maximálně 2 pobočky (viz níže).

<figure markdown>
  ![Map 3](../assets/cviceni3/MAP_buffer-Klatovy.png "Mapa 3"){ width="500" }
  <figcaption>Příklad poboček aspirujících na zrušení</figcaption>
</figure>

**8**. V atributové tabulce poboček vytvoříme pomocí *Add Field* pomocný atribut RUSENO (datový typ *short*, defaultní hodnota 0).

<figure markdown>
  ![Add field](../assets/cviceni3/AT_add-field.png "Přidání atributu")
  <figcaption>Přidání nového pole do atributové tabulky</figcaption>
</figure>

**9**. Manuálně vybereme (pomocí *Select*) pobočky vyhovující kritériím zrušení změnou hodnoty atributu RUSENO na 1.

**10**. Nyní je možné zobrazit rušené pobočky zavedením *Definition Query* (výraz RUSENO = 1) nebo naopak pobočky splňující podmínky, aby byly zachovány (výraz RUSENO = 0).

<figure markdown>
  ![Map 4](../assets/cviceni3/MAP_zachovane-pobocky.png "Mapa poboček")
  <figcaption>Pobočky pošty, kterou mohou být zachovány.</figcaption>
</figure>

**11**. Závěrem lze porovnat, jak rušení poboček České pošty v r. 2023 skutečně proběhlo; přehled naleznete např. [zde](https://www.seznamzpravy.cz/clanek/fakta-ceska-posta-zrusene-pobocky-seznam-mapa-231064). Celý problém je samozřejmě složitější, jelikož finální výběr ovlivnily další faktory jako priorita pobočky (hlavní vs. vedlejší), bezbariérovost, apod.

<hr class="level-1">

## Úloha: Kulturní míle

*Pracovní postup:*

1.  Stáhněte si prostorová data (z OSM přes BBBike): Vyberte ohraničení kolem vaší univerzity (cca 2 km^2^), vyplňte formát, jméno a mail a stiskněte *Extract*. Odkaz na stažení vám bude zaslán na vaši e-mailovou adresu, jakmile bude proces online extrakce hotový.

2.  Načtěte a vyberte data v aplikaci ArcGIS Pro: Do mapy importujte shapefile *points.shp*. Prozkoumejte atributovou tabulku, zejména pole *type*. Najděte a vyberte bod představující vaši univerzitu.

3.  Prostorová analýza (část 1): Po výběru bodu (vaší univerzity) vytvořte pomocí geoprocessingového nástroje *Buffer* (metoda *planar*) kolem tohoto bodu obalovou zónu o velikosti 1 míle. Funkce zpracuje pouze 1 obalovou zónu kolem vybraného bodu, pokud je výběr aktivní.

4.  Atributový dotaz: Proveďte *Select by Attributes* a vyhledejte body související s kulturou pomocí atributu *typ* (vyhledávání divadel, muzeí atd.). Vyberte všechny prvky v nejméně 5 různých kategoriích kultury a extrahujte tato data do geodatabáze projektu.

5.  Prostorová analýza (část 2): Pomocí nástroje *Clip* extrahujte body (vrstva prvků obsahující pouze kulturní místa) v rámci mílové obalové zóny.

6.  V této fázi byste měli mít kolem univerzity  zónu o velikosti 1 míle obsahující body zájmu související s kultury. Všechny ostatní prvky můžete z mapy odstranit.

7.  Najděte vhodné symboly pro jednotlivé typy kulturních zařízení.

8.  Vložte nový layout (*Insert Layout*) ve vybraném formátu a zvolte orientaci na šířku nebo na výšku.

9.  Ve vlastnostech mapy nastavte vhodné referenční měřítko a případně omezte obsahu mapového okna pouze na obalovou zónu.

10. Dokončete rozvržení: vložte mapové okno, přidejte nadpis, podnadpis, legendu a tiráž. Níže inspirace.

<figure markdown>
  ![Mapa](../assets/cviceni3/culturemile.png "Mapa"){ width=600px }
  <figcaption>Výsledná vizualizace</figcaption>
</figure>

<br><br><br><br><br>
