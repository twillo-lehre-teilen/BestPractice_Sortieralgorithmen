<!--
author:   twillo

email:    support.twillo@tib.eu

version:  0.0.1

language: de

narrator: Stina Schäfer, Lennart Rosseburg

comment:  Eine Selbstlerneinheit mit interaktiven Programmieraufgaben für die gängigsten Sortieralgorithmen.
          Diese Seite ist lizenziert unter der [Lizenz CC-BY-SA (3.0)](https://creativecommons.org/licenses/by-sa/3.0/legalcode).

link:     https://de.wikiversity.org/wiki/Kurs:Algorithmen_und_Datenstrukturen/Vorlesung/Sortieren

script:   
-->

# Sortieralgorithmen
Dieser Kurs basiert auf dem Kapitel "Sortieren" aus dem Kurs "Algorithmen und Datenstrukturen" von Wikiversity, zu finden unter diesem [Link](https://de.wikiversity.org/wiki/Kurs:Algorithmen_und_Datenstrukturen/Vorlesung/Sortieren) und ist lizensiert unter der [Lizenz CC-BY-SA (3.0)](https://creativecommons.org/licenses/by-sa/3.0/legalcode).

<!--  style = "background-color: #A6D492; color:black; padding: 10px 10px 5px 10px; margin-bottom: 10px" -->
<div>
  Ziel dieser Selbstlerneinheit ist .
</div>

Diese Selbstlerneinheit konzentriert sich auf die Funktionsweise grundlegender Sortieralgorithmen und enthält interaktive Programmiereinheiten um das Gelernte durch eigene Anwendung zu verinnerlichen.

## Grundlagen

Diese Lektion gibt eine grundlegende Einführung in das Thema Sortieren und Sortieralgorithmen. Sortieren ist ein grundlegendes Problem in der Informatik. Es beinhaltet das Ordnen von Dateien mit Datensätzen, die Schlüssel enthalten und das Umordnen der Datensätze, so, dass eine klar definierte Ordnung der Schlüssel (numerisch/alphabetisch) besteht. Eine Vereinfachung ist die Betrachtung der Schlüssel, z.B. ein Feld von int-Werten.

#### Definition Ordnung

Zunächst wollen wir den grundlegenden Begriffe der Ordnung definieren.

**Partielle Ordnung**

Sei M eine Menge und $\leq$ $\subseteq (M\times M)$ eine binäre Relation.

Es gilt:

- Reflexivität: $x \leq x$ $\forall x \in M$
- Transitivität $x \leq y \land y \leq z \to x \leq z$ $ \forall x,y,z \in M$
- Antisymmetrie $x \leq y \land y \leq x \to x = y$ $ \forall x,y \in M $

**Strikter Anteil einer Ordnungsrelation $\leq$**

$x \le y := x \leq y \land x \neq y$

**Totale Ordnung**

- Partielle Ordnung $(M,\leq)$
- Trichotomie ("Dreiteilung") $x \le y$  $\lor$  $x = y$  $\lor$  $x \le y$ $\forall x,y \in M$

#### Sortieralgorithmen - Problembeschreibung

Als Eingabe haben wir eine Folge von Zahlen $\langle a_1,. . . , a_n\rangle$. Als Ausgabe haben wir die Permutation $\langle a'_{1},...,a'_{n}\rangle$ der gleichen Zahlen mit der Eigenschaft $a'_{1}\leq a'_{2}\leq ,...,a'_{n}$.

Die Sortierung erfolgt anhand eines Schlüssels, z.B. ganzen Zahlen. Jedes zu sortierende Element hat dabei einen festen Schlüssel und die Schlüssel lassen sich mittels einer Ordnungsrelation vergleichen (und somit sortieren). Wie genau die Datenstruktur aussieht auf der sortiert wird, hat natürlich Auswirkungen auf Praktikabilität und Laufzeit, ist für die grundlegende Funktionsweise des Algorithmus aber erst einmal unwichtig.

## InsertionSort

**Grundlegende Idee**

Dieses Kapitel behandelt die Sortiermethode InsertionSort oder auch Sortieren durch Einfügen genannt. Die Idee des Algorithmus ist, die typische menschliche Vorgehensweise, etwa beim Sortieren eines Stapels von Karten umzusetzen. Das heißt es wird mit der ersten Karte ein neuer Stapel gestartet. Anschließend nimmt man jeweils die nächste Karte des Originalstapels und fügt diese an der richtigen Stelle im neuen Stapel ein.

**Beispiel**

Schauen wir uns den Algorithmus einmal Schritt für Schritt an folgendem Beispiel an:

Sei dies eine Reihe zu sortierender Elemente, die Zahlen die zugehörigen Schlüssel, nach denen aufsteigend sortiert werden soll:

![InsertionSort Step1](docs/InsertionSort_Step1.svg)

Wir beginnen ganz links und gehen dann die Reihe zu sortierender Elemente eines nach dem anderen von links nach rechts durch. Die Elemente links des im aktuellen Durchlaufs betrachteten Elements sind dementsprechend schon sortiert (in unserer Grafik grün gefärbt), die rechts davon noch nicht (grau). Da links vom ersten Element keine weiteren Elemente stehen, mit denen der Schlüssel verglichen werden könnte, beginnen wir mit dem zweiten Element:

![InsertionSort Step2](docs/InsertionSort_Step2.svg)

Der Schlüssel des zweiten Elements ist $2$, links von der $2$ steht eine $5$. Da $5>2$ gilt, müssen wir die beiden Elemente also tauschen, damit sie der gewünschten Sortierung entsprechen:

![InsertionSort Step3](docs/InsertionSort_Step3.svg)

Links von der $2$ stehen nun keine weiteren Elemente mehr zum Vergleichen, also sind die beiden ersten Elemente nun sortiert und wir können mit dem nächsten Element weitermachen, welches den Schlüssel $4$ hat:

![InsertionSort Step4](docs/InsertionSort_Step4.svg)

![InsertionSort Step5](docs/InsertionSort_Step5.svg)

$4$ ist kleiner als der Schlüssel des Elements links daneben ($5$), also werden die Elemente getauscht. Der Schlüssel, der dann links neben der $4$ steht ist $2$, $2<4$, es muss also nicht weiter getauscht werden::

![InsertionSort Step6](docs/InsertionSort_Step6.svg)

Jetzt ist die Beobachtung wichtig, dass die Elemente links des betrachteten Elements immer schon sortiert sind. Wenn man dann nämlich auf ein Element trifft, dessen Schlüssel kleiner ist als der des aktuell betrachteten Elements, weiß man, dass das Element fertig einsortiert wurde, da ja alle Elemente weiter links dann nur noch kleinere Schlüssel haben. Die ersten drei Elemente wurden nun also fertig sortiert und wir können mit dem nächsten weitermachen, welches des Schlüssel $1$ hat:

![InsertionSort Step7](docs/InsertionSort_Step7.svg)

![InsertionSort Step8](docs/InsertionSort_Step8.svg)

$1$ ist jeweils kleiner als $3$,$4$ und $5$, das Element muss also ganz nach links "durchgetauscht" werden:

![InsertionSort Step9](docs/InsertionSort_Step9.svg)

![InsertionSort Step10](docs/InsertionSort_Step10.svg)

Das nächste Element hat den Schlüssel $7$. Ein Vergleich mit dem Schlüssel links daneben liefert $5<7$, also befindet sich das betrachtete Element bereits an der richtigen Stelle:

![InsertionSort Step11](docs/InsertionSort_Step11.svg)

![InsertionSort Step12](docs/InsertionSort_Step12.svg)

![InsertionSort Step13](docs/InsertionSort_Step13.svg)

Das nächste Element hat den Schlüssel $6$, da $7>6$ müssen wir einmal tauschen. Der nächste Vergleich liefert $5<6$, also wissen wir, dass das Element nun richtig einsortiert ist:

![InsertionSort Step14](docs/InsertionSort_Step14.svg)

![InsertionSort Step15](docs/InsertionSort_Step15.svg)

![InsertionSort Step16](docs/InsertionSort_Step16.svg)

Nun fehlt nur noch das letzte Element mit dem Schlüssel $3$, welches wir genau wie die anderen Elemente so weit nach links "durchtauschen", bis ein Element einen kleineren Schlüssel (hier $2$) aufweist:

![InsertionSort Step17](docs/InsertionSort_Step17.svg)

![InsertionSort Step18](docs/InsertionSort_Step18.svg)

Nun haben wir alle Elemente betrachtet und die Elemente sind fertig sortiert:

![InsertionSort Step19](docs/InsertionSort_Step19.svg)

## SelectionSort

## BubbleSort

## MergeSort

## QuickSort

# For test purposes

## InsertionSort

![InsertionSort Step1](docs/InsertionSort_Step1.svg)

![InsertionSort Step2](docs/InsertionSort_Step2.svg)

![InsertionSort Step3](docs/InsertionSort_Step3.svg)

![InsertionSort Step4](docs/InsertionSort_Step4.svg)

![InsertionSort Step5](docs/InsertionSort_Step5.svg)

![InsertionSort Step6](docs/InsertionSort_Step6.svg)

![InsertionSort Step7](docs/InsertionSort_Step7.svg)

![InsertionSort Step8](docs/InsertionSort_Step8.svg)

![InsertionSort Step9](docs/InsertionSort_Step9.svg)

![InsertionSort Step10](docs/InsertionSort_Step10.svg)

![InsertionSort Step11](docs/InsertionSort_Step11.svg)

![InsertionSort Step12](docs/InsertionSort_Step12.svg)

![InsertionSort Step13](docs/InsertionSort_Step13.svg)

![InsertionSort Step14](docs/InsertionSort_Step14.svg)

![InsertionSort Step15](docs/InsertionSort_Step15.svg)

![InsertionSort Step16](docs/InsertionSort_Step16.svg)

![InsertionSort Step17](docs/InsertionSort_Step17.svg)

![InsertionSort Step18](docs/InsertionSort_Step18.svg)

![InsertionSort Step19](docs/InsertionSort_Step19.svg)

## Testing Interactive Code Blocks

- normal code block

``` js
function insertionSort(array) {
  for (let i = 1; i < array.length; i++) {
    let j = i;
    while (j > 0 && array[j] < array[j - 1]) {
      [array[j - 1], array[j]] = [array[j], array[j - 1]];
      j--;
    }
  }
return array;
}

//testing above code
var unsortedList = [12, 11, 13, 5, 6];
var sortedList = insertionSort(unsortedList);

//return
send.lia("Sortierte Liste: " + sortedList);
"LIA: stop";
```
<script>@input</script>

---

- multiple code blocks (aka Project)

<!-- data-readOnly="true" -->
``` js +insertionSort.js
function insertionSort(array) {
  for (let i = 1; i < array.length; i++) {
    let j = i;
    while (j > 0 && array[j] < array[j - 1]) {
      [array[j - 1], array[j]] = [array[j], array[j - 1]];
      j--;
    }
  }
return array;
}
```
<!-- data-readOnly="false" -->
``` js -main.js
//testing above code
var unsortedList = [12, 11, 13, 5, 6];
var sortedList = insertionSort(unsortedList);

//return
send.lia("Sortierte Liste: " + sortedList);
"LIA: stop";
```
<script>
  @input(0);
  @input(1);
</script>

### ..with input query

<!-- data-readOnly="true" -->
``` js
function insertionSort(array) {
  for (let i = 1; i < array.length; i++) {
    let j = i;
    while (j > 0 && array[j] < array[j - 1]) {
      [array[j - 1], array[j]] = [array[j], array[j - 1]];
      j--;
    }
  }
return array;
}

var tmp = [];
send.handle("input", input => {
  try{
    tmp = input.split(" ").map(Number);
    var result = insertionSort(tmp);
    send.lia("Sortierte Liste: [" + result + "]");
  } catch (e) {
    console.error(e);
  }
});

send.lia("Bitte geben Sie eine unsortierte Liste ein, getrennt durch Leerzeichen:");
"LIA: terminal";
```
<script>@input</script>

### ..with input query & seperate code-blocks

<!-- data-readOnly="true" -->
``` js
var tmp = [];
send.handle("input", input => {
  try{
    tmp = input.split(" ").map(Number);
    send.dispatch("input", tmp);
    //send.lia("LIA: stop"); //if only one input allowed
  } catch (e) {
    console.error(e);
  }
});

send.lia("Bitte geben Sie eine unsortierte Liste ein, getrennt durch Leerzeichen:");
"LIA: terminal";
```
<script>@input</script>

<!-- data-readOnly="true" -->
``` js
function insertionSort(array) {
  for (let i = 1; i < array.length; i++) {
    let j = i;
    while (j > 0 && array[j] < array[j - 1]) {
      [array[j - 1], array[j]] = [array[j], array[j - 1]];
      j--;
    }
  }
return array;
}
```
<!-- style="display:none;" -->
```js
send.register("input", function(e){
  var result = insertionSort(e);
  send.lia("Sortierte Liste: [" + result + "]");
});

"LIA: wait";
```
<script>
  @input(0);
  @input(1);
</script>

## Aus dem LiaScript Handbuch

### Ping Pong

``` js
send.register("ping", function(e){
  console.warn("ping", e)
})

send.handle("input", input => {
  send.dispatch("pong", input)
})

"LIA: terminal" // execute the code and
```
<script>@input</script>

``` js
send.register("pong", function(e){
  console.warn("pong", e)
})

send.handle("input", input => {
  send.dispatch("ping", input)
})

"LIA: terminal" // execute the code and
```
<script>@input</script>

--> **sending data to other code-blocks only possible if all code-blocks are activated!**
