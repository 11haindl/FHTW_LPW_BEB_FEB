# FHTW_LPW_BEB_FEB - Backend Basics/ Frontend Basics

This is a repository with solutions to the courses "Backend Basics" and "Frontend Basics" (LPW) at FH Technnikum Wien. The two courses are linked to each other. There are 5 assignments for each course. The assignments 1 and 2 are independent from the other assignments. Assignment 3 - 5 are build on each other, Frontend and Backend are connected.

# Assignments

## BEB Assignment 1

**Konzipieren** Sie die Implementierung einer Telefonzentrale als Service, das Anrufe für
mehrere Abteilungen entgegennimmt, verteilt und der Gegenstelle die Leitung, sowie den
Namen der Abteilung und eines zuständigen Mitarbeiters zurückgibt.
Folgende **Schnittstelle** soll das Service bereitstellen:
- **GET** Parameter String : "phoneNumber"
- **GET** Parameter String : "callerName"

Der Output soll wie in folgender JSON Form sein:

```
{
  "department": "String",
  "employee": "String",
  "line": "Number"
}
```

Es ist ausdrücklich nur ein Konzept und keine Implementierung gefordert!


## FEB Assignment 1

### Teil 1

Bauen Sie das Checkout Formular (nur HTML und CSS) in Bootstrap. Recherchieren Sie
die klassischen Felder.
Verwenden Sie Felder mit mind diesen Typen:
- Text,
- Select,
- Passwort,
- E-Mail,
- Checkbox,
- Radio Button,
- Textarea.

Beachten Sie dabei Labels für die Felder und Rahmen für die einzelnen Abschnitte im
Formular.
Verwenden Sie zumindest folgende Felder:
- Anrede,
- Vor- und Nachname,
- Alter/Geburtsdatum,
- Lieferadresse mit den diversen Feldern,
- Zahlungsweise,
- Zustimmung zu einer fiktiven Datenschutzerklärung.

Validieren Sie ihren HTML Code.

### Teil 2

Bauen Sie die Bootstrap Navigation ein.
Alternativ zum Formular soll es einen Link zu zwei anderen HTML Seiten geben (z.b. der
Lebenslauf oder das Burger-Beispiel aus dem Wintersemester).



## BEB Assignment 2

**Planen** und **implementieren** Sie eines Service das PhP Schleifen simuliert. Jede der drei
Schleifen Varianten soll in einem Objekt gekapselt sein. Das Service kann über einen
Parameter gesteuert werden und drei verschiedene Simulationen ausführen. Das
Ergebnis wird als JSON zurück geliefert.

Als Input dient, ein Array der aus den Buchstaben $characters = [A..Z] besteht.
- Die For-Schleife soll alle geraden Buchstaben in ein Array ablegen.
- Die Foreach Schleifen Simulation soll einen rückwärts sortierten Array per For Schleife erzeugen; also [Z..A].
- Die While Schleife soll alle Zeichen in ein Array Schreiben bis das gewünschte
Zeichen gefunden wurde.

**Schnittstelle**
- **GET** Parameter String: loopType (mögliche Werte: REVERSE , EVEN , UNTIL )
- **GET** Parameter String: until (bis zu welchem Zeichen)

**Output**
```
{
"loopName": "String",
"result": "Array"
}
```
Achten Sie darauf, wie die Objekte konzipiert werden, wie sie zusammenarbeiten und
welche Eigenschaften von außen nicht manipuliert werden sollten.
Überlegen Sie sich wo und wie die Daten zwischen Objekten weiter gegeben werden.
Überprüfen Sie Ihre JSON Ausgabe mit https://jsonlint.com/ .

Es ist nun ausdrücklich auch die Implementierung gefordert!


## FEB Assignment 2

Erstellen Sie mit HTML und Bootstrap eine GUI in der Benutzer einen Ajax Request zu
folgender URL auslösen kann: https://dummyjson.com/users

Durch Klicken auf einen Button soll der Request via GET durchgeführt werden und der
Inhalt so verarbeitet werden, dass das empfangene Objekt in Form einer HTML Tabelle
ausgegeben wird, die generisch mit JavaScript erzeugt werden soll.

Überlegen Sie zuerst wie das Interface aussehen könnte (Paper Prototype mit abgeben).
- Konzipieren Sie die Funktionalität.
- Welche Elemente, Events und Aktionen haben Sie zu behandeln.

Verwenden Sie einen objektorientierten Ansatz und trennen Sie JS, HTML und CSS!


## BEB Assignment 3

Planen und Implementieren Sie eine Web-Anwendung, die aus einer Datenbank Produkte
ausliest und nach Kategorien ausgibt. Die Anwendung bietet die Möglichkeit Listen von
Produktkategorien und Produkten auszugeben. Als Grundlage dient eine vorhandene
Datenbank (Diese finden Sie auf Moodle).

In der DB finden Sie unter anderen zwei Tabellen, welche die Produkte ( products ) und
die Produktkategorien ( product_types ) enthalten, die über einen Fremdschlüssel (von
products.id_product_types nach product_types.id ) verbunden sind.

Die Queries die Sie benötigen sind die beiden, wobei die php Variable natürlich einen
gültigen Wert enthalten muss (die ID zur gewählten Kategorie):

- für die Liste der Kategorien
  ```
  SELECT id, name FROM product_types ORDER BY name
  ```
- für die Produkte einer Kategorie
  ```
  SELECT t.name AS productTypeName, p.name AS prodcutName
  FROM product_types t
  JOIN products p ON t.id = p.id_product_types
  WHERE t.id = {$productTypeId};
  ```

**Schnittstelle**

Folgende zwei Parameter sollen über die Schnittstelle verarbeitet werden:
- **GET** Parameter String: action (Kann die Werte listTypes und
listProductsByTypeId enthalten)
- **GET** Parameter Integer: typeId (Im Fall listProductsByTypeId , enthält dieser
Parameter die ID der gewählten Kategorie)

2 Beispiele dazu:
- http://localhost/Uebung3/index.php?action=listTypes
- http://localhost/Uebung3/index.php?action=listProductsByTypeId&typeId=2

**Output zur Aktion listTypes:**
```
[
  {
    "productType": "day creme",
    "url": "http://localhost/Uebung3/index.php?action=listProductsByTypeId&typeId=1"
  },
  {
    "productType": "night creme",
    "url": "http://localhost/Uebung3/index.php?action=listProductsByTypeId&typeId=2"
  }
  /*, ... und so weiter */
]
```

**Output zur Aktion listProductsByTypeId mit typeId:**
```
{
  "productType": "day creme",
  "products": [
    {
      "name": "Daycreme"
    },
    {
      "name": "ZZ SENSITIVE - Protective Day Cream"
    },
    {
      "name": "Mega-Mushroom Skin Relief - Soothing Face Cream"
    } /* , ... und so weiter */
  ],
  "url": "http://localhost/Uebung3/index.php?action=listTypes"
}
```

**ToDos:**

- Verwenden Sie möglichst die im Unterricht vorgestellte MVC Architektur
- Überlegen Sie, wo die DB eingebunden werden kann und wie Sie dazu die Konfiguration und Datenweitergabe organisieren
- Stellen Sie, bevor Sie mit der Umsetzung starten, sicher, dass die DB verbunden
wird

**Planungsschritte**
- überlegen Sie welche Objekte wahrscheinlich eine Rolle spielen werden
- wie könnten die Namen der Objekte lauten
- welche Eigenschaften und Methoden werden die Objekte brauchen
- wo wird es notwendig sein Schleifen oder Fallunterscheidungen einzuplanen
- welche Parameter müssen weiter gereicht werden?
- zeichnen Sie einen leserlichen Plan auf



## FEB Assignment 3

**Wir versuchen die LV mit Backenbasics langsam zu verbinden**

1. Entwerfen Sie ein GUI, mit dem Sie die Produktliste die in der DB gespeichert sind
strukturiert browsen können, wobei Page-Reloads vermieden werden sollen (AJAX
ist gefordert).
Welche HTML Elemente benötigen Sie, welche JavaScript Objekt?
Denken Sie nun voraus: Die Produkte sollen später einer Bestellung hinzugefügt
werden, wie bei einem Webshop.

2. Implementieren Sie die Bootstrap GUI. Binden Sie die GUI an Ihre Übung aus
Backendbasics an und laden Sie die Produktkategorien.
Klickt man auf eine Kategorie, sollen die Produkte in übersichtlicher Form
ausgegeben werden. Welches Problem müssen Sie lösen um BE und FE zu
verbinden?

Die Schnittstellen finden Sie in der Übung aus BEB.



## BEB Assignment 4

**Planen und Implementieren:**

Erweitern Sie die Übung mit den Produktliste (gerne Ihren eigenen Code, oder die
Musterlösung) mit der Funktionalität eines Warenkorbs. Der Client soll über zwei
Schnittstellen jeweils einen Artikel hinzufügen, oder entfernen können (mehrfach möglich:
n mal hinzu oder weg => die Anzahl wird je Eintrag mehr oder weniger) und mit einer
weiteren Schnittstelle die Liste der Waren im Warenkorb anzeigen können. Verweden Sie
weiterhin die MVC Architektur und überlegen Sie welche Technologien zum behalten des
Warenkorbinshalts eingesetzt werden kann.

**Schnittstelle**
- http://localhost/Uebung4/index.php?action=addArticle&articleId=10
- http://localhost/Uebung4/index.php?action=removeArticle&articleId=10
- http://localhost/Uebung4/index.php?action=listCart
- Ergebnis nach Add oder Remove: 
  ```{"state": "OK / ERROR"}```
- Ergebnis der Cartliste:
  ```
  { "cart":
    [
      {"articleName": "String", "amount": "Number" },
      /** ... **/
    ]
  }
  ```


## FEB Assignment 4

**Wir erweitern die gemeinsame Übung von BEB und FEB.**

1. Erweitern Sie die Produktliste mit der Funktionalität, dass man einzelne Artikel einem
Warenkorb hinzufügen kann.
War die Aktion erfolgreich, soll dem Benutzer dies mitgeteilt werden (Verwenden Sie
ein Bootstrap Modal dazu).
2. Erstellen Sie eine zweite View in der der Benutzer den Warenkorb ansehen kann.
Beide Views sollen über die Navbar aufgerufen werden können.
3. In dieser Liste sollen die Artikel und die Stückzahl, so wie der Gesamtpreis pro
Posten und auch die Gesamtsumme angezeigt werden. Die Liste soll dynamisch
beim Laden der View erzeugt werden.
4. In dieser Liste soll es außerdem möglich sein, die Stückzahlen der Artikel weiter zu
erhöhen oder eben zu verringern, bis der Artikel 0 wird. In dem Fall soll der Artikel
nicht mehr in der Liste angezeigt werden.

Die Schnittstellendefinition finden Sie in der Übung aus BEB.



## BEB Assignment 5

**Planen und Implementieren:**

Erweitern Sie das bestehende Projekt um 2 weitere Funktionalitäten.

1. Der Benutzer soll die möglichkeit haben sich am System anzumelden. Erstellen Sie
dazu Testuseraccounts und implementieren Sie eine Login- und Logout-variante.
Das System soll den aktuellen Benutzer wieder erkennen können (Session,
Datenbank, Token?)

2. Es soll die Möglichkeit (für angemeldete Benutzer) geben, den Warenkorb auf der
Datenbank abspeichern zu können.
Und es soll die Möglichkeit die List der vergangen "Bestellungen" aufzulisten (Datum,
der Bestellungen reicht aus)

**Schnittstelle**

- **POST** http://localhost/Uebung4/index.php?action=login (Username und Password als
Parameter)
- **POST** http://localhost/Uebung4/index.php?action=logout
- **POST** http://localhost/Uebung4/index.php?action=placeOrder
- **GET** http://localhost/Uebung4/index.php?action=listOrderHistory
- Ergebnis nach Login und Logout: ```{"state": "OK / ERROR"}```
- Ergebnis der History: Überlegen Sie eine sinnvolle Repräsentation der Daten


## FEB Assignment 5

**Wir erweitern die gemeinsame Übung von BEB und FEB ein letztes Mal.**

1. Konzipieren und implementieren Sie ein Login Formular und die Übersicht über
vergangene Bestellungen eines Benutzers (Datum und Gesamtbetrag reichen in der
Anzeige aus)
2. Verbinden Sie die beiden neuen GUI Elemente mit den vorhandenen API
Schnittstellen. Für eingeloggte Benutzer erhalten Sie einen Token, der beim Aufruf
der Bestellhistory mit übertragen werden muss.
3. Fehlerhafte Logins ergeben eine entsprechende Fehlermeldung.
4. Aufrufe der History ohne Token, oder falschen Token führen auch zu einer
entsprechenden Fehlermeldung.
Die Schnittstellendefinition finden Sie in der Übung aus BEB.




























