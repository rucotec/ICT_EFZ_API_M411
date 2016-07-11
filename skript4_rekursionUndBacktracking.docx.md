Rekursion und Backtracking
===========================

Lernziele:
----------
* verstehen das Prinzip von Rekursion und wenden es Beispielen
 an

* verstehen das Prinzip des Backtracking und zeigen es an einem
    Beispiel auf

Rekursion
---------

Die Rekursion ist ein zentrales Konzept in der Computerwissenschaft, um
komplexere Probleme in einfache-überschaubare Problemgebiete zu
unterteilen. Eine einfache Definition von Rekursion ist:

*Ein Problem wird mit einer Funktion in ein Teil-Problem zerlegt, das
wiederum mit der gleichen Funktion weiter zerlegt wird, bis der Rest des
Problems gelöst ist. *

Somit enthält eine Rekursion endlose Selbst-Aufrufe. Dem entsprechend
wird Abbruch-bedingung benötigt, damit es nicht zu einer Endlos-Schlaufe
kommt.

Die Rekursion kann also ein Problem aufteilen (um es somit
überschaubarer und lösbarer zu machen). Eine Rekursion kann aber auch in
einer Datenstruktur abgebildet werden.

### Rekursion in einer Datenstruktur

Wir haben die Rekursion bereits bei Datenstrukturen wie verkettete
Listen und Stapel kennengelernt:

~~~~~~~~~~~~~~~~~~~~~~~~~~
public class Node{
	//these are private
	private Object item;
	privateNodenext;
	//constructor
	public Node (Object value){
		next = null;
		item = value;
	}
...
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Die Klasse `Node` besitzt als Eigenschaft wiederum sich
selbst. Sie verwendet rekursiv die eigene Klasse, um auf das
nächste Element zu verweisen.

###Rekursive Algorithmen

Unter rekursiven Algorithmen versteht man Funktionen, die sich selbst wieder aufrufen. Entsprechend in der rekursiven Funktion die *Abbruchbedingung* sichergestellt sein, damit
es nicht zu unendlichen Aufrufen der Methode kommt.

**Beispiel: Fakultätsberechnung **

Es gibt unzählige Beispiele für Probleme, die man am einfachsten mittels
einer Rekursion löst. Ein bekanntes mathematisches Problem ist die
Berechnung der Fakultät (`fak(n)` = Produkt der Zahlen von 1 bis `n`) , hier in Pseudo-Code:

~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~
int fak(n){
	if (n==1)
		return 1;
	return n * fak(n-1);
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~

Die Funktion gibt das Produkt von `n` multipliziert mit dem Rückgabewert von `fak(n-1)` aus. Tatsächlich wird für jedem rekursiven Aufruf ein neuer Abschnitt im Arbeitspeicher (respektive im Stack) angelegt, und erst beim Erreichen der Abbruchbedingung (hier `n==1`) wird der Stack wieder von oben nach unten freigegeben.

**Beispiel: Fibonacci-Reihe berechnen **

Die Fibonacci-Reihe (1,1,2,3,5,8,…)
kann mittels Rekursion berechnet werden:

![Fibonacci-Folge, Quelle: [*https://de.wikipedia.org/wiki/Fibonacci-Folge*](https://de.wikipedia.org/wiki/Fibonacci-Folge)](media10/Fibonacci_sequence_-_optional_starting_with_zero.jpg){}

~~~~~~~~~~~~~~~~
public int calculate(int number) {
	if((number == 0) || (number == 1)){
		return number;
	}
	else {
		return calculate(number -1) + calculate(number-2);
	}
}
~~~~~~~~~~~~~~~~~~~


Übrigens ist obige Methode `calculate` ein Beispiel einer
**Mehrfach-Rekursion**, da die Methode gleich mehrmals (hier zweimal)
aufgerufen wird.

**Beispiel: Rekursives durchlaufen von Baumstrukturen**

Rekursion findet sich auch im Bearbeiten einer Baum-Struktur, um die
einzelnen Knoten durchzugehen. Wir können beispielsweise das bekannte
DOM (Document Object Model) für XML verwenden und dabei die
Child-Elemente (Kinder) in der XML-Struktur rekursiv aufrufen:

~~~~~~~~~~~~~~~~~~~~~~~
public void visitRecursively(Node node) {
	// get child nodes:
	NodeList list = node.getChildNodes();
	for (int i=0; i&lt;list.getLength(); i++) {
		// get child node:
		Node childNode = list.item(i);
		System.out.println("Found Node: " + childNode.getNodeName()
			+ " - with value: " + childNode.getNodeValue());
		// call next children with recursion:
		visitRecursively(childNode);
	}
}
~~~~~~~~~~~~~~~~~~~~~~~~

Analog dazu kann man natürlich auch Dateisysteme mit rekursiven Funktionen durchlaufen.

Rekursion vs Iteration
--------------------------

Jede Rekursion kann in eine Iteration umgewandelt werden. Die Rekursion
ist meistens die elegantere Lösung, jedoch mit dem Nachteil, dass sie
langsamer ist. Ja nach geforderter Performance macht es also mehr Sinn,
ein Problem iterativ (also mit einer Schleife) oder rekursiv zu lösen.
Gewisse Programmiersprachen verbieten explizit die Iteration und
bevorzugen die Rekursion (z.Bsp. LISP oder Prolog).

Beispiel: Eine Funktion soll die Zahlen von n1 bis n2 ausgeben, wobei n1 <= n2 sein soll.

Als Iteration würden wir es so programmieren:

~~~~~~~~~~~~~~~~~~~~
public static void printSeries(int n1, int n2){
	for (int i = n1; i < n2; i++){
		System.out.print(i + ",");
	}
	System.out.print(n2);
}
~~~~~~~~~~~~~~~~~~~~~

Wir können diese Iteration auch als Rekursion programmieren:

~~~~~~~~~~~~~~~~~~~~~~~
public static void printSeries(int n1, int n2){
	//stop recursion:
	if (n1 == n2){
		System.out.print(n2);
	} 
	else {
		System.out.print(n1 + ",");
		printSeries(n1 + 1, n2); //recursive call
	}
}
~~~~~~~~~~~~~~~~~~~~~~~

```include
skript4_ueb01_rekursion.md
```

Backtracking
-------------

Backtracking ist eine Form von Rekursion, bei der verschiedene
Lösungswege für ein Problem durchsucht werden. Wenn man beim Suchen der
Lösung merkt, dass dies der falsche Weg ist, wird der Weg bis zur
letzten Entscheidung zurückgegangen und es wird nach einer neuen Lösung
gesucht. Am einfachsten stellt man sich das Suchen nach einer Lösung in
Form eines Baumes vor:


![](media10/image2.gif){}   

1. Man beginnt bei *Root* und hat A oder B zur Auswahl. Man wählt A.                                                                          
2. Bei A haben wir C oder D zur Auswahl. Man wählt C.                                                                          
3.  C ist schlecht. Gehen wir zurück zu A.

4.  Bei A haben wir C schon probiert. Versuchen wir D.                                                                          
5.  D ist schlecht. Gehen wir zurück zu A.
                                                                         
6.  Bei A haben wir keine weitere Lösungswege. Gehen wir zurück zu *Root*.                                                                          
7.  Bei *Root* haben wir A schon probiert. Versuchen wir B.                                                                          
8.  Bei B haben E und F zur Auswahl. Versuchen wir E.                                                                          
9.  E ist gut. Wir haben einen Weg gefunden.

Der Baum ist eine abstrakte Struktur, um Lösungswege zu
veranschaulichen. Bei den meisten Problemen haben wir keine
Baumstruktur, sondern müssen mit anderen Datenstrukturen (z.Bsp. Arrays)
arbeiten. In Pseudo-code sieht ein Backtracking-Algorithmus wie folgt
aus:

~~~~~~~~~~~~~~~~~~~~~~~~~~
boolean solve(Node n) {
	if n is a leafnode {
		if the leaf is a goal node return true
	else 
		return false
	}
	else {
		foreach child c of n {
			if solve(c) succeeds, return true
		}
		return false
	}
}
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Wichtig ist, dass die Backtracking-Funktion als *boolean* umgesetzt
wird. Somit wissen wir, wenn ein bestimmter Knoten (*Node*) *true* ist,
dass wir einen gültigen Lösungsweg haben.

Der Algorithmus besteht aus 2 Teilen:

Das Ende eines Lösungsweges, wo wir prüfen, ob wir erfolgreich sind:

~~~~~~~~~~~~~~~~~~~~~~~~~~~
if the leaf is a goal node:
	return true
else: 
	return false
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Und der rekursive Teil, wo wir solange in „Unter-Wegen“ Suchen (mit
Rekursion) bis eine erfolgreiche Lösung gefunden wurde oder gar keine:

~~~~~~~~~~~~~~~~~~~~~~~~~~~
foreach child c of n {
	if solve(c) succeeds, return true
}
return false
~~~~~~~~~~~~~~~~~~~~~~~~~~~

Quelle:
[*http://www.cis.upenn.edu/\~matuszek/cit594-2012/Pages/backtracking.html*](http://www.cis.upenn.edu/~matuszek/cit594-2012/Pages/backtracking.html)
(Stand Sept. 2015)