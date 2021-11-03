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

## Grundlagen

## InsertionSort

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
