---
title: INTERLIS VALIDIERUNG IN QGIS
description: INTERLIS VALIDIERUNG IN QGIS
customTheme: stylesheets/collab-theme
transition: none
revealOptions: {
  transition: 'none',
  slideNumber: false,
  overview: true,
  autoPlayMedia: true,
}
---

# INTERLIS VALIDIERUNG IN QGIS
### Möglichkeiten und Ideen

---

<!-- Oli's stage -->

## Wer wir sind

### Oliver Grimm @ [Geowerkstatt](https://www.geowerkstatt.ch/) 

### Dave Signer @ [OPENGIS.ch](https://www.opengis.ch/) 

<aside class="notes">
Wir arbeiten in Schweizer Softwarebuden, die sich beide den Open Source Lösungen im GIS Bereich verschrieben haben.
</aside>

---

## Thema

<!-- Dave's stage -->

- INTERLIS setzt **valide** Daten voraus
- Daten können in QGIS **geflickt** werden
- ...

<aside class="notes">
In diesem Talk möchten wir euch folgendes näher bringen... 
- Ein Hauptpfeiler des INTERLIS Ansatzes ist, dass die Daten <b>harmonisch</b> und <b>valide</b> sind.
</aside>


---

<!-- Dave's stage -->

## INTERLIS Validierung in QGIS

<video controls="controls">
<source src="assets/validator.mp4" type="video/mp4">
</video>

<aside class="notes">
In dem letzten zwei Jahren wurde der ilivalidator quasi vollintegriert in QGIS Model Baker.
Das heisst, die Daten müssen nicht exportiert werden, sondern werden direkt im QGIS validiert.

<b>Video:</b>
- Die Datenquelle wird automatisch erkannt
- Man kann die Daten anhand von Modell / Dataset / Behälter EINGRENZEN
- Man kann auch ein Konfigurationsfile übergeben werden, dass mittels Meta Attributen einzelne <b>Checks ausschalten</b> kann oder Constraints mit besseren <b>Fehlermeldungen</b> beschreiben kann.
- Die Resultate erscheinen in einer Liste, man kann sie durchgehen und wie in der <b>Attributtabelle</b> navigieren.
- Man kann dann das <b>Formular öffnen</b>
- Man kann dann zu den <b>Koordinaten zoomen</b> und mit den vorhandenen Tools die Geometrie "flicken".
</aside>

---

<!-- Oli's stage -->

## Was passiert im Backend?
<aside class="notes">
... das war nun das Frontend im Model Baker Plugin, doch was passiert im Hintergrund?
</aside>

---

<!-- Dave's stage -->

## Ideen

  - Mächtigere **QGIS Tools**
  - **Vollintegration** der Constraints
  - ...
  - Live (**Subset**) Validierung 

<aside class="notes">
Es gibt einige Ideen, wie man das nun <b>noch besser</b> machen könnte.

QGIS Tools so zu verbessern: ZBs. der Topologiechecker - ersetzt aber INTERLIS Check nicht.

Integration der Constraints (herauslesen aus INTERLIS Compiler)

Problem, dass grosse Datensätze immer ganz validiert werden müssen. Es gibt die Möglichkeit von Behälter etc. aber die Daten können nicht immer einfach separiert werden. Deshalb die Idee der Subset validierung.

</aside>

---

## PoC Live Validierung 🎥

<!-- Oli's stage -->

---

## Model Baker Frontend
</br>

#### Übergeben einer Selektion
![selection](assets/validate-selection.png)

#### Aufzeichnung einer Session
![recordoids](assets/record-oids.png)

<aside class="notes">
Es gibt mehrere Ansätze, wie dies in Model Baker integriert werden könnte. Sie <b>schliessen sich nicht aus</b>.

1. Übergeben der OIDs aller selektierten Features. Auch möglich "Selektierte Features des aktuellen Layers"
<b>Pros</b>
- Straightforeward und leicht verständliche Lösung.
- Kann auch als Validierung des Layers (wenn alles selektiert ist) benutzt werden.

<b>Cons</b>
- Man muss den Überblick über alle Selektionen behalten. Man muss evtl. durch alle Layer gehen und die Selektion überprüfen. Vielleicht wär auch noch eine Option "Deselect all on all layers" hilfreich.
- Auch erfasst man vielleicht Features auf Kind-Layer, die dann mühsam zu finden sind für die Selektion. Ein automatisches Ermitteln und Hinzufügen von referenzierten Features aber kann zu Loops und grossen Datenmengen führen, weshalb darauf verzichtet wird.

2. Aufzeichnung aller Features, die geändert wurden (ihre OIDs) - könnte auch automatisch starten.

<b>Pros</b>
- Es braucht keine manuelle Selektion.
- Man behält die OIDs der geänderten Features über mehrere "Speicherungen".

<b>Cons</b>
- Komplexität / Verständlichkeit / Neue Komponente (Maintanance etc.)

</aside>

---

## Model Baker Zusatzfunktion

#### Ermitteln der Nachbarn
![neighbours](assets/collect-neighbours.png)

<aside class="notes">
Sofern die Features Geometrien haben, sollen auch die OIDs der Nachbars-Features ermittelt und übergeben werden.

Je nach Menge muss auf die Performance geachtet werden. Evtl. braucht es einen zusätzlichen Panel: "Collect neighbours" -> wenn man sieht es geht viel zu lange, soll man auch abbrechen können.
</aside>

---

## Fragen?
<br>

#### Web: www.geowerkstatt.ch / www.opengis.ch
#### Emails: oliver.grimm@geowerkstatt.ch / david@opengis.ch 
#### Social: @GrimmOliver / @signedav@techhub.social
