# Funktionale Anforderungen – TCO App

Stand: 08.04.2026

## Präambel

Die App ist die digitale Vereinsapp des **TCO** (Tauch-Club). Diese Datei beschreibt alle funktionalen Anforderungen als fachliche Arbeitsgrundlage für Planung, Implementierung und Priorisierung. Technische Details gehören in `PROJEKTPLAN.md`, Rollen und Berechtigungen in `roles.md`.

**Prioritäten:** Muss · Soll · Kann  
**Status:** Offen · In Klärung · Freigegeben · Umgesetzt

## Globale Anforderungen (gelten für alle FRs)

- Alle Funktionen laufen auf iOS, Android und Web (Ausnahmen sind explizit dokumentiert)
- Authentifizierung und Datenpersistenz erfolgen über Supabase
- Geschützte Bereiche sind nur für angemeldete und freigeschaltete Benutzer zugänglich
- Rollenbasierte Zugriffskontrolle gemäß `roles.md`
- DSGVO-Konformität: personenbezogene Daten werden nur zweckgebunden gespeichert
- Ladefehler und Fehlerzustände werden dem Benutzer verständlich angezeigt
- Verpflichtende Profilfelder: Vorname, Nachname, E-Mail-Adresse

## Getroffene fachliche Entscheidungen

- Benutzer dürfen sich selbst registrieren; das Konto muss von Admin oder Vorstand freigeschaltet werden
- Ein Benutzer darf gleichzeitig mehrere Rollen haben
- Push-Benachrichtigungen werden über den Expo Push Notification Service versendet
- News werden über die WordPress REST API der Vereinswebsite geladen

## Funktionale Anforderungen

### FR-001 Anmeldung · Muss · Umgesetzt

Benutzer meldet sich mit E-Mail und Passwort an. Session bleibt dauerhaft aktiv.

- Login-Formular akzeptiert E-Mail und Passwort
- Fehlgeschlagene Anmeldung liefert verständliche Fehlermeldung
- Session bleibt nach App-Neustart erhalten

### FR-002 Kontoaktivierung und Freischaltung · Muss · Umgesetzt

Neues Konto ist erst nach E-Mail-Bestätigung und manueller Freischaltung durch Admin oder Vorstand nutzbar.

- Nach Registrierung: Aktivierungslink per E-Mail (gültig 2 Tage)
- Nicht aktivierte oder nicht freigeschaltete Konten haben keinen Zugriff
- Admin/Vorstand sieht ausstehende Konten und kann freischalten
- Ungültige oder abgelaufene Links werden sauber behandelt

### FR-003 Rollen und Berechtigungen · Muss · Umgesetzt

Jedes Konto hat mindestens eine Rolle (Admin, Vorstand, Übungsleiter, Mitglied). Rollen steuern den Zugriff auf Bereiche und Aktionen.

- Rolle ist nach Anmeldung in der Session verfügbar
- Konto ohne Rolle kann sich nicht einloggen
- Mehrfachrollen sind möglich

Offene Fragen: Ob Rollen manuell oder regelbasiert vergeben werden.

### FR-004 Rollenbereiche Vorstand und Übungsleiter · Soll · In Klärung

Vorstand und Übungsleiter erhalten gegenüber Mitgliedern erweiterte Rechte. Umfang ist in `roles.md` zu spezifizieren.

- Vorstand: mindestens ein klar abgegrenzter erweiterter Bereich
- Übungsleiter: mindestens ein fachlicher Verantwortungsbereich (Trainings/Termine)
- Rechte sind von Admin-Rechten getrennt

Offene Fragen: Welche Daten Vorstand sieht; ob Übungsleiter nur Termine der eigenen Sparte verwaltet.

### FR-005 Benutzerverwaltung durch Admin · Soll · Umgesetzt

Admin verwaltet alle Benutzerkonten.

- Benutzer einsehen, Rollen vergeben/ändern, Kontostatus erkennen
- Konto löschen mit doppelter Bestätigung (DSGVO-konform, Inhalte bleiben als „gelöscht" erhalten)
- Konto kann nicht durch den Benutzer selbst gelöscht werden

Offene Fragen: Ob Admin Aktivierungslinks erneut auslösen kann.

### FR-006 Eigenes Profil · Soll · Umgesetzt

Angemeldeter Benutzer kann eigene Profildaten einsehen und erlaubte Felder bearbeiten.

- Pflichtfelder: Vorname, Nachname, E-Mail-Adresse
- Passwort änderbar über Profil (aktuelles Passwort erforderlich, min. 8 Zeichen)
- Nach Passwortänderung bleibt Session aktiv

Offene Fragen: Ob E-Mail-Änderung erneut bestätigt werden muss.

### FR-007 Registrierung · Muss · Umgesetzt

Neue Benutzer können sich selbst registrieren.

- Formular: Vorname, Nachname, E-Mail, Passwort (min. 8 Zeichen), Passwort-Wiederholung
- Doppelte E-Mail-Adressen werden abgelehnt
- Nach Registrierung: Hinweis auf nächsten Schritt (E-Mail prüfen, auf Freischaltung warten)

### FR-008 Passwort zurücksetzen · Muss · Umgesetzt

Benutzer kann vergessenes Passwort über E-Mail-Link zurücksetzen (Link gültig 1 Stunde).

### FR-009 Abmelden · Muss · Umgesetzt

Benutzer kann sich jederzeit abmelden. Session wird serverseitig beendet, Weiterleitung zum Login.

### FR-010 Startseite · Muss · Umgesetzt

Nach dem Login wird eine Startseite mit Vereinsname, aktuellen News, nächsten Terminen und personalisierter Begrüßung angezeigt.

### FR-011 Vereinsnews · Soll · Teilweise umgesetzt

News vom Vereinsblog werden chronologisch angezeigt. Artikelansicht inline in der App noch offen.

- Jede News zeigt: Titel, Datum, Vorschaubild, Kurztext
- Artikel öffnet sich in der App (nicht im Browser)

### FR-012 Vereinstermine einsehen · Muss · Umgesetzt

Alle angemeldeten Benutzer sehen Termine mit Datum, Titel, Beschreibung und Sparte. Filterbar nach Tauchsparte (Allgemein, Tauchen, Hockey, Rugby).

### FR-013 Termine verwalten · Soll · Umgesetzt

Admin, Vorstand und Übungsleiter können Termine anlegen, bearbeiten und absagen. Datum/Uhrzeit über nativen Picker. Abgesagte Termine sind als solche erkennbar.

Offene Fragen: Ob Übungsleiter nur Termine der eigenen Sparte verwalten darf.

### FR-014 Terminanmeldung · Soll · Offen

Mitglieder können sich zu Terminen an- und abmelden. Teilnehmerliste ist für alle einsehbar.

- Anmeldung nach Terminablauf nicht mehr möglich
- Optional: maximale Teilnehmerzahl je Termin

### FR-015 Tauchsparten verwalten · Soll · Umgesetzt

Admin kann Tauchsparten anlegen, umbenennen und löschen (nur wenn keine Termine zugeordnet). Sparten gelten systemweit.

### FR-016 Push-Benachrichtigungen · Muss · Umgesetzt

App fordert beim ersten Start Berechtigung an. Push-Tokens werden in der Datenbank gespeichert und beim Abmelden entfernt. Funktioniert auch bei geschlossener App (iOS und Android). Web optional.

- Benutzer kann Push-Benachrichtigungen im Profil global und je Typ (Chat, Termine, Umfragen) steuern

### FR-017 Push-Benachrichtigung bei Neuregistrierung · Soll · Umgesetzt

Alle Admins erhalten eine Push-Benachrichtigung wenn sich ein neuer Benutzer registriert. Nachricht enthält Vor- und Nachname. Tipp öffnet App im Verwaltungsbereich.

Offene Fragen: Ob Vorstand ebenfalls benachrichtigt werden soll.

### FR-018 E-Mail-Benachrichtigungen · Kann · Offen

Benutzer erhalten E-Mails bei: Registrierung (Aktivierungslink), Freischaltung, Passwort-Zurücksetzen. Abbestellbar im Profil.

Offene Fragen: Ob weitere Ereignisse (neue Termine etc.) Benachrichtigungen auslösen sollen.

### FR-019 Notrufnummern · Soll · Umgesetzt

Tauchrelevante Notrufnummern (Notruf 112, DAN Europe, Druckkammer) ohne Login einsehbar. Tipp auf Eintrag öffnet Telefon-Wähler. Admin kann Einträge pflegen.

Offene Fragen: Ob Druckkammer-Nummern regional gefiltert werden sollen.

### FR-020 Preisliste Vereinsheim · Soll · Umgesetzt

Preisliste für Getränke/Snacks, nach Kategorie gruppiert. Admin pflegt Einträge und PayPal-Link. Tipp auf Link öffnet PayPal-App oder Browser.

Offene Fragen: Ob Kategorien frei definierbar oder fest vorgegeben sein sollen.

### FR-021 Octopost (Vereinszeitschrift) · Soll · Umgesetzt

PDF-Archiv der Vereinszeitschrift. Alle Mitglieder können Ausgaben öffnen. Admin lädt neue Ausgaben hoch und kann Ausgaben löschen. PDFs nur für angemeldete Benutzer abrufbar.

- Liste chronologisch sortiert (neueste zuerst), Eintrag zeigt Titel, Monat, Jahr
- PDF öffnet im nativen Viewer oder Browser via signierter URL

### FR-022 Trainingsplan · Soll · Umgesetzt

Admin, Vorstand und Übungsleiter pflegen Trainer-Einteilungen (Name, Datum, optionale Bemerkung). Alle Mitglieder können nur lesen. Chronologisch sortiert. Ein Trainer pro Termin, keine Spartenfilterung.

### FR-023 Threadbasierter Chat · Soll · Offen

Vereinsinterne Kommunikation in Kanälen (Allgemein + spartenbezogene Kanäle). Nachrichten mit Thread-Antworten in Echtzeit (Supabase Realtime).

- Admin: Kanäle und Nachrichten verwalten; Mitglieder: eigene Nachrichten löschen
- Ungelesene Nachrichten erkennbar

Offene Fragen: Rollenbasierte Kanal-Einschränkungen; Dateianhänge; Nachrichtenaufbewahrungsfrist; Privatchat.

### FR-024 Umfragen und Abstimmungen · Soll · Offen

Admin, Vorstand und Übungsleiter erstellen Umfragen (Frage, Antwortoptionen, optionales Enddatum). Jedes Mitglied stimmt einmal ab. Ergebnis nach eigener Stimmabgabe sichtbar. Ersteller kann Umfrage vorzeitig beenden.

Offene Fragen: Anonymität; Zielgruppen nach Rolle/Sparte; Einfach- vs. Mehrfachauswahl; Integration in Chat.

### FR-025 Mitgliederliste · Soll · Offen

Liste aller aktiven Mitglieder (Vorname, Nachname, Rollen, Profilbild) alphabetisch sortiert. Mitglieder laden eigenes Profilbild hoch. Admin kann Profilbilder entfernen. Nicht freigeschaltete Konten erscheinen nicht.

Offene Fragen: Detailansicht je Mitglied; Filter nach Sparte/Rolle; Datenschutz-Sichtbarkeit.

### FR-026 Seebedingungen · Soll · Offen

Mitglieder tragen aktuelle Seebedingungen ein (Wassertemperatur, Sichtweite, Kommentar, bis zu 3 Fotos). Aktueller Stand und letzten 10 Einträge als Verlauf sichtbar. Admin kann Einträge/Bilder löschen. Tauchplatzkarte later einbettbar.

Offene Fragen: Tiefenspezifische Messwerte; Benachrichtigungen bei neuen Einträgen.

### FR-027 Bildergalerie · Kann · Offen

Mitglieder teilen Fotos in Alben (nach Veranstaltung/Datum). Vollbildansicht. Admin verwaltet Alben. Bilder in Supabase Storage.

Offene Fragen: Wer Alben anlegen darf; Kommentare/Likes; Speicherlimit; automatische Komprimierung.

### FR-028 Materialbuchung · Soll · Offen

Mitglieder buchen Vereinsausrüstung (Regler, Flaschen, Jackets) für einen Zeitraum. Verfügbarkeit in Echtzeit sichtbar. Admin verwaltet Gegenstände. Admin/Vorstand sehen und stornieren alle Buchungen.

Offene Fragen: Maximale Buchungsdauer; Warteliste; Zustandserfassung (defekt/Wartung); Kopplung an Termine.

## Bezug zu anderen Dokumenten

- `PROJEKTPLAN.md` – technische Planung und Architektur
- `roles.md` – Rollen- und Rechtemodell
