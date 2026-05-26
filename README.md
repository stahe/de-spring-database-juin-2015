# Arbeiten mit einer relationalen Datenbank unter Verwendung des Spring-Ökosystems (Juni 2015)

Ziel dieses Projekts ist es, verschiedene Architekturen für den Datenzugriff in einer Java-Anwendung auf Basis des **Spring**-Ökosystems zu untersuchen und zu vergleichen, insbesondere **Spring JDBC** und **Spring JPA**, wenn diese auf eine relationale Datenbank angewendet werden.

Die dazugehörigen theoretischen und didaktischen Materialien sind hier verfügbar:  
👉 https://stahe.github.io/de-spring-database-juin-2015/

---

## Projektziele

- Verständnis einer **mehrschichtigen Anwendungsarchitektur**
- Zwei Ansätze für den Datenzugriff vergleichen:
  - „Klassisches“ JDBC
  - JPA (Java Persistence API)
- Die **Leistung** beider Lösungen messen und vergleichen
- Die Herausforderungen der **Portabilität zwischen DBMS** untersuchen

---

## Allgemeine Architektur

Die Anwendung basiert auf einer mehrschichtigen Architektur, in der der Ausführungsfluss von links nach rechts verläuft:

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000007080000017A09403716.png)


### Rolle der Schichten

#### UI-Schicht (Benutzeroberfläche)
- Einstiegspunkt der Anwendung
- Empfängt Benutzeraktionen
- Zeigt Ergebnisse an

#### Business-Schicht (Geschäftslogik)
- Implementiert die **Geschäftsregeln**
- Verarbeitet Daten aus:
  - der Datenbank (über DAO)
  - vom Benutzer (über UI)
- Kann Ergebnisse zurückgeben oder speichern

#### DAO-Ebene (Data Access Object)
- Stellt eine **Schnittstelle für den Zugriff auf Unternehmensdaten** bereit
- Verbirgt die technischen Details des Datenbankzugriffs
- Hängt von der verwendeten Technologie ab (JDBC oder JPA)

#### JDBC-Ebene
- Standardschnittstelle für den Zugriff auf relationale Datenbanken
- DBMS-unabhängig (über JDBC-Treiber)
- Ermöglicht gute Leistung, in der Praxis jedoch nur begrenzte Portabilität

---

## Entwicklung hin zu JPA

Seit Mitte der 2000er Jahre kann sich die Architektur wie folgt entwickeln:

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000006FE000001774C207100.png)

### Spezifische Merkmale von JPA

- Die **JPA**-Ebene generiert SQL-Abfragen
- Die DAO-Ebene:
  - enthält kein SQL mehr;
  - manipuliert persistente Objekte;
- Vorteile:
  - Bessere Portabilität zwischen DBMS'en
  - Abstraktion vom proprietären SQL
- Nachteile:
  - Im Allgemeinen geringere Leistung als bei JDBC

JPA formalisiert Konzepte, die zuvor von Frameworks wie **Hibernate** eingeführt wurden.

---

## Vergleich zwischen JDBC und JPA

Das Projekt implementiert **zwei unterschiedliche DAO-Implementierungen**:

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000006FE000001774C207100.png)

![](https://stahe.github.io/spring-database-juin-2015/images/10000000000006E10000016947159BE8.png)


### Gemeinsame Voraussetzungen

- `DAO1` und `DAO2` implementieren die **gleiche Schnittstelle `IDAO`**
- Die Unit-Tests sind für beide Implementierungen **identisch**
- Ziel: Vergleich von **Funktionalität** und **Leistung**

---

## Tests und Leistung

- Die Tests werden mit **JUnit** durchgeführt
- Es wird eine einzige Testklasse (`JUnitTestsDao`) verwendet
- Die Ergebnisse ermöglichen es uns:
  - die funktionale Konformität zu überprüfen;
  - die Ausführungszeiten von JDBC und JPA zu vergleichen;

---

## Portabilität des DBMS

Obwohl JDBC auf maximale Portabilität abzielt:
- proprietäres SQL;
- Strategien zur Generierung von Primärschlüsseln;
- spezifische reservierte Wörter;

schränken diese Portabilität in der Praxis ein.

In diesem Projekt wurden die JDBC- und JPA-Architekturen auf **sechs verschiedene DBMS** portiert, was für jedes DBMS spezifische Konfigurationen erforderte.

---

## Fazit

Dieses Projekt veranschaulicht:
- die Kompromisse zwischen **Leistung** und **Abstraktion**;
- die architektonischen Entscheidungen hinsichtlich des Datenzugriffs;
- den Beitrag von Spring zur Strukturierung und Testbarkeit von Anwendungen;

Es dient als Lernressource, um ein praktisches Verständnis von JDBC, JPA und deren vergleichenden Einsatzmöglichkeiten innerhalb einer Spring-Architektur zu erlangen.

Serge Tahé, Juni 2015
---
