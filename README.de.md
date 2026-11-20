# RF2 Server Manager

[English](README.md) · [Italiano](README.it.md) · [Español](README.es.md) · [Français](README.fr.md) · **Deutsch** · [Português](README.pt.md)

**Download:** [neueste Version](https://github.com/KarmaTV80/rf2-server-manager/releases/latest)

**Projekt unterstützen:** [mit PayPal spenden](https://www.paypal.com/donate/?business=3T7ZTAXBQY3EN&no_recurring=0&item_name=Sostieni+Karma+TV%3A+progetti+e+canali+YouTube%2C+Instagram%2C+TikTok.+Support+my+projects+and+channels.+Grazie%21+Thanks%21&currency_code=EUR) – die App ist kostenlos, jede Spende hilft, sie aktuell zu halten.

---

Ein Windows-Programm, das einen RF2 Dedicated Server einrichtet und startet.
Es ist kein offizielles Produkt und steht in keiner Verbindung zu Studio 397 oder Motorsport Games.

Beim ersten Start erkennt die App die Sprache von Windows: Italienisch, Englisch, Spanisch, Französisch, Deutsch oder Portugiesisch. Andere Sprachen werden zu Englisch. Der Button mit der Flagge oben rechts ändert sie, und die App merkt sich deine Wahl.

## Voraussetzungen

- Windows 10 oder 11, 64 Bit. .NET ist bereits in der exe enthalten.
- Speicherplatz für den Server und die Inhalte.
- Microsoft Edge WebView2 Runtime, nur für den Browser im Workshop-Tab. Ohne ihn kannst du die Workshop-ID von Hand einfügen.

Der Dedicated Server und SteamCMD sind nicht enthalten: Die App kann sie mit der geführten Einrichtung von Valve und Steam herunterladen.

## Erster Start

1. Starte `RF2ServerManager.exe`. Eine Installation ist nicht nötig.
2. Zeigt Windows „Der Computer wurde durch Windows geschützt“, wähle **Weitere Informationen** und dann **Trotzdem ausführen**. Die Meldung erscheint, weil die exe keine digitale Signatur hat.
3. Wähle in der geführten Einrichtung die Ordner von SteamCMD und vom Server, oder lass die App sie herunterladen.
4. Starte den Server einmal: Er legt seine Konfigurationsdateien an. Fragt Windows nach der Firewall-Erlaubnis, wähle **Zulassen**.

## Updates

Beim Start prüft die App auf GitHub, ob es eine neue Version gibt. Wenn ja, erscheint unten im linken Menü das Feld **Jetzt aktualisieren**. Die App lädt sie herunter, prüft ihren SHA-256-Fingerabdruck und öffnet sich selbst neu; ein laufender Server bleibt an. Unter der Versionsnummer prüft **Nach Updates suchen** noch einmal von Hand. Kann in den Ordner der App nicht geschrieben werden (zum Beispiel unter Programme), lade die neue Version von der [Versionsseite](https://github.com/KarmaTV80/rf2-server-manager/releases) herunter.

## Inhalte, die du schon im Spiel hast

Du musst sie weder neu herunterladen noch von Hand kopieren. Die App findet den Spielordner selbst, du kannst ihn aber auch in Schritt 1. Vorbereiten wählen. Drücke in Schritt 3. Inhalte auf **Aus dem Spiel hinzufügen**, wähle Autos und Strecken und drücke **Auf den Server kopieren**. Das Spiel wird nur gelesen.

In der **Bibliothek** zeigt jeder Inhalt seinen Zustand: *Bereit*, *Zu installieren* oder *Paket fehlt*, wenn Freunde ihn nicht herunterladen können. Der Button in der Zeile tut das Richtige: Er installiert, kopiert das Paket aus dem Spiel oder öffnet den Workshop mit der Suche nach diesem Inhalt. Autos und Strecken des Events wählst du in Schritt 4. Event mit **Neues Event erstellen**.

Inhalte, die im Spiel ohne `.rfcmp`-Paket installiert sind (zum Beispiel auf einer Website gekauft), stehen am Ende der Listen: Von ihnen wird die Installation auf den Server kopiert, und beitreten können nur Fahrer, die sie schon haben, in derselben Version.

Gekaufte offizielle DLCs funktionieren auf dem Server: Die App kopiert selbst die Freischaltdatei, die das Spiel vorbereitet (`ServerUnlock.bin`). Updates der Inhalte werden ebenfalls selbst angewendet.

## Mit anderen spielen

Leite am Router auf die IP des PCs weiter:

| Port | Protokoll | Zweck |
|---|---|---|
| 54297 | TCP und UDP | Simulation |
| 64297 | TCP | Herunterladen der Dateien durch die Clients |
| 64298 und 64299 | UDP | Steam: Ohne sie erscheint der Server nicht in der Liste des Spiels |

**Öffne niemals die Ports 5397 und 5398**: Sie steuern den Server und das Spiel. Setze immer ein Beitrittspasswort und ein Admin-Passwort, die sich unterscheiden. Der Button **Netzwerk und Ports prüfen** in Schritt 10. Server hilft dir bei der Prüfung.

## Anti-Cheat

In Schritt 9. Chat und Ping kann die App Fahrer mit unmöglichen Runden oder Geschwindigkeiten und Sprünge von einem Punkt der Strecke zum anderen melden; dabei vergleicht sie jeden Fahrer mit den anderen derselben Klasse. Sie trennt niemanden: Sie warnt und schreibt alles ins Verdachtsprotokoll (`sospetti.log`), dann entscheidet, wer den Server betreibt. Der Server sieht nicht in die PCs der Fahrer, er findet also die Auswirkungen von Cheats, nicht die Programme.

## Wo die Daten liegen

- Einstellungen und Protokoll: `%AppData%\RF2ServerManager`
- Passwörter: nur in den Konfigurationsdateien des Servers, der sie im Klartext speichert. Sie landen nicht in den Profilen.

## Ein Problem melden

Nutze **Melden** oben rechts in der App oder **Info → Problem melden** (ab Version 1.0.6). Die App zeigt das Protokoll bereits ohne Windows-Benutzername, Fahrernamen, Steam-IDs, IP-Adressen und Chatnachrichten, speichert es als Textdatei und öffnet auf GitHub das [Meldeformular](https://github.com/KarmaTV80/rf2-server-manager/issues/new?template=segnalazione.yml): Beschreibe, was passiert ist, und hänge die Datei an. Meldungen sind öffentlich und brauchen ein kostenloses GitHub-Konto. Der Button **Protokollordner öffnen** ist in Schritt 1. Vorbereiten.

## Bekannte Grenzen

- Das Erstellen von Mods und das Installieren von Paketen steuern MAS2 und ModMgr im Hintergrund, mit versteckten Fenstern: Den Fortschritt liest du im Protokoll der App. Mit „Sitzung sofort starten“ startet auch das Serverfenster minimiert: Du öffnest es über die Windows-Taskleiste wieder. Ein Update dieser Werkzeuge kann eine Anpassung der App erfordern.
- Kostenpflichtige Inhalte und aus dem Workshop kopierte Pakete lassen sich eventuell nicht installieren: Die App zeigt den Fehler an und räumt die Dateien auf.
- Training 2 hat in der Serverkonfiguration keine eigene Uhrzeit und Dauer.

## Nutzungsbedingungen

Kostenlos, auch für Meisterschaften und Ligen. Es ist nicht erlaubt, das Programm zu verändern, zu dekompilieren, weiterzuverkaufen oder von anderen Seiten aus zu verbreiten: Teile nur den offiziellen Link. Vollständiger Text in `LICENSE.txt` und im Fenster **Info** der App.

Komponenten von Drittanbietern: FlaUI und Newtonsoft.Json (MIT-Lizenz), Microsoft WebView2 SDK (Microsoft-Lizenz), .NET (MIT-Lizenz), Schriften Saira Extra Condensed und Barlow (SIL Open Font License, Texte in `Licenze\`).
