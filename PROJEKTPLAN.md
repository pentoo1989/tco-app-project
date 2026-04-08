# Projektplan: Expo App fuer iOS, Android und Web

Stand: 06.04.2026

## Ziel

Es wird ein neues Projekt fuer eine App aufgebaut, die auf folgenden Plattformen laeuft:

- iOS
- Android
- Webbrowser

Die technische Entscheidung ist getroffen: Das Projekt wird mit Expo, React Native, TypeScript und React Native Web umgesetzt.

## Getroffene Entscheidung

Ausgewaehlter Stack:

- Expo
- React Native
- TypeScript
- Expo Router
- React Native Web
- Supabase (Auth + Postgres + Storage)

Diese Wahl ist fuer das Vorhaben sinnvoll, weil sie eine gemeinsame Codebasis fuer Mobile und Web erlaubt, schnell startbar ist und ein starkes Oekosystem fuer MVP und spaetere Erweiterungen bietet.

Verbindliche Backend-Entscheidung:

- Supabase wird fuer Authentifizierung und saemtliche Datenablagen verwendet.
- Benutzerdaten werden nicht lokal in der App persistiert, sondern in Supabase verwaltet.

## Projektziele

- Eine moeglichst gemeinsame Codebasis fuer iOS, Android und Web
- Schnelles lokales Entwickeln mit kurzer Feedback-Schleife
- Solide Wartbarkeit durch klare Projektstruktur
- Gute Erweiterbarkeit fuer API-Anbindung, Authentifizierung und native Funktionen
- TypeScript als gemeinsame Sprache fuer UI und Anwendungslogik
- Anmeldung mit Username oder E-Mail und Passwort unterstuetzen
- Account-Aktivierung ueber einen Link per E-Mail vorsehen
- Rollen und Rechte von Anfang an beruecksichtigen

## Geplanter Initial-Stack

- App Framework: Expo
- UI Laufzeit: React Native
- Web-Unterstuetzung: React Native Web
- Sprache: TypeScript
- Navigation und Routing: Expo Router
- Server State: TanStack Query
- Lokaler State: Zustand
- Formulare: React Hook Form
- Validierung: Zod
- Authentifizierung: Supabase Auth mit Session-Handling und Rollenpruefung
- Datenbank: Supabase Postgres
- Dateispeicher: Supabase Storage (fuer Medien und Dokumente)
- Optional spaeter: Supabase Edge Functions fuer serverseitige Logik
- Styling: NativeWind oder alternativ ein schlankes Design-System auf Basis von React Native StyleSheet
- Tests: React Native Testing Library fuer Komponenten, Vitest oder Jest fuer Logik, Playwright fuer Web E2E

## Architektur fuer den Projektstart

Die erste Version soll bewusst schlank und skalierbar aufgebaut werden.

Vorgesehene Struktur:

- `app/` fuer Routen, Layouts und Screens mit Expo Router
- `src/components/` fuer wiederverwendbare UI-Bausteine
- `src/features/` fuer fachliche Module
- `src/lib/` fuer API-Client, Konfiguration und Utilities
- `src/features/auth/` fuer Login, Aktivierung und Session-Flows
- `src/features/access/` fuer Rollen, Rechte und Guards
- `src/store/` fuer globalen Zustand
- `src/hooks/` fuer gemeinsame Hooks
- `src/types/` fuer zentrale TypeScript-Typen
- `assets/` fuer Bilder, Icons und Fonts

## Authentifizierung und Account-Aktivierung

Die App soll bereits in der Grundarchitektur auf Benutzerkonten vorbereitet werden.

Vorgesehene Anforderungen:

- Login mit Username oder alternativ E-Mail plus Passwort
- Aktivierungslink per E-Mail nach Registrierung oder Benutzeranlage
- Erst nach erfolgreicher Aktivierung darf ein Konto produktiv genutzt werden
- Session-Status und Benutzerrolle muessen zentral verfuegbar sein
- Gesperrte oder nicht aktivierte Konten muessen sauber abgefangen werden

Geplanter technischer Zuschnitt:

- Dedizierte Auth-Screens fuer Login, Aktivierung und Fehlerfaelle
- Zentrale Session-Verwaltung im Client
- Rollenpruefung ueber Guards oder Helper-Funktionen
- Supabase Auth liefert Session, Benutzerstatus und Aktivierungsprozess
- Rolleninformationen werden in Supabase-Tabellen gefuehrt und mit der Session verknuepft

## Datenablage und Persistenz

Die Datenhaltung erfolgt zentral in Supabase.

- Relationale Fachdaten und Benutzerprofile werden in Supabase Postgres gespeichert
- Authentifizierung und Aktivierungsflows laufen ueber Supabase Auth
- Dateien und Medien werden in Supabase Storage abgelegt
- Zugriff wird ueber Rollenmodell und Row Level Security gesteuert
- Der Client speichert lokal nur Session-bezogene Informationen, nicht die zentrale Benutzerdatenhaltung

## Rollen und Rechte

Das Projekt soll ein rollenbasiertes Berechtigungssystem erhalten.

Aktuell vorgesehene Rollen:

- Admin
- Mitglied
- Vorstand
- Uebungsleiter

Die fachliche Beschreibung der Rollen und Rechte wird in einer separaten Datei dokumentiert: `roles.md`.

Im Projekt selbst bedeutet das:

- Rollen muessen Teil des Benutzerprofils und der Session sein
- Zugriffe auf Screens, Aktionen und Verwaltungsfunktionen muessen anhand der Rolle steuerbar sein
- Berechtigungsregeln sollen nicht verteilt in UI-Komponenten entstehen, sondern zentral definiert werden

## Technische Leitlinien

- Business-Logik soll moeglichst von Screens getrennt werden
- Wiederverwendbare Komponenten sollen plattformneutral entworfen werden
- Web soll kein nachtraeglicher Zusatz sein, sondern von Beginn an mitlaufen
- Native Sonderfaelle sollen gezielt gekapselt werden
- Abhaengigkeiten werden bewusst klein gehalten, damit das Projekt spaeter nicht unnötig verkompliziert wird
- Authentifizierung und Berechtigungen sollen frueh in die Architektur integriert werden statt spaeter nachgeruestet zu werden

## Umsetzungsplan

### Phase 1: Projektgrundlage

- Neues Expo-Projekt mit TypeScript initialisieren
- Web-Support pruefen und lauffaehig machen
- Expo Router einrichten
- Basisstruktur fuer `app/` und `src/` anlegen
- Supabase-Projekt anlegen und lokale Umgebungsvariablen definieren

### Phase 2: Entwicklungsbasis

- TanStack Query integrieren
- Zustand fuer lokalen State vorbereiten
- Zod und React Hook Form einbinden
- Gemeinsame App-Konstanten und Konfiguration definieren
- Auth-State und Session-Modell definieren
- Rollen- und Berechtigungsmodell in Code vorbereiten
- Supabase Client integrieren und grundlegende Tabellenstruktur planen

### Phase 3: UI-Grundgeruest

- Startscreen fuer Mobile und Web anlegen
- Wiederverwendbare Basis-Komponenten definieren
- Ein einfaches Layout-System fuer Abstaende, Farben und Typografie aufsetzen
- Login-Screen und Aktivierungs-Flow vorbereiten

### Phase 4: Qualitaetssicherung

- Testbasis fuer Logik und Komponenten vorbereiten
- Web-E2E-Tests spaeter mit Playwright ergaenzen
- Linting und Type-Checks frueh aktiv halten

### Phase 5: Benutzer und Rechte

- Rollenmodell gemaess `roles.md` technisch abbilden
- Zugriffsschutz fuer Screens und Aktionen einfuehren
- Nicht aktivierte Benutzerkonten im UX-Flow sauber behandeln
- Auth- und Rollenlogik durch Tests absichern
- Supabase Row Level Security Policies fuer Rollen und Datenzugriffe definieren

## Was als Naechstes umgesetzt wird

Im naechsten Schritt wird das Projekt als Expo-App mit TypeScript fuer iOS, Android und Web angelegt.

Anschliessend richte ich die Basisstruktur fuer Routing, State, Authentifizierung und gemeinsame App-Module ein.

## Status

- Die technische Entscheidung fuer Vorschlag 1 ist getroffen.
- Der Projektplan wurde auf die konkrete Umsetzung mit Expo ueberarbeitet.
- Login, Aktivierungslink und Rollenmodell sind als Anforderungen aufgenommen.
- Die Rollen und Rechte werden zusaetzlich in `roles.md` dokumentiert.
- Supabase ist als verbindlicher Dienst fuer Auth und Datenablage festgelegt.
- Bis zu diesem Punkt wurde weiterhin noch kein Projekt erzeugt.