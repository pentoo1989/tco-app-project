# Funktionale Anforderungen

Stand: 08.04.2026

## Zweck

Diese Datei sammelt die funktionalen Anforderungen fuer die App.

Sie dient als fachliche Arbeitsgrundlage fuer Planung, Implementierung und Priorisierung. Technische Entscheidungen gehoeren primaer in den Projektplan. Rollen und Berechtigungen werden fachlich in `roles.md` ergaenzt.

## Abgrenzung

Diese Datei enthaelt:

- Funktionale Anforderungen
- Fachliche Regeln
- Benutzerbezogene Anwendungsfaelle
- Offene fachliche Punkte

Diese Datei enthaelt nicht primaer:

- Technische Architekturdetails
- Framework-Entscheidungen
- Build- oder Infrastrukturthemen

Verbindliche technische Rahmenbedingung:

- Authentifizierung und Datenablage erfolgen ueber Supabase.

## Arbeitsweise

Jede Anforderung sollte moeglichst eindeutig, testbar und fachlich nachvollziehbar formuliert sein.

Empfohlene Struktur pro Anforderung:

- ID
- Titel
- Beschreibung
- Prioritaet
- Akzeptanzkriterien
- Offene Fragen

Prioritaeten:

- Muss
- Soll
- Kann

Statuswerte fuer spaetere Pflege:

- Offen
- In Klaerung
- Freigegeben
- Umgesetzt

## App-Identitaet

Die App ist die digitale Vereinsapp des **TCO Weinheim** (Tauch-Club Weinheim). Der Vereinsname soll in der App sichtbar sein, insbesondere auf der Startseite.

## Aktueller Scope

Die App soll auf iOS, Android und im Webbrowser laufen. Der aktuell bekannte fachliche Kern umfasst:

- Benutzeranmeldung
- Account-Aktivierung per E-Mail-Link
- Rollen und Rechte
- Geschuetzte Bereiche je nach Rolle

Rahmenbedingung fuer Umsetzung:

- Supabase wird als zentrale Plattform fuer Auth und Datenpersistenz genutzt.

## Funktionale Anforderungen

### FR-000 Die App muss auf iOS, Android und im Webbrowser funktionieren

Prioritaet: Muss

Beschreibung:
Alle Funktionen der App muessen auf iOS, Android und im Webbrowser vollstaendig nutzbar sein. Plattformspezifische Einschraenkungen oder abweichendes Verhalten sind nicht akzeptabel, sofern nicht ausdruecklich dokumentiert und fachlich freigegeben.

Akzeptanzkriterien:

- Jede neue Funktion wird auf allen drei Plattformen getestet bevor sie als umgesetzt gilt
- Das UI-Layout ist auf allen Plattformen korrekt dargestellt und bedienbar
- Authentifizierung, Session-Management und Datenzugriff funktionieren auf allen Plattformen
- Plattformspezifische Abweichungen (z.B. native Picker, Dateiauswahl) sind dokumentiert und haben akzeptable Alternativen
- Es gibt keine Funktion, die nur auf einer oder zwei Plattformen verfuegbar ist, ohne explizite fachliche Begruendung

Status: Umgesetzt

### FR-001 Benutzer kann sich mit Username oder E-Mail anmelden

Prioritaet: Muss

Beschreibung:
Ein Benutzer soll sich mit Passwort anmelden koennen. Als Login-Kennung soll entweder der Username oder die E-Mail-Adresse akzeptiert werden.

Akzeptanzkriterien:

- Das Login-Formular akzeptiert Username oder E-Mail in einem Eingabefeld
- Das Login-Formular besitzt ein separates Passwortfeld
- Eine erfolgreiche Anmeldung fuehrt zu einer gueltigen Session
- Eine fehlgeschlagene Anmeldung liefert eine verstaendliche Fehlermeldung
-  die Anmeldung soll dauerhaft eingeloggt bleiben koennen
- Es sollen Rate-Limits oder Sperrmechanismen fachlich sichtbar sein


Status: Umgesetzt

### FR-002 Benutzerkonto muss vor Nutzung freigeschaltet werden

Prioritaet: Muss

Beschreibung:
Ein Benutzerkonto darf erst nach Aktivierung ueber einen E-Mail-Link und anschliessender Freischaltung durch einen Admin oder Vorstand vollstaendig genutzt werden.

Akzeptanzkriterien:

- Benutzer kann sich selbst registrieren
- Nach Registrierung wird ein Aktivierungslink per E-Mail versendet
- Ein nicht per E-Mail aktiviertes Konto kann sich nicht anmelden
- Nach E-Mail-Aktivierung ist das Konto noch gesperrt bis zur manuellen Freischaltung
- Admin oder Vorstand kann ausstehende Konten einsehen und freischalten
- Ein nicht freigeschaltetes Konto erhaelt keinen Zugriff auf geschuetzte Bereiche
- Ungueltige oder abgelaufene Aktivierungslinks werden sauber behandelt
- Ein Aktivierungslink ist 2 Tage gueltig

Status: Umgesetzt

### FR-003 Benutzerrolle muss Teil des Kontos sein

Prioritaet: Muss

Beschreibung:
Jedes Benutzerkonto muss mindestens eine primaere Rolle besitzen. Aktuell sind die Rollen Admin, Mitglied, Vorstand und Uebungsleiter vorgesehen. Zusaetzliche Rollen koennen spaeter moeglich sein.

Akzeptanzkriterien:

- Jedem Benutzer ist mindestens eine primaere Rolle zugeordnet
- Die Rolle ist nach erfolgreicher Anmeldung in der Session verfuegbar
- Rollen koennen fuer Berechtigungsentscheidungen verwendet werden
- Ein Benutzer ohne zugewiesene Rolle kann sich nicht einloggen und erhaelt eine verstaendliche Fehlermeldung

Offene Fragen:

- Ob Mehrfachrollen von Beginn an unterstuetzt werden sollen
- Ob Rollen manuell oder regelbasiert vergeben werden

Status: Umgesetzt

### FR-004 Geschuetzte Bereiche muessen nach Rolle gesteuert werden

Prioritaet: Muss

Beschreibung:
Bestimmte Screens, Aktionen und Verwaltungsfunktionen duerfen nur fuer dafuer berechtigte Rollen verfuegbar sein.

Akzeptanzkriterien:

- Nicht berechtigte Benutzer koennen geschuetzte Bereiche nicht aufrufen
- Nicht berechtigte Aktionen werden verhindert
- Berechtigungen orientieren sich an den in `roles.md` beschriebenen Rollen
- Ein nicht aktiviertes Konto erhaelt keinen regulaeren Zugriff auf geschuetzte Bereiche

Offene Fragen:

- Welche konkreten Screens und Aktionen im MVP geschuetzt werden muessen
- Welche Funktionen Vorstand und Uebungsleiter in Version 1 tatsaechlich erhalten

Status: Umgesetzt

### FR-005 Admin kann Benutzer verwalten

Prioritaet: Soll

Beschreibung:
Ein Admin soll Benutzerkonten verwalten koennen.

Akzeptanzkriterien:

- Admin kann Benutzer einsehen
- Admin kann Benutzer anlegen oder zur Anlage vorbereiten
- Admin kann Rollen vergeben oder aendern
- Admin kann Kontostatus erkennen, zum Beispiel aktiv, nicht aktiviert oder gesperrt

Offene Fragen:

- Ob Admin Benutzer direkt deaktivieren oder loeschen darf
- Ob Admin Aktivierungslinks erneut ausloesen kann

Status: Umgesetzt

### FR-006 Mitglied kann eigenes Profil verwalten

Prioritaet: Soll

Beschreibung:
Ein angemeldeter Benutzer soll sein eigenes Profil einsehen und bearbeiten koennen, soweit dies fachlich freigegeben ist.

Akzeptanzkriterien:

- Benutzer kann eigene Profildaten einsehen
- Benutzer kann erlaubte Profildaten aendern
- Nicht erlaubte Felder sind nicht bearbeitbar
- Verpflichtende Felder: E-Mail-Adresse, Vorname, Nachname

Offene Fragen:

- Ob Aenderungen an der E-Mail-Adresse erneut bestaetigt werden muessen

Status: Umgesetzt

### FR-007 Vorstand erhaelt erweiterte Einsichts- oder Verwaltungsrechte

Prioritaet: Soll

Beschreibung:
Die Rolle Vorstand soll gegenueber Mitgliedern erweiterte fachliche Rechte erhalten. Der genaue Umfang ist noch zu praezisieren.

Akzeptanzkriterien:

- Vorstand hat mindestens einen klar abgegrenzten erweiterten Funktionsbereich
- Rechte sind von Admin-Rechten getrennt
- Rechte sind in `roles.md` dokumentiert und fachlich freigegeben

Offene Fragen:

- Welche Organisationsdaten sichtbar sein sollen
- Welche Verwaltungsaktionen erlaubt sein sollen

Status: In Klaerung

### FR-008 Uebungsleiter kann fachliche Bereiche fuer Gruppen oder Termine pflegen

Prioritaet: Soll

Beschreibung:
Die Rolle Uebungsleiter soll eigene Gruppen-, Trainings- oder Terminbereiche verwalten koennen. Der genaue Zuschnitt ist noch zu klaeren.

Akzeptanzkriterien:

- Uebungsleiter hat mindestens einen klar abgegrenzten fachlichen Verantwortungsbereich
- Rechte sind von Admin-Rechten getrennt
- Rechte sind in `roles.md` dokumentiert und fachlich freigegeben

Offene Fragen:

- Ob Teilnehmerlisten bearbeitet werden duerfen
- Ob Termine erstellt, bearbeitet oder nur eingesehen werden duerfen

Status: In Klaerung

### FR-009 Startseite ist nach dem Login sichtbar

Prioritaet: Muss

Beschreibung:
Nach erfolgreicher Anmeldung wird dem Benutzer eine Startseite angezeigt. Diese Seite dient als zentraler Einstiegspunkt in die App und repraesentiert den Tauch-Club TCO Weinheim.

Akzeptanzkriterien:

- Die Startseite zeigt den Vereinsnamen TCO Weinheim sichtbar an
- Die Startseite ist fuer alle angemeldeten Benutzerrollen zugaenglich
- Von der Startseite aus koennen andere Bereiche der App navigiert werden
- Welche Inhalte sollen auf der Startseite abgebildet sein: aktuelle News, naechste Termine, Willkommenstext
-  die Startseite soll personalisiert sein (z.B. Begruessung mit Vorname)

Status: Umgesetzt

### FR-010 Benutzer kann Vereinstermine einsehen

Prioritaet: Muss

Beschreibung:
Angemeldete Benutzer sehen eine Uebersicht aller Vereinstermine. Termine koennen nach Tauchsparten gefiltert werden, sodass Mitglieder nur fuer sie relevante Termine sehen.

Akzeptanzkriterien:

- Terminliste zeigt Datum, Titel, Beschreibung und Sparte
- Termine koennen nach Tauchsparte gefiltert werden
- Initiale Tauchsparten: Allgemein, Tauchen, Hockey, Rugby
- Tauchsparten sind durch Admin administrierbar (anlegen, umbenennen, loeschen)
- Vergangene und kuenftige Termine sind unterscheidbar
- Alle angemeldeten Benutzer koennen Termine einsehen

Status: Umgesetzt

### FR-011 Benutzer kann sich fuer Termine anmelden

Prioritaet: Soll

Beschreibung:
Angemeldete Mitglieder koennen sich zu Terminen an- und abmelden. Die Teilnehmerliste ist fuer alle angemeldeten Benutzer einsehbar.

Akzeptanzkriterien:

- Benutzer kann sich fuer einen Termin anmelden
- Benutzer kann eine Anmeldung wieder zurueckziehen
- Teilnehmerliste (Namen der Angemeldeten) ist fuer alle angemeldeten Benutzer einsehbar
- Die Anzahl der Anmeldungen ist je Termin sichtbar
- Optional: maximale Teilnehmerzahl je Termin konfigurierbar
- Anmeldung nach Ablauf des Termins nicht mehr moeglich

Status: Offen

### FR-012 Admin, Vorstand und Uebungsleiter koennen Termine anlegen und verwalten

Prioritaet: Soll

Beschreibung:
Admin, Vorstand und Uebungsleiter koennen Termine erstellen, bearbeiten und absagen. Mitglieder sehen die jeweils aktuellen Termindaten.

Akzeptanzkriterien:

- Berechtigte Rollen koennen einen neuen Termin anlegen mit Titel, Datum, Beschreibung und Sparte
- Berechtigte Rollen koennen bestehende Termine bearbeiten
- Berechtigte Rollen koennen Termine absagen
- Abgesagte Termine sind fuer Mitglieder als abgesagt erkennbar
- Datum und Uhrzeit werden ueber einen nativen Datums- und Zeitpicker eingegeben, nicht per Freitexteingabe

Offene Fragen:

- Ob Uebungsleiter nur Termine der eigenen Sparte verwalten darf

Status: Umgesetzt

### FR-013 Benutzer kann sich selbst registrieren

Prioritaet: Muss

Beschreibung:
Neue Benutzer koennen sich eigenstaendig ueber ein Registrierungsformular anmelden. Nach der Registrierung erhalten sie einen Aktivierungslink per E-Mail. Die eigentliche Kontonutzung setzt die E-Mail-Bestaetigung und die manuelle Freischaltung durch einen Admin oder Vorstand voraus (siehe FR-002).

Akzeptanzkriterien:

- Das Registrierungsformular enthaelt: Vorname, Nachname, E-Mail-Adresse, Passwort, Passwort-Wiederholung
- Das Passwort muss einem Mindeststandard genuegen (mindestens 8 Zeichen)
- Die E-Mail-Adresse muss ein gueltiges Format haben
- Nach erfolgreicher Registrierung wird ein Aktivierungslink per E-Mail versendet
- Doppelte E-Mail-Adressen werden abgelehnt mit einer verstaendlichen Fehlermeldung
- Der Benutzer wird nach der Registrierung ueber den naechsten Schritt informiert (E-Mail pruefen, auf Freischaltung warten)

Status: Umgesetzt

### FR-014 Benutzer kann sein Passwort zuruecksetzen

Prioritaet: Muss

Beschreibung:
Ein Benutzer, der sein Passwort vergessen hat, kann ueber die Login-Seite einen Passwort-Zuruecksetzen-Prozess starten. Der Prozess laeuft ueber einen per E-Mail zugestellten Link.

Akzeptanzkriterien:

- Auf der Login-Seite gibt es eine sichtbare Option "Passwort vergessen"
- Benutzer gibt seine E-Mail-Adresse ein und bestaetigt
- Eine E-Mail mit einem Zuruecksetzen-Link wird versendet
- Der Link fuehrt auf einen Screen, auf dem ein neues Passwort gesetzt werden kann
- Ein abgelaufener oder ungueltig verwendeter Link wird sauber behandelt
- Nach erfolgreichem Zuruecksetzen kann sich der Benutzer mit dem neuen Passwort anmelden
- Der Link ist maximal 1 Stunde gueltig

Status: Umgesetzt

### FR-015 Benutzer kann sein Passwort aendern

Prioritaet: Soll

Beschreibung:
Ein angemeldeter Benutzer kann sein Passwort ueber das eigene Profil aendern, ohne einen Zuruecksetzen-Link zu benoetigen.

Akzeptanzkriterien:

- Im Profilereich gibt es eine Option zum Passwort aendern
- Benutzer muss das aktuelle Passwort bestaetigen bevor ein neues gesetzt werden kann
- Das neue Passwort muss dem Mindeststandard genuegen (mindestens 8 Zeichen)
- Eingabe des neuen Passworts und Wiederholung sind Pflicht
- Nach erfolgreicher Aenderung bleibt die Session aktiv

Status: Umgesetzt

### FR-016 Admin kann Tauchsparten verwalten

Prioritaet: Soll

Beschreibung:
Ein Admin kann die verfuegbaren Tauchsparten der App pflegen. Diese Sparten werden fuer die Filterung von Terminen (FR-010, FR-012) und spaeter weiteren Bereichen verwendet.

Akzeptanzkriterien:

- Admin kann neue Tauchsparten anlegen (Name, ggf. Beschreibung)
- Admin kann bestehende Tauchsparten umbenennen
- Admin kann Tauchsparten loeschen, sofern sie keinen Terminen mehr zugeordnet sind
- Initiale Tauchsparten: Allgemein, Tauchen, Hockey, Rugby
- Tauchsparten sind systemweit fuer alle berechtigten Bereiche (Termine, etc.) verwendbar

Status: Umgesetzt

### FR-017 Benutzer erhaelt E-Mail-Benachrichtigungen bei relevanten Ereignissen

Prioritaet: Kann

Beschreibung:
Benutzer sollen bei fachlich relevanten Ereignissen automatisch per E-Mail informiert werden, sofern sie dem nicht widersprochen haben.

Akzeptanzkriterien:

- Nach Registrierung: Aktivierungslink
- Nach Freischaltung durch Admin: Bestaetigung, dass das Konto nun nutzbar ist
- Nach Passwort-Zuruecksetzen: Bestaetigung der erfolgreichen Aenderung
- Benutzer kann E-Mail-Benachrichtigungen im Profil deaktivieren

Offene Fragen:

- Ob weitere Ereignisse (z.B. neue Termine, Anmeldung bestaetigt) Benachrichtigungen ausloesen sollen

Status: Offen

### FR-018 Benutzer kann aktuelle Vereinsnews einsehen

Prioritaet: Soll

Beschreibung:
Angemeldete Benutzer koennen aktuelle Neuigkeiten und Nachrichten des Vereins auf der Startseite lesen. Die News werden direkt von der Vereinswebsite tco-weinheim.de geladen und chronologisch angezeigt.

Akzeptanzkriterien:

- Die Startseite zeigt die aktuellen News aus dem Vereins-Blog
- Jede News zeigt: Titel, Datum, Vorschaubild (falls vorhanden) und Kurztext
- Ein Tipp auf eine News oeffnet den vollstaendigen Artikel direkt in der App (nicht im Browser)
- Der Artikel wird inline dargestellt mit Titel, Datum, Bild (falls vorhanden) und vollstaendigem Inhalt
- Ein Zurueck-Button fuehrt zur Newsübersicht
- News werden chronologisch sortiert (neueste zuerst)
- Ladefehler werden dem Benutzer verstaendlich angezeigt
- Die News funktionieren auf iOS, Android und Web

Getroffene technische Entscheidung:

- Datenquelle: WordPress REST API von tco-weinheim.de (`/wp-json/wp/v2/posts?_embed`)
- Begruendung: Liefert direkt JSON, kein XML-Parser noetig, kein zusaetzliches Package erforderlich
- Kein eigener Backend-Proxy: Die API ist oeffentlich zugaenglich ohne Authentifizierung
- Alternativen geprueft: RSS-Feed (`/feed`) ebenfalls verfuegbar, aber REST API bevorzugt

Status: Teilweise umgesetzt – Artikelansicht in der App offen

### FR-019 Benutzer kann sich abmelden

Prioritaet: Muss

Beschreibung:
Ein angemeldeter Benutzer kann sich jederzeit aus der App abmelden. Die Session wird dabei vollstaendig beendet.

Akzeptanzkriterien:

- Es gibt eine klar sichtbare Abmeldefunktion
- Nach dem Abmelden ist keine geschuetzte Funktion mehr zugaenglich
- Die Session wird serverseitig beendet
- Nach dem Abmelden wird der Benutzer auf den Login-Bereich weitergeleitet

Status: Umgesetzt

### FR-020 Admin kann Benutzerkonto loeschen

Prioritaet: Soll

Beschreibung:
Nur ein Admin kann ein Benutzerkonto vollstaendig loeschen. Mitglieder koennen keine Eigenloeschung durchfuehren.

Akzeptanzkriterien:

- Admin kann ein Benutzerkonto aus der Verwaltung heraus loeschen
- Vor dem Loeschen erfolgt eine doppelte Bestaetigung per Popup
- Ein geloeschtes Konto ist nicht wiederherstellbar
- Nach dem Loeschen kann sich der betroffene Benutzer nicht mehr anmelden
- Loeschung erfolgt DSGVO-konform (personenbezogene Daten werden entfernt)
- Inhalte des geloeschten Benutzers bleiben erhalten, werden aber als "geloescht" angezeigt

Status: Umgesetzt

### FR-021 Trainingsplan mit Trainer-Einteilung

Prioritaet: Soll

Beschreibung:
Admin, Vorstand und Uebungsleiter koennen einen Trainingsplan pflegen, der die Einteilung von Trainern zu bestimmten Terminen abbildet. Alle angemeldeten Benutzer koennen den Plan einsehen. Das Anlegen, Bearbeiten und Loeschen von Eintraegen ist nur fuer berechtigte Rollen moeglich.

Akzeptanzkriterien:

- Der Trainingsplan ist ueber ein aufklappbares Menue in der App erreichbar
- Die Listenansicht zeigt pro Eintrag: Datum, Wochentag, Monat, Name des Trainers, Bemerkung (optional)
- Eintraege sind chronologisch sortiert
- Berechtigte Rollen (Admin, Vorstand, Uebungsleiter) koennen neue Eintraege anlegen
- Ein neuer Eintrag enthaelt: Name (Pflicht), Datum (Pflicht), Bemerkung (optional)
- Berechtigte Rollen koennen Eintraege bearbeiten und loeschen
- Nicht berechtigte Rollen (Mitglied) koennen den Plan nur lesen, nicht bearbeiten
- Die Funktion ist auf iOS, Android und Web verfuegbar
- Ob der Trainingsplan spartenspezifisch gefiltert werden soll: nein
- Ob mehrere Trainer pro Termin eingetragen werden koennen: nein

Status: Umgesetzt

### FR-022 Admin erhaelt Push-Benachrichtigung bei neuer Kontoregistrierung

Prioritaet: Soll

Beschreibung:
Wenn sich ein neuer Benutzer registriert und auf Freischaltung wartet, sollen alle Admins eine Push-Benachrichtigung auf ihrem Geraet erhalten. Ziel ist, dass Admins zeitnah reagieren koennen, ohne die App aktiv oeffnen zu muessen. Setzt FR-032 voraus.

Akzeptanzkriterien:

- Nach erfolgreicher Registrierung eines neuen Benutzers erhalten alle Admins eine Push-Benachrichtigung
- Die Benachrichtigung enthaelt Vorname und Nachname des neuen Benutzers
- Ein Tipp auf die Benachrichtigung oeffnet die App im Verwaltungsbereich
- Die Benachrichtigung wird nur an Benutzer mit der Rolle Admin gesendet
- Die Benachrichtigung funktioniert auf iOS und Android
- Admins erhalten die Benachrichtigung auch wenn die App im Hintergrund oder geschlossen ist

Offene Fragen:

- Ob Vorstand ebenfalls benachrichtigt werden soll

Status: Umgesetzt

### FR-023 Benutzer kann tauchrelevante Notrufnummern einsehen

Prioritaet: Soll

Beschreibung:
Die App stellt eine Liste wichtiger Notrufnummern bereit, die fuer Taucheinsaetze und Notfaelle relevant sind. Die Nummern sind ohne Login erreichbar und koennen direkt aus der App angerufen werden.

Akzeptanzkriterien:

- Die Notrufnummern sind ohne Anmeldung erreichbar
- Jeder Eintrag zeigt: Name der Stelle, Telefonnummer, optionale Beschreibung
- Ein Tipp auf eine Nummer oeffnet direkt den Telefon-Waehler
- Initiale Eintraege: Notruf (112), DAN Europe Notruf, naechste Druckkammer
- Admin kann Eintraege verwalten (anlegen, bearbeiten, loeschen)
- Die Funktion ist auf iOS, Android und Web verfuegbar

Offene Fragen:

- Ob die Druckkammer-Nummern regional (nach Standort) gefiltert werden sollen
- Ob die Liste fest im Code hinterlegt oder per Datenbank pflegbar sein soll

Status: Umgesetzt

### FR-024 Preisliste fuer das Vereinsheim

Prioritaet: Soll

Beschreibung:
Die App zeigt eine Preisliste fuer Getraenke und Snacks im Vereinsheim. Die Eintraege sind durch einen Admin pflegbar. Zusaetzlich ist ein Link zum PayPal-Konto des Vereins vorhanden, damit Mitglieder bequem bezahlen koennen.

Akzeptanzkriterien:

- Die Preisliste ist fuer alle angemeldeten Benutzer einsehbar
- Jeder Eintrag zeigt: Artikelname und Preis in Euro
- Eintraege koennen nach Kategorie gruppiert werden (z.B. Getraenke, Snacks)
- Admin kann Eintraege anlegen, bearbeiten und loeschen
- Admin kann den PayPal-Link hinterlegen und aendern
- Ein Tipp auf den PayPal-Link oeffnet die PayPal-App oder den Browser
- Die Seite ist ueber das Seitenmenue erreichbar
- Die Funktion ist auf iOS, Android und Web verfuegbar

Offene Fragen:

- Ob Kategorien frei definierbar oder fest vorgegeben sein sollen

Status: Umgesetzt

### FR-025 Benutzer kann die Vereinszeitschrift Octopost einsehen

Prioritaet: Soll

Beschreibung:
Die App stellt die monatliche Vereinszeitschrift "Octopost" als PDF-Archiv bereit. Alle angemeldeten Benutzer koennen verfuegbare Ausgaben einsehen und oeffnen. Admins koennen neue Ausgaben direkt in der App hochladen.

Akzeptanzkriterien:

- Die Octopost-Seite ist ueber das Seitenmenue fuer alle angemeldeten Benutzer erreichbar
- Die Seite zeigt eine chronologisch sortierte Liste aller verfuegbaren Ausgaben (neueste zuerst)
- Jeder Eintrag zeigt: Titel (z.B. "Octopost April 2026"), Monat und Jahr
- Ein Tipp auf eine Ausgabe oeffnet das PDF im nativen Viewer des Geraets oder im Browser
- Admin kann eine neue Ausgabe hochladen: Dateiauswahl (PDF), Monat und Jahr angeben, speichern
- Admin kann eine Ausgabe loeschen
- PDFs sind nur fuer angemeldete Benutzer abrufbar (kein oeffentlicher Zugriff)
- Die Funktion ist auf iOS, Android und Web verfuegbar

Getroffene technische Entscheidungen:

- Ablage der PDF-Dateien: Supabase Storage Bucket "octopost" (privat, signierte URLs)
- Metadaten (Titel, Monat, Jahr, Dateiname, Hochladedatum): Supabase Tabelle "octopost_issues"
- Upload durch Admin direkt in der App via expo-document-picker (PDF-Filter)
- Anzeige: Oeffnen per Linking.openURL mit signierter URL (plattformuebergreifend)
- Alternativen geprueft: Manueller Upload ueber Supabase Dashboard abgelehnt, da nicht fuer normale Admins geeignet
- Ob aeltere Ausgaben archiviert oder nach einer bestimmten Anzahl automatisch entfernt werden sollen: nein
- Ob eine Vorschau (Titelbild) der Ausgabe in der Liste angezeigt werden soll: nein

Status: Umgesetzt

### FR-026 Threadbasierter Chat als vereinsinterne Kommunikationsplattform

Prioritaet: Soll

Beschreibung:
Die App soll eine eigene Kommunikationsplattform bereitstellen, die WhatsApp-Gruppen, E-Mail-Verteiler und Excel-Planung schrittweise ablöst. Kern ist ein threadbasierter Chat, strukturiert in Kanaelen ähnlich einer WhatsApp Community: ein Hauptkanal fuer alle Mitglieder sowie thematische Untergruppen (z.B. je Sparte). Innerhalb eines Kanals koennen Mitglieder Nachrichten schreiben und auf bestehende Nachrichten antworten (Thread).

Akzeptanzkriterien:

- Es gibt mindestens einen allgemeinen Kanal fuer alle Mitglieder
- Weitere Kanaele koennen nach Thema oder Sparte organisiert werden (z.B. Tauchen, Hockey, Rugby, Orga)
- Jeder Kanal zeigt eine chronologische Nachrichtenliste
- Mitglieder koennen Nachrichten in einem Kanal schreiben
- Auf eine Nachricht kann geantwortet werden (Thread-Antwort), sichtbar als eingerueckter Unterdialog
- Neue Nachrichten und Antworten erscheinen in Echtzeit ohne manuelles Neuladen
- Ungelesene Nachrichten sind erkennbar (z.B. Badge oder Markierung)
- Admin kann Kanaele anlegen, umbenennen und loeschen
- Admin kann Nachrichten loeschen
- Mitglieder koennen eigene Nachrichten loeschen
- Die Funktion ist auf iOS, Android und Web verfuegbar

Offene Fragen:

- Ob Kanaele rollenbasiert eingeschraenkt werden sollen (z.B. nur Uebungsleiter sehen den Trainer-Kanal)
- Ob Dateianhänge (Bilder, PDFs) in Nachrichten erlaubt sein sollen
- Ob eine Pushbenachrichtigung bei neuen Nachrichten ausgeloest werden soll
- Wie lange Nachrichten aufbewahrt werden (unbegrenzt oder mit Aufbewahrungsfrist)
- Ob ein direkter Privatchat zwischen zwei Mitgliedern gewuenscht ist

Getroffene technische Entscheidung:

- Echtzeit-Synchronisation ueber Supabase Realtime (bestehende Infrastruktur)

Status: Umgesetzt

### FR-027 Umfragen- und Abstimmungsfunktion

Prioritaet: Soll

Beschreibung:
Berechtigte Rollen koennen Umfragen und Abstimmungen erstellen, an denen alle oder bestimmte Mitglieder teilnehmen koennen. Ziel ist es, Entscheidungen und Planungen direkt in der App abzubilden und externe Tools (z.B. WhatsApp-Abstimmungen, E-Mail-Rundfragen) abzuloesen.

Akzeptanzkriterien:

- Admin, Vorstand und Uebungsleiter koennen eine Umfrage erstellen mit: Frage, Antwortoptionen (mind. 2), optionalem Enddatum
- Mitglieder koennen an einer offenen Umfrage teilnehmen und eine oder mehrere Optionen waehlen
- Jedes Mitglied kann pro Umfrage nur einmal abstimmen
- Das Abstimmungsergebnis (Anzahl Stimmen je Option) ist nach der eigenen Stimmabgabe sichtbar
- Abgeschlossene Umfragen (Enddatum erreicht oder manuell beendet) zeigen das Endergebnis
- Der Ersteller kann eine Umfrage vorzeitig beenden
- Admin kann Umfragen loeschen
- Umfragen sind ueber einen eigenen Bereich oder im Kontext eines Termins erreichbar
- Die Funktion ist auf iOS, Android und Web verfuegbar

Offene Fragen:

- Ob Umfragen anonym sein koennen oder die Stimmabgabe namentlich nachvollziehbar sein soll
- Ob Umfragen an bestimmte Rollen oder Sparten adressiert werden koennen
- Ob Einfach- und Mehrfachauswahl konfigurierbar sein soll
- Ob Umfragen im Chat (FR-026) eingebettet werden sollen oder als eigenstaendiger Bereich

Status: Offen

### FR-028 Mitgliederliste mit Profilbild

Prioritaet: Soll

Beschreibung:
Angemeldete Benutzer koennen eine Liste aller aktiven Vereinsmitglieder einsehen. Jedes Mitglied kann optional ein Profilbild hinterlegen. Die Liste dient der Orientierung innerhalb des Vereins und unterstuetzt den Gemeinschaftsgedanken.

Akzeptanzkriterien:

- Die Mitgliederliste ist fuer alle angemeldeten Benutzer einsehbar
- Jeder Eintrag zeigt: Vorname, Nachname, Rolle(n) im Verein, Profilbild (falls vorhanden, sonst Platzhalter)
- Die Liste ist alphabetisch sortiert
- Jedes Mitglied kann ein eigenes Profilbild hochladen und aendern
- Profilbilder werden in Supabase Storage abgelegt
- Admin kann Profilbilder entfernen
- Nicht freigeschaltete oder deaktivierte Konten erscheinen nicht in der Liste
- Die Funktion ist auf iOS, Android und Web verfuegbar

Offene Fragen:

- Ob eine Detailansicht je Mitglied gewuenscht ist (z.B. mit Kontaktdaten oder Spartenzugehoerigkeit)
- Ob die Liste nach Sparte oder Rolle filterbar sein soll
- Welche Profilfelder oeffentlich sichtbar sein sollen (Datenschutz)
- Ob Mitglieder selbst steuern koennen, welche Informationen sichtbar sind

Status: Offen

### FR-029 Aktuelle Seebedingungen

Prioritaet: Soll

Beschreibung:
Alle angemeldeten Benutzer koennen aktuelle Informationen zum Vereinssee einsehen und selbst aktualisieren: Wassertemperatur, Sichtweite, Fotos und sonstige Hinweise. Zusaetzlich soll spaeter eine Tauchplatzkarte eingebettet werden koennen. Ziel ist eine lebendige, von der Community gepflegte Infoseite zum See.

Akzeptanzkriterien:

- Die Seite zeigt die zuletzt eingetragenen Bedingungen: Wassertemperatur (°C), Sichtweite (m), Freitextkommentar (optional), Datum und Uhrzeit des Eintrags sowie Name des Eintragers
- Jedes angemeldete Mitglied kann einen neuen Eintrag erstellen
- Ein neuer Eintrag ersetzt den aktuell angezeigten Stand (es gibt immer genau einen aktuellen Stand)
- Aeltere Eintraege sind als Verlauf einsehbar (z.B. die letzten 10 Eintraege)
- Mitglieder koennen Fotos zum Eintrag hochladen (optional, mind. 1, max. 3 Bilder)
- Admin kann beliebige Eintraege und Bilder loeschen
- Die Seite ist ueber das Menue erreichbar
- Die Funktion ist auf iOS, Android und Web verfuegbar
- Eine Tauchplatzkarte kann spaeter als Bild oder PDF eingebettet werden (Admin pflegt diese)

Offene Fragen:

- Ob Temperatur und Sichtweite in verschiedenen Tiefen erfasst werden sollen (z.B. Oberflaechentemperatur vs. Tiefentemperatur)
- Ob Benachrichtigungen bei neuen Eintraegen gewuenscht sind
- In welchem Format die Tauchplatzkarte vorliegen wird (Bild oder PDF)

Status: Offen

### FR-030 Bildergalerie

Prioritaet: Kann

Beschreibung:
Die App stellt eine Bildergalerie bereit, in der Vereinsmitglieder Fotos aus dem Vereinsleben teilen koennen. Bilder koennen in Alben oder nach Ereignissen organisiert werden.

Akzeptanzkriterien:

- Alle angemeldeten Benutzer koennen die Galerie einsehen
- Bilder sind in Alben organisiert (z.B. nach Veranstaltung oder Datum)
- Mitglieder koennen Bilder hochladen und einem Album zuordnen
- Admin, Vorstand und der Hochladende koennen Bilder loeschen
- Admin kann Alben anlegen, umbenennen und loeschen
- Bilder werden in Supabase Storage abgelegt
- Bilder koennen in einer Vollbildansicht betrachtet werden
- Die Funktion ist auf iOS, Android und Web verfuegbar

Offene Fragen:

- Ob alle Mitglieder Alben anlegen duerfen oder nur berechtigte Rollen
- Ob Bilder kommentiert oder mit "Gefaellt mir" markiert werden koennen
- Ob eine maximale Dateigroesse oder ein Speicherlimit je Mitglied gelten soll
- Ob Bilder automatisch komprimiert werden sollen

Status: Offen

### FR-031 Materialbuchung und Verfuegbarkeitsanzeige

Prioritaet: Soll

Beschreibung:
Mitglieder koennen Tauchausruestung des Vereins (z.B. Regler, Flaschen, Jackets) direkt in der App buchen. Die aktuelle Verfuegbarkeit ist fuer alle angemeldeten Benutzer jederzeit einsehbar. Ziel ist es, Doppelbuchungen und manuelle Abstimmungen per WhatsApp oder E-Mail zu vermeiden.

Akzeptanzkriterien:

- Die App zeigt eine Liste aller buchbaren Ausruestungsgegenstaende mit Kategorie (z.B. Regler, Flasche, Jacket), Bezeichnung und Gesamtanzahl
- Fuer jeden Gegenstand ist die aktuelle Verfuegbarkeit sichtbar (verfuegbar / belegt)
- Mitglieder koennen einen verfuegbaren Gegenstand fuer einen Zeitraum (Datum von / bis) buchen
- Eine Buchung ist nur moeglich, wenn der Gegenstand im gewuenschten Zeitraum verfuegbar ist
- Mitglieder koennen eigene Buchungen einsehen und stornieren
- Admin und Vorstand koennen alle Buchungen einsehen und stornieren
- Admin kann Ausruestungsgegenstaende anlegen, bearbeiten und loeschen
- Die Funktion ist auf iOS, Android und Web verfuegbar

Offene Fragen:

- Ob eine maximale Buchungsdauer je Gegenstand oder je Mitglied gelten soll
- Ob Mitglieder bei Verfuegbarkeit eines gebuchten Gegenstands benachrichtigt werden sollen (Warteliste)
- Ob der Zustand der Ausruestung (z.B. defekt, in Wartung) erfasst werden soll
- Ob Buchungen an Termine (FR-010) gekoppelt werden koennen

Status: Offen

### FR-032 Die App unterstuetzt Push-Benachrichtigungen

Prioritaet: Muss

Beschreibung:
Die App verfuegt ueber eine technische Grundlage fuer Push-Benachrichtigungen auf iOS und Android. Diese Infrastruktur wird von allen Funktionen genutzt, die Benachrichtigungen ausloesen (z.B. FR-022, FR-026, FR-027). Benutzer koennen Push-Benachrichtigungen in ihrem Profil verwalten.

Akzeptanzkriterien:

- Die App fordert beim ersten Start die Berechtigung fuer Push-Benachrichtigungen an
- Push-Benachrichtigungen funktionieren auf iOS und Android, auch wenn die App im Hintergrund oder geschlossen ist
- Auf Web sind Push-Benachrichtigungen nicht verpflichtend, koennen aber optional unterstuetzt werden
- Benutzer koennen Push-Benachrichtigungen im Profil global aktivieren oder deaktivieren
- Benutzer koennen einzelne Benachrichtigungstypen gezielt ein- oder ausschalten (z.B. Chat, Termine, Umfragen)
- Push-Tokens werden sicher in der Datenbank gespeichert und beim Abmelden entfernt

Getroffene technische Entscheidung:

- Versand ueber Expo Push Notification Service (passt zu bestehendem Expo-Stack)

Offene Fragen:

- Welche Ereignisse konkret eine Push-Benachrichtigung ausloesen sollen (wird je FR spezifiziert)

Status: Umgesetzt

## Getroffene fachliche Entscheidungen

- **Registrierung**: Benutzer duerfen sich selbst registrieren. Das Konto muss anschliessend von einem Admin oder Vorstand freigeschaltet werden, bevor es vollstaendig genutzt werden kann.
- **Mehrfachrollen**: Ein Benutzer darf gleichzeitig mehrere Rollen haben.
- **MVP-Umfang**: Der MVP umfasst Login, Startseite und Logout. Gesonderte Rollenbereiche (Vorstand, Uebungsleiter) kommen in einem spaeteren Release.
- **Verpflichtende Profilfelder**: E-Mail-Adresse (dient als Login-Kennung), Vorname, Nachname.

## Bezug zu anderen Dokumenten

- Projektkontext und technische Planung: `PROJEKTPLAN.md`
- Rollen- und Rechtemodell: `roles.md`

## Pflegehinweise

- Neue funktionale Anforderungen fortlaufend als neue `FR-` Eintraege ergaenzen
- Anforderungen moeglichst fachlich statt technisch formulieren
- Akzeptanzkriterien nur so konkret schreiben, dass sie spaeter testbar sind