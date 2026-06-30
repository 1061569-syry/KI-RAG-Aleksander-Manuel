\# Wissensbasis: SQL / Datenbanken (MySQL - Reifenservice)



Diese Wissensbasis dient als Referenz für die Erstellung syntaktisch korrekter, sicherer und effizienter MySQL-Abfragen im Kontext des Reifenservice-Systems.



\---



\## Daten abfragen (SELECT)



Standardabfrage zum Filtern und Ausgeben von Daten aus einer Tabelle (z. B. alle Kunden mit einem bestimmten Nachnamen oder aus einer Region):



```sql

SELECT name, telefon

FROM kunden

WHERE ort = 'Münster';



Daten einfügen / ändern / löschen

1\. Daten einfügen (INSERT)

Fügt einen neuen Datensatz (z. B. einen neuen Kunden oder ein neues Fahrzeug) in die Datenbank ein.



INSERT INTO kunden (name, telefon, ort)

VALUES ('Max Mustermann', '0123-456789', 'Münster');



2\. Daten ändern (UPDATE)

Ändert bestehende Daten (z. B. wenn ein Kunde eine neue Telefonnummer hat).



UPDATE kunden

SET telefon = '0987-654321'

WHERE name = 'Max Mustermann' AND ort = 'Münster';



3\. Daten löschen (DELETE)

Entfernt Datensätze dauerhaft aus der Tabelle (z. B. einen alten Auftrag).



DELETE FROM auftraege

WHERE auftrag\_id = 1042;



WICHTIGE WARNUNG ZU UPDATE \& DELETE OHNE WHERE!

Wird die WHERE-Klausel bei einem UPDATE oder DELETE weggelassen, betrifft die Aktion alle Datensätze der Tabelle!



Ein DELETE FROM kunden; löscht den gesamten Kundenstamm unwiderruflich.



Ein UPDATE fahrzeuge SET reifengroesse = '205/55 R16'; überschreibt die Reifengröße bei absolut jedem Auto in der Datenbank.

Merke: Niemals ein destruktives Statement ohne WHERE ausführen!



Joins

Joins verknüpfen Daten aus mehreren Tabellen basierend auf einer logischen Beziehung (Primärschlüssel zu Fremdschlüssel), z. B. um zu sehen, welches Fahrzeug welchem Kunden gehört.



Beispiel-Struktur (Reifenservice):

Tabelle kunden (Spalten: kunden\_id, name, telefon)



Tabelle fahrzeuge (Spalten: fahrzeug\_id, kennzeichen, modell, kunden\_id)



INNER JOIN

Liefert nur die Datensätze zurück, bei denen es in beiden Tabellen eine Übereinstimmung gibt. Kunden ohne registriertes Fahrzeug oder Fahrzeuge ohne eingetragenen Besitzer werden ausgeblendet.



SELECT k.name, f.kennzeichen, f.modell

FROM kunden k

INNER JOIN fahrzeuge f ON k.kunden\_id = f.kunden\_id;



LEFT JOIN (LEFT OUTER JOIN)

Liefert alle Datensätze der linken Tabelle (kunden), selbst wenn für sie kein Fahrzeug in der rechten Tabelle (fahrzeuge) existiert. Hat ein Kunde kein Auto angemeldet, werden die Fahrzeug-Spalten mit NULL aufgefüllt.



SELECT k.name, f.kennzeichen

FROM kunden k

LEFT JOIN fahrzeuge f ON k.kunden\_id = f.kunden\_id;



Normalisierung

Die Normalisierung minimiert Redundanzen (doppelte Datenhaltung) und verhindert Datenfehler (Anomalien).



1\. Normalform (1NF)

Definition: Alle Attribute müssen atomar sein (nur ein Wert pro Zelle, keine Listen) und die Tabelle darf keine Wiederholungsgruppen besitzen.



Problem im Reifenservice: Eine Spalte montierte\_reifen mit dem Wert "Vorne: Michelin, Hinten: Continental" verletzt die 1NF.



Lösung: Reifenmarke und Position müssen in separate Spalten oder in eine eigene Tabelle aufgeteilt werden.



2\. Normalform (2NF)

Definition: Die Tabelle muss in der 1NF sein und jedes Nicht-Primärattribut muss voll funktionell vom gesamten Primärschlüssel abhängen (wichtig bei zusammengesetzten Schlüsseln).



Problem im Reifenservice: In einer Tabelle AuftragsPositionen mit dem zusammengesetzten Schlüssel (AuftragsID, ReifenID) existiert die Spalte KundenName. Der Name hängt aber nur von der AuftragsID ab, nicht vom Reifen.



Lösung: Der KundenName gehört in die Tabelle kunden oder direkt zur auftraege-Haupttabelle.



3\. Normalform (3NF)

Definition: Die Tabelle muss in der 2NF sein und es dürfen keine transitiven Abhängigkeiten existieren (keine Abhängigkeiten unter Nicht-Schlüsseln).



Problem im Reifenservice: In der Tabelle fahrzeuge gibt es die Spalten hersteller (z.B. VW) und hersteller\_land (z.B. Deutschland). Das Land hängt vom Hersteller ab, nicht direkt vom einzelnen Fahrzeug-Kennzeichen.



Lösung: Die Spalte hersteller\_land gehört in eine separate Stammdaten-Tabelle hersteller.



Häufige Fehler (Troubleshooting-Guide für die KI)

Fehlende WHERE-Klausel: Führt zur unbeabsichtigten Zerstörung oder Änderung des gesamten Datenbestands bei UPDATE und DELETE.



Falsche oder fehlende Join-Bedingung (ON): Eine fehlerhafte Bedingung (z.B. k.kunden\_id = f.fahrzeug\_id) führt zu unlogischen Datenverknüpfungen. Fehlt das ON komplett, entsteht ein Cross Join (Kartesisches Produkt), was den MySQL-Server bei vielen Kunden/Fahrzeugen komplett lahmlegen kann.



Falsche NULL-Wert-Prüfung: NULL steht für das Fehlen eines Wertes (z.B. wenn ein Fahrzeug noch keinen Folgetermin hat). Die Abfrage WHERE naechster\_termin = NULL liefert niemals Ergebnisse. Richtig ist: WHERE naechster\_termin IS NULL.



Datentyp-Konflikte (Implizite Konvertierung): Kennzeichen oder Reifenbezeichnungen müssen immer in einfachen Anführungszeichen stehen ('MS-AB-123'), numerische IDs hingegen nicht (WHERE kunden\_id = 5). Falsche Typisierungen zwingen MySQL dazu, Indizes zu ignorieren, was Abfragen extrem verlangsamt.

