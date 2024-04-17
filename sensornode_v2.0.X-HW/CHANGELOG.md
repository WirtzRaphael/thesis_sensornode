# Changelog

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
