# Was ist Butler

Butler ist eine Haushaltsapp zum Anzeigen der Einnahmen und Ausgaben.

## Was soll Butler können?

1. Es sollen Kategorien und Fixkosten ersichtlich sein.
2. Es sollen Intervalle und Start-Enddaten möglich sein. Es soll aber auch ohne Enddatum möglich sein.
3. Der Startscreen soll die Übersicht des aktuellen Monats sein. Insgesamt wird es fües erste nur 3 Screens geben (Detailansicht, Jahresübersicht und ein Screen zum Anlegen bzw bearbeiten eines Eintrages)
4. Einträge ohne Enddatum sollen bis X Jahre wiederholt werden.
5. Beim Ändern eines Eintrages soll es eine Auswahl geben ob alle betroffenen Einträge (vergangen, aktuell, zukünftig) angepasst werden sollen oder gelöscht oder ob nur der aktuelle Eintrag angepasst werden soll. Mehr dazu später.
6. Ausgaben sollen sortiert nach Fixkosten> Kategorie> Betrag angezeigt werden.
7. Beim ersten App Start erscheint ein Tutorial

### Zukunftsideen:

1. Daten auf Cloud/Google Drive etc. Aktuell: vasern DB lokal
2. Schuldenmanager
3. Sparmanager
4. Kontoverknüpfung
5. Kassenzettel einlesen

# Design

1. Darkmode und Lightmode
2. Landscape + Portrait

## Verwendendete Frameworks

1. NativeBase 3.0 | https://docs.nativebase.io/
2. DatePicker | https://github.com/react-native-datetimepicker/datetimepicker
3. Picker | https://github.com/react-native-picker/picker
4. SVG Charts | https://github.com/JesperLekland/react-native-svg-charts
5. Icons | https://ionic.io/ionicons

# Problemstellung:

1.  Verhalten bei Enddatum => leer
    Einträge können mit Start und/oder Enddatum angelegt werden. Wie soll das Handling für Einträge ohne
    festen Endtermin gestaltet werden?
    **Option 1:**
    Es werden automatisch Einträge für die nächsten
    ✗ Jahre generiert.

    **Option 2:**
    Bei Klick auf ein neues Jahr werden die Einträge angelegt

    > wird nur einmalig, jedoch für jedes Jahr durchgeführt
    > der Nutzer muss vor der Anzeige kurz warten.

    **Option 3:**
    Bei Appstart wird für die nächsten ✗ Jahre aktualisiert.

    > Längere Appstartphase, jedoch keine Wartezeit

        beim Jahreswechsel

    **Idee:**
    Kombination aus Opt 1- 3.
    Neuer Eintrag > Es werden alle Einträge für ✗ Jahre angelegt.

    Bei Jahresauswahl über ✗ werden erst die Daten
    generiert.

    Bei Appstart werden die Einträge aktualisiert.

    **Lösung:**
    Für den Anfang wird nur Option 1 beachtet, X entspricht hier 12 Monate

2.  Einträge als Haupteinträge oder einzelne Einträge
    Dieses Problem steht in Kombination zu Problem 1.

    **Option 1:**
    Es wird ein Haupteintrag mit den Eckdaten angelegt und dazu die Einzelnen Einträge für die Monate

    > höhere Datenlast in DB aber schnelleres anzuges
    > der Einträge

    **Option 2:**
    Es wird nur der Haupteintrag angelegt und für jeden Monat angezeigt.

    > geringere Datenlast aber auch geringere Performance

    **Lösung:**
    Option 1 bietet höhere Performance.

3.  Anzeige Übersicht
    Auf kleinen Geräten kann kein ganzes Jahr dargestellt werden. Hier müssen weniger Details angezeigt werden.

**Was sind die wichtigen Infos in der Übersicht?**
Einnahmen, Ausgaben, Rest
Darstellung als Balken. Mit Klick ⇒ ausklappen
↳ Progressbar
Button ⇒ mehr> Detailansicht

4. Intelligentes Bearbeiten

Beispieleintrag:
Ausgaben Miete von Jan 2021 bis
Dezember 2022 monatlich 690€

    Im Mai 2021 erhöht der User den Betrag
    auf 720€

**Was soll passieren?**

Die App soll abfragen ob dies nur einmalig (Mai 2021) für alle (Januar 21 - Dezember 22) oder für alle zukünftigen
(Mai 21-Dezember 22) passieren soll.
Wählt der Nutzer nun zB. Letzteres soll die App abfragen
ob alles andere gelöscht oder beibehalten wird.
Dies wird in einen Screen dargestellt.
