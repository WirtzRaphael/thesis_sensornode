# Changelog

## Revision C
### Entscheide

### Anpassungen
*Generell*
- Schema Top Übersicht überarbeitet
- Power Ports sind nun global gültig.
- Die Versorgungsspannungen wurden mit Farben gekennzeichnet und dem Power Diagramm abgeglichen.
- MCU Schema auf A3
- Neue Nummerieriung (Annotation)
- Einheitliche Bezeichnung der Versorgungsspannungen (3V3, 3V3-1, 3V3-2) und verwenden von Netzklassen (Altium Parameter Set Symbol).

*Power Schema*

- Kontrolllogik *Power Control* zum schalten der Hauptversorgung der MCU hinzugefügt. P-Kanal FET an Ausgang von RTC, wegen Open-Collector Ausgang.
- Charger IC für Ni-MH Beschaltung für 2000mAh Akku 3S1P mit 1/10C Ladestrom.
- DC/DC 3V3 immer aktiv.
- Stiftleisten am Ausgang der DC/DC Wandler und Lastschalter platziert. Ermöglicht Strommessungen und Einsetzten von externen Spannungsversorgungen (Backup).
- Power Source mittels Schottky Dioden, FET entfernt.
- Load Switch Modell ersetzt mit TPS22919DCKR
  - Geringer Ruhestrom
  - Mehr Maximalstrom als TPS22860DBVR

*Komponenten & Signale*

- Radio UART Verbindung angepasst (RX, TX, Flow Control)
- Digitale Isolatoren bei Verbindungen der MCU
  - Zwischen den Spannungsebenen 3V3 und der unterliegenden, gesteuerten 3V3-1.
- Schema Symbol für Flash aktualisiert
- LED's und Vorwiderstände definiert.

## Revision B
Änderungen basieren im wesentlichen auf
- Komponentenauswahl und deren Verfügbarkeit.
- Anpassung auf Ni-MH Akkumulatoren.
- Rückmeldungen von Erich Styger.

### Entscheide
- Kein Reset Button
- Batterien (3xAAA) nicht auf PCB. Dies benötigt zu viel Platz und deckt zu viel Fläche ab.
- Hauptschalter in Serie zur Batterie und nicht auf PCB
- USB als Energiequelle anstelle von Batterie, wenn angeschlossen.

### Anpassungen
*Komponenten & Signale*

- Crystal für MCU (Y300) mit integrierten Kondensatoren und Position verschoben.
- Charger BQ25172DSGR[^1] für NiMH Akkus.
- USB-C Modell USB4105 (J800)
- Energieversorgung über USB-C, wenn angeschlossen.
  - MOSFET (Q200) zum Deaktivieren der Batterie.
  - Schotky Diode (D201) zum Einkoppeln der USB-C Versorgung.
- DC/DC Wandler (U203) 3V3 TPS63802DLAR
- Ausgangs-Kondensatoren bei den Load Switches. Werte ein Zehntel der Eingangs-Kapazität.
- WAKEUP Signal für Power Management
  - GPIO von MCU
  - Button von I/Os
- RS-232 MAX3221 (U700)
    - Power Management via Signale FORCEON, FORCEOFF über MCU.
    - Enable Eingang zum de-, aktiveren von RX.
    - SSOP Bauform ohne zusätzliche GND Fläche, Pin entfernt.
    
*Generell*

- I/Os, also Buttons und LEDs auf separates Schema verschoben.
- Nicht benutzte Pins markiert
- Bemerkungen zu Schaltungsfunktionen hinzugefügt
- Schema Seite 'power' auf zweite Seite.

[^1]: [ti.com BQ25172DSGR](https://www.ti.com/lit/ds/symlink/bq25172.pdf?ts=1713164591620&ref_url=https%253A%252F%252Fwww.ti.com%252Fproduct%252FBQ25172)


## Backlog
- Kontrolle von den DC/DC Modi Light & Heavy
- Logik um die Spannungsversorgung VCC1-1 zu steuern.
  - Interrupt von RTC
  - Haltemechanismus zwischen Interrupt von RTC und Signal von MCU.
  - Signal von MCU
