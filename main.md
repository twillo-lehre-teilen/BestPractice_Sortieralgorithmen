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

``` js -insertionSort.js
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

### Testing input query's

``` js
var tmp = [];
send.handle("input", input => {
  try{
    tmp = input;
    send.dispatch("input", tmp);
    send.lia("LIA: stop");
  } catch (e) {
    console.error(e);
  }
});

"LIA: terminal";
```
<script>@input;</script>

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
```js
send.register("input", function(e){
  console.warn("stop", e);
});
```
<script>
  @input(0);
  @input(1);
</script>

## Ping Pong

```
send.register("ping", function(e){
  console.warn("ping", e)
})

send.handle("input", input => {
  send.dispatch("pong", input)
})

"LIA: terminal" // execute the code and
```
<script>@input</script>

```
send.register("pong", function(e){
  console.warn("pong", e)
})

send.handle("input", input => {
  send.dispatch("ping", input)
})

"LIA: terminal" // execute the code and
```
<script>@input</script>

## Executable Code

You can make your code executable and define projects:

``` js     -EvalScript.js
let who = data.first_name + " " + data.last_name;

if(data.online) {
  who + " is online"; }
else {
  who + " is NOT online"; }
```
``` json    +Data.json
{
  "first_name" :  "Sammy",
  "last_name"  :  "Shark",
  "online"     :  true
}
```
<script>
  // insert the JSON dataset into the local variable data
  let data = @input(1);

  // eval the script that uses this dataset
  eval(`@input(0)`);
</script>
