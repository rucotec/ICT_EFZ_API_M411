##Übungen: Stack implementieren und für Kartenspiel nutzen

**Lernziele**

* Erstellen und Benutzen Stack-Datenstruktur in akademischer und praktischer Variante

**Zeit:** 30 + 45 + x Minuten

###Stack Klasse erstellen 

Implementieren Sie Ihre `Stack` Klasse mit den `push` und `pop`
Methoden. Bei `push` wird ein Element zuoberst hinzugefügt. Bei `pop`
wird das aktuelle Element entfernt. Sie können den Code Ihrer `Node`-
Klasse der Verketten Liste für die interne Datenstruktur übernehmen.

Testen Sie die Funktionalität mit einem geeigneten Testrahmen.

###`isEmpty()`-Methode implementieren

Fügen Sie eine `isEmpty()`-Methode hinzu. Diese überprüft, ob es Elemente
im `Stack` hat. Die Methode gibt einen boolean zurück.

###Stack ergänzen

Ergänzen Sie `Stack` um eine Methode `peek()`, welche das zuletzt auf
dem Stapel gelegte Element zurück liefert ohne es zu entfernen.

###Palindrome prüfen (25 Minuten)
 
Verwenden Sie den `Stack` um zu überprüfen, ob ein String ein Palindrom
ist. Gültige Palindrome sind beispielsweise *OTTO*, *ANNA*, oder *RACECAR* - also Worte oder Sätze, die dasselbe von vorne und von hinten gelesen gleich sind. Mit einem `Stack` lässt sich das einfach überprüfen. Erweitern Sie den Code,
so dass der Benutzer einen String eingeben kann.

Verwenden Sie für diese Lösung ihren eigenen `Stack`.

**Lösungsvorschlag:**

`Skript2b_ObjectStack.java`


###Kartenstapel implementieren (45 Minuten)

*Einführung:* Sie wollen gern ein PC-Kartenspiel entwickeln. Dazu wird zunächst ein Kartenstapel benötigt. Die einzelnen Karten sollen als Objekte der Klasse `Card` mit den Attributen `String farbe`, `int wert` und `String anzeige` angelegt werden. Damit es ein echter Kartenstapel wird, speichern Sie alle Karten in einem Stack ab.

*Auftrag:* Erstellen Sie einen Stack von Patience- bzw. Solitär-Karten (52 Karten, 4 Farben {Karo, Herz, Pik, Kreuz} mit den Zahlen 2 bis 10, Bube, Dame, König, Ass). Zur späteren Spielimplementierung geben Sie den Zahlen-Karten die Werte 2 - 10 zu. Bube bekommt Wert 11, Dame den Wert 12, König = 13 und Ass = 14. Nutzen Sie sinnvolle Schleifenkonstrukte zum Generieren der Karten.

**Lösungsvorschlag:**

`Skript2b_CardStack.java`


*Zusatz:* 
1. Mischen Sie die Karten in Ihrem Stack.
2. Entwerfen Sie eine grafische Oberfläche für ein Kartenspiel. Dazu leiten Sie Ihre `Card`-Klasse von `JPanel` ab und erstellen eine Klassenmethode `public void paint(Graphics g)`, in der die jeweilige Karte als JPanel gerendert wird. Den Stack können Sie beispielsweise auf einer JLayeredPane realisieren.

![Beispiel Black Jack](media/swing_blackjack.png){#fig:fig_blackjack}
 


