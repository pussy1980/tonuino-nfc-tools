# Readme

Android app to write and read NFC tags that can be used on the [TonUINO DIY music box](https://tonuino.de/).

The app will be released on the [play store](https://play.google.com/store/apps/details?id=de.mw136.tonuino) 
and [f-droid](https://gitlab.com/fdroid/fdroiddata/blob/master/CONTRIBUTING.md) 
once it is considered stable.

## TODO

- Add English translation
- Hide on-screen-keyboard when switching between edit fragments
- Add entry "unknown <#>" to mode spinner on EditSimple fragment
- Add support for Tonuino 2.1
- Add support for futher NFC tag technologies
- Simulate NFC tag
- Use proper Material design theming instead of faking it
    - MainActivity if NFC is not available
- Use data binding



## Tonuino 2.0.x
[Repository](https://github.com/xfjx/TonUINO/blob/d15df6c7bb53bc970e4def43fd3e93fd82c13086/Tonuino.ino)

### Daten

| # | name | range | description |
| --- | --- | --- | --- |
| 0 | cookie | uint32 | Identifiziert Tonuino, erwartet `0x1337b347` |
| 4 | version | uint8 | immer 1 |
| 5 | folder | uint8 | Werte von 1 bis 99, siehe [dfplayer doku](https://wiki.dfrobot.com/DFPlayer_Mini_SKU_DFR0299#target_1)  |
| 6 | mode | uint8 | Werte von 1 bis 5, siehe nächste Tabelle |
| 7 | special | uint8 | |


**Verschiedene Modi**  
Basierend auf dem Wert von *mode* und was geschieht, wenn die *vorwärts* und *zurück* Tasten betätigt werden

| # | Titel | Beschreibung | vorwärts| zurück |
| --- | --- | --- | --- | --- |
| 1 | Hörspiel | eine zufällige Datei aus dem Ordner | stop | Titel von vorne spielen |
| 2 | Album | kompletten Ordner spielen | nächster Titel | vorherigen Titel spielen |
| 3 | Party | Ordner in zufälliger Reihenfolge abspielen | zufälliger Titel | Titel von vorne spielen  |
| 4 | Einzel | Eine Datei aus dem Ordner abspielen | stop | Titel von vorne spielen |
| 5 | Hörbuch | kompletten Ordner spielen und Fortschritt merken | nächster Titel | vorherigen Titel spielen |
| 6 | Admin | Noch ohne Funktion | - | - |

**Special**  
Wird nur in bestimmten Modi benutzt für:
- mode 4: Titelnummer
- mode 6: Platzhalter, bisher ohne Funktion


## NFC
How discovered NFC tags are dispatched to activities: 
https://developer.android.com/guide/topics/connectivity/nfc/nfc.html#dispatching

Currently only Mifare Classic, but I want to look into supporting generic NfcA in the future.
Links:

- [Android Tag Technology (NfcA, NfcB, ..)](https://developer.android.com/guide/topics/connectivity/nfc/advanced-nfc)
- [Stackoverflow answer that also contains a command overview of NfcA commands](https://stackoverflow.com/a/42915018)
- [Stackoverflow answer with general help on NfcA](https://stackoverflow.com/a/40303293)
- [Summary of Open Source projects using Android's NfcA API](https://www.programcreek.com/java-api-examples/index.php?api=android.nfc.tech.NfcA)
    - [Example from above's list that actually uses NfcA (and not Mifare)](https://www.programcreek.com/java-api-examples/?code=ProjectMAXS/maxs/maxs-master/module-nfc/src/org/projectmaxs/module/nfc/tech/NfcAHandler.java#)
