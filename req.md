# Funktionale Anforderungen – TCO App

> Stand: 08.04.2026 · Technische Details → `PROJEKTPLAN.md`

Die App ist die digitale Vereinsapp des **TCO** (Tauch-Club). Dieses Dokument beschreibt alle funktionalen Anforderungen sowie das Rollen- und Rechtemodell als fachliche Arbeitsgrundlage für Planung, Implementierung und Priorisierung.

| Priorität | Bedeutung |
|-----------|-----------|
| **Muss** | Zwingend erforderlich |
| **Soll** | Hohe Priorität, aber kein Blocker |
| **Kann** | Nice-to-have |

| Status | Bedeutung |
|--------|-----------|
| `Offen` | Noch nicht begonnen |
| `In Klärung` | Fachlich noch offen |
| `Freigegeben` | Abgenommen, bereit zur Umsetzung |
| `Umgesetzt` | Fertig implementiert |

---

## Globale Anforderungen

Gelten für alle FRs, sofern nicht explizit abweichend dokumentiert.

- Alle Funktionen laufen auf **iOS, Android und Web**
- Authentifizierung und Datenpersistenz über **Supabase**
- Geschützte Bereiche nur für angemeldete und freigeschaltete Benutzer zugänglich
- Rollenbasierte Zugriffskontrolle (siehe Abschnitt Rollen und Rechte)
- DSGVO-Konformität: personenbezogene Daten werden nur zweckgebunden gespeichert
- Ladefehler und Fehlerzustände werden dem Benutzer verständlich angezeigt
- Verpflichtende Profilfelder: Vorname, Nachname, E-Mail-Adresse

---

## Getroffene fachliche Entscheidungen

- Benutzer dürfen sich selbst registrieren; Konto muss von Admin oder Vorstand freigeschaltet werden
- Ein Benutzer darf gleichzeitig mehrere Rollen haben
- Push-Benachrichtigungen werden über den Expo Push Notification Service versendet
- News werden über die WordPress REST API der Vereinswebsite geladen

---

## Übersicht

| ID | Titel | Priorität | Status |
|----|-------|-----------|--------|
| FR-001 | Anmeldung | Muss | `Umgesetzt` |
| FR-002 | Kontoaktivierung und Freischaltung | Muss | `Umgesetzt` |
| FR-003 | Rollen und Berechtigungen | Muss | `Umgesetzt` |
| FR-004 | Rollenbereiche Vorstand und Übungsleiter | Soll | `In Klärung` |
| FR-005 | Benutzerverwaltung durch Admin | Soll | `Umgesetzt` |
| FR-006 | Eigenes Profil | Soll | `Umgesetzt` |
| FR-007 | Registrierung | Muss | `Umgesetzt` |
| FR-008 | Passwort zurücksetzen | Muss | `Umgesetzt` |
| FR-009 | Abmelden | Muss | `Umgesetzt` |
| FR-010 | Startseite | Muss | `Umgesetzt` |
| FR-011 | Vereinsnews | Soll | `Umgesetzt` |
| FR-012 | Vereinstermine einsehen | Muss | `Umgesetzt` |
| FR-013 | Termine verwalten | Soll | `Umgesetzt` |
| FR-014 | Terminanmeldung | Soll | `Umgesetzt` |
| FR-015 | Tauchsparten verwalten | Soll | `Umgesetzt` |
| FR-016 | Push-Benachrichtigungen | Muss | `Umgesetzt` |
| FR-017 | Push-Benachrichtigung bei Neuregistrierung | Soll | `Umgesetzt` |
| FR-018 | E-Mail-Benachrichtigungen | Kann | `Offen` |
| FR-019 | Notrufnummern | Soll | `Umgesetzt` |
| FR-020 | Preisliste Vereinsheim | Soll | `Umgesetzt` |
| FR-021 | Octopost (Vereinszeitschrift) | Soll | `Umgesetzt` |
| FR-022 | Trainingsplan | Soll | `Umgesetzt` |
| FR-023 | Threadbasierter Chat | Soll | `Offen` |
| FR-024 | Umfragen und Abstimmungen | Soll | `Umgesetzt` |
| FR-025 | Mitgliederliste | Soll | `Offen` |
| FR-026 | Seebedingungen | Soll | `Umgesetzt` |
| FR-027 | Bildergalerie | Kann | `Umgesetzt` |
| FR-028 | Materialbuchung | Soll | `Offen` |
| FR-029 | Taucher-Rechner (EAD, MOD, Auftrieb, Rig) | Soll | `Umgesetzt` |
| FR-030 | Gas-Blender Tool | Kann | `Umgesetzt` |
| FR-031 | Decoplanner | Kann | `Umgesetzt` |
| FR-032 | Deco2000 / Bergsee / Nitrox-Tabellen | Kann | `Umgesetzt` |

---

## Anforderungen

### FR-001 Anmeldung
**Priorität:** Muss · **Status:** `Umgesetzt`

Benutzer meldet sich mit E-Mail und Passwort an. Session bleibt dauerhaft aktiv.

- Login-Formular akzeptiert E-Mail und Passwort
- Fehlgeschlagene Anmeldung liefert verständliche Fehlermeldung
- Session bleibt nach App-Neustart erhalten

---

### FR-002 Kontoaktivierung und Freischaltung
**Priorität:** Muss · **Status:** `Umgesetzt`

Neues Konto ist erst nach E-Mail-Bestätigung und manueller Freischaltung durch Admin oder Vorstand nutzbar.

- Aktivierungslink per E-Mail nach Registrierung (gültig 2 Tage)
- Nicht aktivierte oder nicht freigeschaltete Konten haben keinen Zugriff
- Admin/Vorstand sieht ausstehende Konten und kann freischalten
- Ungültige oder abgelaufene Links werden sauber behandelt

---

### FR-003 Rollen und Berechtigungen
**Priorität:** Muss · **Status:** `Umgesetzt`

Jedes Konto hat mindestens eine Rolle (Admin, Vorstand, Übungsleiter, Mitglied). Rollen steuern den Zugriff auf Bereiche und Aktionen.

- Rolle ist nach Anmeldung in der Session verfügbar
- Konto ohne Rolle kann sich nicht einloggen
- Mehrfachrollen sind möglich

> **Offene Fragen:** Ob Rollen manuell oder regelbasiert vergeben werden.

---

### FR-004 Rollenbereiche Vorstand und Übungsleiter
**Priorität:** Soll · **Status:** `In Klärung`

Vorstand und Übungsleiter erhalten gegenüber Mitgliedern erweiterte Rechte. Umfang ist in `roles.md` zu spezifizieren.

- Vorstand: mindestens ein klar abgegrenzter erweiterter Bereich
- Übungsleiter: mindestens ein fachlicher Verantwortungsbereich (Trainings/Termine)
- Rechte sind von Admin-Rechten getrennt

> **Offene Fragen:** Welche Daten Vorstand sieht; ob Übungsleiter nur Termine der eigenen Sparte verwaltet.

---

### FR-005 Benutzerverwaltung durch Admin
**Priorität:** Soll · **Status:** `Umgesetzt`

Admin verwaltet alle Benutzerkonten.

- Benutzer einsehen, Rollen vergeben/ändern, Kontostatus erkennen
- Konto löschen mit doppelter Bestätigung (DSGVO-konform, Inhalte bleiben als „gelöscht" erhalten)
- Konto kann nicht durch den Benutzer selbst gelöscht werden

> **Offene Fragen:** Ob Admin Aktivierungslinks erneut auslösen kann.

---

### FR-006 Eigenes Profil
**Priorität:** Soll · **Status:** `Umgesetzt`

Angemeldeter Benutzer kann eigene Profildaten einsehen und erlaubte Felder bearbeiten.

- Pflichtfelder: Vorname, Nachname, E-Mail-Adresse
- Passwort änderbar über Profil (aktuelles Passwort erforderlich, min. 8 Zeichen)
- Nach Passwortänderung bleibt Session aktiv

> **Offene Fragen:** Ob E-Mail-Änderung erneut bestätigt werden muss.

---

### FR-007 Registrierung
**Priorität:** Muss · **Status:** `Umgesetzt`

Neue Benutzer können sich selbst registrieren.

- Formular: Vorname, Nachname, E-Mail, Passwort (min. 8 Zeichen), Passwort-Wiederholung
- Doppelte E-Mail-Adressen werden abgelehnt
- Nach Registrierung: Hinweis auf nächsten Schritt (E-Mail prüfen, auf Freischaltung warten)

---

### FR-008 Passwort zurücksetzen
**Priorität:** Muss · **Status:** `Umgesetzt`

Benutzer kann vergessenes Passwort über E-Mail-Link zurücksetzen. Link ist 1 Stunde gültig.

---

### FR-009 Abmelden
**Priorität:** Muss · **Status:** `Umgesetzt`

Benutzer kann sich jederzeit abmelden. Session wird serverseitig beendet, Weiterleitung zum Login.

---

### FR-010 Startseite
**Priorität:** Muss · **Status:** `Umgesetzt`

Nach dem Login wird eine Startseite mit Vereinsname, aktuellen News, nächsten Terminen und personalisierter Begrüßung angezeigt.

---

### FR-011 Vereinsnews
**Priorität:** Soll · **Status:** `Umgesetzt`

News vom Vereinsblog werden chronologisch angezeigt. Artikel öffnen sich inline in der App.

- Jede News zeigt: Titel, Datum, Vorschaubild, Kurztext
- Artikel öffnet sich in der App (nicht im Browser)
- Link zum Original-Artikel auf der Website vorhanden

---

### FR-012 Vereinstermine einsehen
**Priorität:** Muss · **Status:** `Umgesetzt`

Alle angemeldeten Benutzer sehen Termine mit Datum, Titel, Beschreibung und Sparte. Filterbar nach Tauchsparte (Allgemein, Tauchen, Hockey, Rugby).

---

### FR-013 Termine verwalten
**Priorität:** Soll · **Status:** `Umgesetzt`

Admin, Vorstand und Übungsleiter können Termine anlegen, bearbeiten und absagen. Datum/Uhrzeit über nativen Picker. Abgesagte Termine sind als solche erkennbar.

> **Offene Fragen:** Ob Übungsleiter nur Termine der eigenen Sparte verwalten darf.

---

### FR-014 Terminanmeldung
**Priorität:** Soll · **Status:** `Umgesetzt` Teilnehmerliste ist für alle einsehbar.

- Anmeldung nach Terminablauf nicht mehr möglich
- maximale Teilnehmerzahl je Termin soll möglich sein
- Es soll möglich sein die Abmeldung zu sperren (zB für Kurse)
- Es soll dem Admin möglich sein Teilnehmer von einem Termin zu entfernen

---

### FR-015 Tauchsparten verwalten
**Priorität:** Soll · **Status:** `Umgesetzt`

Admin kann Tauchsparten anlegen, umbenennen und löschen (nur wenn keine Termine zugeordnet). Sparten gelten systemweit.

---

### FR-016 Push-Benachrichtigungen
**Priorität:** Muss · **Status:** `Umgesetzt`

App fordert beim ersten Start Berechtigung an. Push-Tokens werden in der Datenbank gespeichert und beim Abmelden entfernt. Funktioniert auch bei geschlossener App (iOS und Android). Web optional.

- Benutzer kann Push-Benachrichtigungen im Profil global und je Typ (Chat, Termine, Umfragen) steuern

---

### FR-017 Push-Benachrichtigung bei Neuregistrierung
**Priorität:** Soll · **Status:** `Umgesetzt`

Alle Admins erhalten eine Push-Benachrichtigung wenn sich ein neuer Benutzer registriert. Nachricht enthält Vor- und Nachname. Tipp öffnet App im Verwaltungsbereich.

> **Offene Fragen:** Ob Vorstand ebenfalls benachrichtigt werden soll.

---

### FR-018 E-Mail-Benachrichtigungen
**Priorität:** Kann · **Status:** `Offen`

Benutzer erhalten E-Mails bei: Registrierung (Aktivierungslink), Freischaltung, Passwort-Zurücksetzen. Abbestellbar im Profil.

> **Offene Fragen:** Ob weitere Ereignisse (neue Termine etc.) Benachrichtigungen auslösen sollen.

---

### FR-019 Notrufnummern
**Priorität:** Soll · **Status:** `Umgesetzt`

Tauchrelevante Notrufnummern (Notruf 112, DAN Europe, Druckkammer) ohne Login einsehbar. Tipp auf Eintrag öffnet Telefon-Wähler. Admin kann Einträge pflegen.

> **Offene Fragen:** Ob Druckkammer-Nummern regional gefiltert werden sollen.

---

### FR-020 Preisliste Vereinsheim
**Priorität:** Soll · **Status:** `Umgesetzt`

Preisliste für Getränke/Snacks, nach Kategorie gruppiert. Admin pflegt Einträge und PayPal-Link. Tipp auf Link öffnet PayPal-App oder Browser.

> **Offene Fragen:** Ob Kategorien frei definierbar oder fest vorgegeben sein sollen.

---

### FR-021 Octopost (Vereinszeitschrift)
**Priorität:** Soll · **Status:** `Umgesetzt`

PDF-Archiv der Vereinszeitschrift. Alle Mitglieder können Ausgaben öffnen. Admin lädt neue Ausgaben hoch und kann Ausgaben löschen. PDFs nur für angemeldete Benutzer abrufbar.

- Liste chronologisch sortiert (neueste zuerst), Eintrag zeigt Titel, Monat, Jahr
- PDF öffnet im nativen Viewer oder Browser via signierter URL

---

### FR-022 Trainingsplan
**Priorität:** Soll · **Status:** `Umgesetzt`

Admin, Vorstand und Übungsleiter pflegen Trainer-Einteilungen (Name, Datum, optionale Bemerkung). Alle Mitglieder können nur lesen. Chronologisch sortiert. Ein Trainer pro Termin, keine Spartenfilterung.

---

### FR-023 Threadbasierter Chat
**Priorität:** Soll · **Status:** `Offen`

Vereinsinterne Kommunikation in Kanälen (Allgemein + spartenbezogene Kanäle). Nachrichten mit Thread-Antworten in Echtzeit (Supabase Realtime).

- Jede Nachricht zeigt Absender (Vorname + Nachname) und Zeitstempel
- Admin: Kanäle und Nachrichten verwalten
- Mitglieder: eigene Nachrichten löschen
- Ungelesene Nachrichten erkennbar
- Dateianhänge: nein
- Nachrichten sollen nach 1 Monat gelöscht werden
- Privatchat nicht möglich
- Kanäle sollen für Rollen eingeschränkt werden können z.B. Kanal für Übungsleiter.
- Chat soll in der unteren Leiste als Symbol sein


---

### FR-024 Umfragen und Abstimmungen
**Priorität:** Soll · **Status:** `Umgesetzt` (Frage, Antwortoptionen, optionales Enddatum). Jedes Mitglied stimmt einmal ab. Ergebnis nach eigener Stimmabgabe sichtbar. Ersteller kann Umfrage vorzeitig beenden.

> **Offene Fragen:** Anonymität; Zielgruppen nach Rolle/Sparte; Einfach- vs. Mehrfachauswahl; Integration in Chat.

---

### FR-025 Mitgliederliste
**Priorität:** Soll · **Status:** `Offen`

Liste aller aktiven Mitglieder (Vorname, Nachname, Rollen, Profilbild) alphabetisch sortiert. Mitglieder laden eigenes Profilbild hoch. Admin kann Profilbilder entfernen. Nicht freigeschaltete Konten erscheinen nicht.

> **Offene Fragen:** Detailansicht je Mitglied; Filter nach Sparte/Rolle; Datenschutz-Sichtbarkeit.

---

### FR-026 Seebedingungen
**Priorität:** Soll · **Status:** `Umgesetzt` (Wassertemperatur, Sichtweite, Kommentar, bis zu 3 Fotos). Aktueller Stand und letzte 10 Einträge als Verlauf sichtbar. Admin kann Einträge/Bilder löschen. Tauchplatzkarte später einbettbar.

> **Offene Fragen:** Tiefenspezifische Messwerte; Benachrichtigungen bei neuen Einträgen.

---

### FR-027 Bildergalerie
**Priorität:** Kann · **Status:** `Umgesetzt`

Mitglieder teilen Fotos in Alben. Vollbildansicht. Jedes Mitglied kann Alben anlegen und Fotos hochladen. Eigene Fotos löschen möglich, Admin kann alle löschen. Bilder in Supabase Storage (Bucket `photos`).

---

### FR-028 Materialbuchung
**Priorität:** Soll · **Status:** `Offen`

Mitglieder buchen Vereinsausrüstung (Regler, Flaschen, Jackets) für einen Zeitraum. Verfügbarkeit in Echtzeit sichtbar. Admin verwaltet Gegenstände. Admin/Vorstand sehen und stornieren alle Buchungen.

> **Offene Fragen:** Maximale Buchungsdauer; Warteliste; Zustandserfassung (defekt/Wartung); Kopplung an Termine.

---

### FR-029 Taucher-Rechner (EAD, MOD, Auftrieb, Balanced Rig)
**Priorität:** Soll · **Status:** `Umgesetzt`

Sammlung taucherischer Berechnungstools, alle lokal (clientseitig, kein Server-Call). Ergebnisse werden sofort bei Eingabe neu berechnet. Keine Speicherung der Eingaben.

**FR-030a – EAD (Equivalent Air Depth):**
Berechnet die äquivalente Lufttiefe für ein Nitrox-Gemisch.
- Eingabe: Tauchtiefe (m), O₂-Anteil (%)
- Ausgabe: EAD in Metern
- Formel: `EAD = (Tiefe + 10) × (1 − fO₂) / 0,79 − 10`

**FR-030b – MOD (Maximum Operating Depth):**
Berechnet die maximale Betriebstiefe für ein Gemisch bei gegebener ppO₂-Grenze.
- Eingabe: O₂-Anteil (%), ppO₂-Grenzwert (Standard 1,4 bar, einstellbar bis 1,6 bar)
- Ausgabe: MOD in Metern
- Formel: `MOD = (ppO₂ / fO₂ − 1) × 10`
- Farbliche Warnung wenn ppO₂ > 1,4 bar

**FR-030c – Flaschen-Auftriebsberechnung:**
Berechnet den Auftrieb einer Stahlflasche leer vs. voll.
- Eingabe: Flaschengröße (l), Arbeitsdruck (bar), Leergewicht (kg), Materialauftrieb (kg, vorausgefüllt für gängige Typen)
- Ausgabe: Auftrieb leer (kg), Auftrieb voll (kg), Differenz
- Hinweis: positive Zahl = Auftrieb, negative Zahl = Abtrieb

**FR-030d – Balanced Rig Rechner:**
Hilft dem Taucher, sein Tauchequipment optimal auszubalancieren (Nullauftrieb an der Oberfläche am Ende des Tauchgangs).
- Eingabe: Körpergewicht (kg), Neoprendicke oder Trockensuit, Salzwasser/Süßwasser, Flasche(n) mit Auftriebswerten, Jacket-Typ mit Liftkapazität, aktuelles Blei (kg)
- Ausgabe: Empfohlenes Blei (kg), Systemgesamtauftrieb, Hinweis ob Über-/Unterbleit
- Vordefinierte Flaschenkonfigurationen: 10 l Stahl, 12 l Stahl, D8.5, D10, D12
- Dry-Suit-Inflation wird nicht berücksichtigt

---

### FR-030 Gas-Blender Tool
**Priorität:** Kann · **Status:** `Umgesetzt`

Unterstützt Gasmischer beim Berechnen von Nitrox- und Trimix-Mischungen. Alle Berechnungen lokal, kein Server-Call.

**Teilfunktionen:**

**Partial-Pressure Blending (PP-Blending):**
- Eingabe: Ziel-O₂% (und optional He%), Zieldruck (bar), Restdruck in der Flasche (bar), Restgasanalyse (O₂%, He%)
- Ausgabe: Aufzufüllende O₂-Menge (bar), aufzufüllende He-Menge (bar), Restluft (bar), Zieldruck-Kontrolle
- Schrittweise Anleitung: 1. O₂ auffüllen, 2. He auffüllen, 3. mit Luft/Nitrox auffüllen

**Continuous-Flow / Blending Stick:**
- Eingabe: Ziel-O₂%, Zieldruck, verfügbare Quellgase (O₂-Anteil und Druck je Quelle)
- Ausgabe: Mischverhältnis der Quellen in Prozent und bar

**Mischungskontrolle / Analyse:**
- Eingabe: Gemessener O₂-Anteil (%), Fülldruck (bar)
- Ausgabe: MOD bei ppO₂ 1,4 und 1,6 bar, EAD

> **Offene Fragen:** Trimix (He-Anteil) als Pflichtfeld oder optional; Gesetzliche Hinweise/Haftungsausschluss; Einheitenwahl bar/PSI.

---

### FR-031 Decoplanner
**Priorität:** Kann · **Status:** `Umgesetzt`

Interaktives Tool zur Planung von Dekotauchgängen. Berechnet Dekostopps, Gesamtzeit und Gasverbrauch.

**Eingaben:**
- Tiefenprofil: max. Tiefe (m), Grundzeit (min), Abstiegsrate (m/min), Aufstiegsrate (m/min)
- Gasgemische: Grundgas (O₂%, He%), Dekogase (bis zu 3, je mit Wechseltiefe)
- Algorithmus-Parameter: Gradient Factors (GF Low / GF High), Höhe über NN (m)
- Wassertyp: Salz- oder Süßwasser

**Ausgaben:**
- Dekostopps-Tabelle: Tiefe (m), Haltezeit (min), Gas
- Gesamtaufstiegszeit (min)
- Gasverbrauchsplan je Gas (l, bei gegebenem SAC-Wert)
- TTS (Time To Surface)
- CNS O₂-Belastung (%)
- Hinweis bei Überschreitung von ppO₂-Grenzwerten

**Algorithmus:**
- Bühlmann ZHL-16C mit Gradient Factors als Basis
- Reine Clientberechnung in TypeScript

> **Offene Fragen:** Repetitive Tauchgänge / Surface Interval; Multi-Level-Profile; VPM-B als alternative Modell-Option; Export der Deko-Tabelle als PDF; Integration mit Logbuch (FR-029).

---

### FR-032 Deco2000 / Bergsee / Nitrox-Tabellen
**Priorität:** Kann · **Status:** `Umgesetzt`

Digitale Nachschlagewerke klassischer Tauchtabellen als Read-only-Referenz in der App. Kein interaktiver Rechner, sondern Tabellenanzeige zum Nachschlagen.

**Enthaltene Tabellen:**

**Deco2000 (Deutsche Sporttaucher-Dekotabelle):**
- Standardtabelle für Sporttaucher in Deutschland
- Nullzeittabelle und Dekostopptabelle
- Wiederholungstauchgänge mit Gruppenintervall
- Anzeige als scrollbare Tabelle mit Suchfunktion (Tiefe + Zeit → Gruppe/Stopps)

**Bergsee-Korrektur:**
- Höhenkorrekturtabelle für Tauchgänge ab 300 m über NN
- Eingabe: Höhe (m), Gruppe aus Vortauchgang → Korrigierte Gruppe
- Als separater Tab oder Zusatzabschnitt zur Deco2000-Tabelle

**Nitrox-Tabelle:**
- Standardnitrox-Tabelle (CMAS/PADI-Stil)
- Für EAN32 und EAN36
- Anzeige: Tiefe, Nullzeit, MOD, ppO₂

**Darstellung:**
- Farbcodierung der Dekostufen (grün = keine Deko, gelb = Stopptime < 10 min, rot = > 10 min)
- Zoomfähige Tabellen auf kleinen Bildschirmen (horizontales Scrollen)

> **Offene Fragen:** Urheberrechtliche Klärung der Tabelleninhalte (insb. Deco2000); ob Tabellenwerte manuell einzupflegen oder aus lizenzierten Quellen zu übernehmen sind; Aktualität der Tabellen (letzte offizielle Version).

---

## Rollen und Rechte

### Rollen

| Rolle | Zweck |
|-------|-------|
| **Admin** | Vollzugriff auf alle Verwaltungsfunktionen |
| **Vorstand** | Erweiterte Einsichts- und Verwaltungsrechte (fachlich noch zu schärfen) |
| **Übungsleiter** | Verwaltung von Trainings, Terminen und Gruppen |
| **Mitglied** | Standardrolle für alle normalen Benutzer |

**Grundprinzipien:**
- Jeder Benutzer hat mindestens eine Rolle, Mehrfachrollen sind möglich
- Nicht freigeschaltete Konten haben keinen Zugriff auf geschützte Bereiche
- Die Session enthält Rolle, Aktivierungs- und Kontostatus
- UI-Sichtbarkeit allein ist keine ausreichende Sicherheitsmaßnahme

### Rechte-Matrix (aktuell implementiert)

| Funktion | Admin | Vorstand | Übungsleiter | Mitglied |
|----------|:-----:|:--------:|:------------:|:--------:|
| Anmelden, Profil bearbeiten, Abmelden | ✅ | ✅ | ✅ | ✅ |
| Termine einsehen | ✅ | ✅ | ✅ | ✅ |
| News, Startseite, Notrufnummern | ✅ | ✅ | ✅ | ✅ |
| Octopost einsehen | ✅ | ✅ | ✅ | ✅ |
| Preisliste einsehen | ✅ | ✅ | ✅ | ✅ |
| Trainingsplan einsehen | ✅ | ✅ | ✅ | ✅ |
| Termine anlegen/bearbeiten/absagen | ✅ | ✅ | ✅ | ❌ |
| Trainingsplan pflegen | ✅ | ✅ | ✅ | ❌ |
| Octopost hochladen/löschen | ✅ | ❌ | ❌ | ❌ |
| Preisliste und PayPal-Link pflegen | ✅ | ❌ | ❌ | ❌ |
| Notrufnummern pflegen | ✅ | ❌ | ❌ | ❌ |
| Tauchsparten verwalten | ✅ | ❌ | ❌ | ❌ |
| Benutzer verwalten (einsehen, Rollen, freischalten) | ✅ | ❌ | ❌ | ❌ |
| Benutzer löschen | ✅ | ❌ | ❌ | ❌ |
| Push-Nachrichten an alle senden | ✅ | ❌ | ❌ | ❌ |
| Admin-Tab sichtbar | ✅ | ❌ | ❌ | ❌ |

### Offene Punkte

- Welche konkreten Rechte Vorstand gegenüber Mitgliedern erhalten soll
- Ob Übungsleiter nur Termine der eigenen Sparte verwalten darf
- Ob Vorstand ebenfalls Push-Benachrichtigungen bei Neuregistrierungen erhält

---

## Bezug zu anderen Dokumenten

- [`PROJEKTPLAN.md`](PROJEKTPLAN.md) – technische Planung und Architektur
