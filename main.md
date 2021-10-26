<!--
author:   twillo

email:    support.twillo@tib.eu

version:  0.0.1

language: de

narrator: Stina Schäfer, Lennart Rosseburg

comment:  Eine Selbstlerneinheit mit interaktiven Programmieraufgaben für die gängigsten Sortieralgorithmen.

link:     https://de.wikiversity.org/wiki/Kurs:Algorithmen_und_Datenstrukturen/Vorlesung/Sortieren

script:   
-->

# Testing Interactive Code Blocks

## InsertionSort

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
