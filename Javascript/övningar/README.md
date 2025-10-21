# JavaScript Övningar

## Instruktioner

**Filstruktur:**

1. Skapa en HTML-fil med namnet `övningar-javascript.html`
2. Skapa separata JavaScript-filer för varje övning: `övning1.1.js`, `övning1.2.js`, etc.
3. Referera till rätt JavaScript-fil i HTML-filen med `<script src="övning1.1.js"></script>`

**Exempel på HTML-struktur:**

```html
<!DOCTYPE html>
<html>
  <head>
    <title>JavaScript Övningar</title>
  </head>
  <body>
    <h1>JavaScript Övningar</h1>

    <!-- Kommentera ut de övningar du inte arbetar med för tillfället -->
    <script src="övning1.1.js"></script>
    <!-- <script src="övning1.2.js"></script> -->
    <!-- <script src="övning1.3.js"></script> -->
  </body>
</html>
```

**Arbetsprocess:**

- Använd `console.log()` för att visa resultat i webbläsarens konsol (F12)
- Använd `console.log()` när det specificeras i övningen
- Kommentera ut andra script-taggar när du arbetar med en specifik övning
- Ladda upp alla filer till GitHub när du är klar

## Innehåll

1. [Variabler](#11-variabler)
2. [Datatyper](#12-datatyper)
3. [Operatorer](#13-operatorer)
4. [Jämförelser](#14-jämförelser)
5. [If-satser](#15-if-satser)
6. [Loopar](#16-loopar-while-och-for)
7. [Switch](#17-switch-satsen)
8. [Funktioner](#18-funktioner)
9. [Objekt](#19-objekt)
10. [Arrays](#110-listor-arrays)
11. [Arrow functions](#111-arrow-functions-pil-funktioner)
12. [Array filter med arrow functions](#112-array-filter-med-arrow-functions)
13. [Asynkron JavaScript](#113-asynkron-javascript-promises)

---

## 1.1 Variabler

### Övningsuppgifter

### **Övning 1.1.1 - Grundläggande variabler**

1. Deklarera 3 variabler: `name`, `age`, `hasDriverLicense`
2. Tilldela värden: `"Kalle Kula"`, `18`, `true`
3. Skriv ut alla variabler till konsolen

### **Övning 1.1.2 - Kopiera variabler**

1. Deklarera två variabler: `admin` och `name`
2. Tilldela värdet `"John"` till `name`
3. Kopiera värdet från `name` till `admin`
4. Skriv ut värdet på `admin` med `console.log()` (ska visa "John")

### **Övning 1.1.3 - Variabelnamngivning**

1. Skapa en variabel med namnet på vår planet (fundera på bra variabelnamn)
2. Skapa en variabel för att lagra namnet på en webbplatsbesökare (fundera på bra variabelnamn)

### **Övning 1.1.4 - Konstanter**

1. Skapa en konstant `pi` med pi-värdet (3 decimaler)
2. Försök tilldela `pi` ett annat värde
3. Skriv ut `pi` med `console.log()` - vad händer och varför?

## 1.2 Datatyper

### Övningsuppgifter

### **Övning 1.2.1 - Identifiera datatyper**

**Uppgift:** Fundera först över vilka datatyper följande värden har, skriv ner dina gissningar:

1. `undefined`
2. `0`
3. `3.14`
4. `"3.14"`
5. `true`
6. `"foo"`
7. `Math`
8. `null`
9. `5 > 4`

**Kontroll:** Skriv sedan ut typerna med `console.log(typeof värde)` för att se om du hade rätt.

## 1.3 Operatorer

### Övningsuppgifter

### **Övning 1.3.1 - Grundläggande räkneoperationer**

1. Skapa 2 variabler med valfria tal (t.ex. `tal1 = 5`, `tal2 = 3`)
2. Skriv ut addition, subtraktion och multiplikation av talen med `console.log()`

### **Övning 1.3.2 - Prefix och postfix**

**Fråga:** Vilka är de slutliga värdena för `a`, `b`, `c` och `d`?

```javascript
let a = 1,
  b = 1;
let c = ++a; // ?
let d = b++; // ?
```

**Kontroll:** Bekräfta genom att skriva ut värdena med `console.log()`.

### **Övning 1.3.3 - Tilldelningsoperatorer**

**Fråga:** Vilka värden får `a` och `x`?

```javascript
let a = 2;
let x = 1 + (a *= 2);
```

**Kontroll:** Bekräfta med `console.log()`.

### **Övning 1.3.4 - Typkonvertering**

**Fråga:** Vad blir resultatet av detta uttryck? Gissa först!

```javascript
"" + 1 + 0;
```

**Kontroll:** Bekräfta med `console.log()`.

## 1.4 Jämförelser

### Övningsuppgifter

### **Övning 1.4.1 - Jämförelseoperatorer**

**Fråga:** Vad blir resultatet för dessa uttryck? Gissa först!

```javascript
1. 5 > 4
2. "apple" > "pineapple"
3. "2" > "12"
```

**Kontroll:** Bekräfta med `console.log()`.

## 1.5 If-satser

### Övningsuppgifter

**Övning 0. If sats**

1. Skapa en variabel med `age` som tilldelas värdet 16.
2. Används if-sats för att kontrollera om age är större eller lika med 18. Stämmer det skriv ut "Du får ta körkort".
3. Utöka sedan med else del där du skriver du skriver ut "Du får inte ta körkort!".

**Övning 1. If sats**

1. Ta en ett namn från användaren med _prompt_ och tilldela det till en variabel name.
2. Använd en if-sats för att kontrollera om namnet är "Kalle". Stämmer det skriv ut "Du heter Kalle".
3. Utöka sedan med else del där du skriver ut "Du heter inte Kalle!".

**Övning 2. Namnet Javascript**<br>
Med `if..else`-konstruktionen, skriv koden som frågar: "Vad är det officiella namnet på JavaScript?"

Använd `prompt()` för att läsa in ett värde från användaren.

Om besökaren skriver in "ECMAScript", skriver du ut "Korrekt!", Annars skriver du ut: "Du vet inte? ECMAScript!”
![Första Javascript programmet!](https://github.com/abbjoafli/Programmering-1/blob/master/img/if_exercise_3.png?raw=true)
<br>

**Övning 3. Visa tecknet**<br>
Använd `if..else` och skriv koden som tar in ett nummer med `prompt()` och visar sedan med `console.log()` beroende på värdet:

- `1`, om värdet är större än noll,
- `-1`, om mindre än noll,
- `0`, om det är lika med noll.

I denna uppgift antar vi att vi alltid får in ett nummer.

**Övning 4. Skriv om 'if' med '?'**<br>
Skriv om `if` så att vi istället använder `?` operatorn:

```
let result;
let a = 1;
let b = 2;

if (a + b < 4) {
  result = 'Below';
} else {
  result = 'Over';
}
```

## 1.6 Loopar: while och for

### Övningsuppgifter

**Övning 0. For-loop**<br>
Skapa en for-loop som skriver ut siffrorna 1-10.

**Övning 1. While-loop**<br>
Skapa en while-loop som skriver ut siffrorna 1-10.

**Övning 2. Vilka värden visas av while-loopen?**<br>
För varje loop-iteration, skriv ner vilket värde det matar ut och jämför sedan det med lösningen.

Båda looparna skriver ut samma värden eller inte?

1. prefix formen `++i`:

```
let i = 0
while (++i < 5) {
  console.log( i )
}
```

2. postfix formen `i++`:

```
let i = 0;
while (i++ < 5) {
  console.log( i );
}
```

**Övning 3. Vilka värden visas av for-loopen?**<br>
För varje loop ska du skriva ner vilka värden den ska visa. Jämför sedan med svaret.

Båda looparna skriver ut samma värden eller inte?

1. postfix formen:

```
for (let i = 0; i < 5; i++) {
  console.log( i );
}

```

2. prefix formen:

```
for (let i = 0; i < 5; ++i) {
  console.log( i );
}

```

**Övning 4. Skriv ut jämna siffror i loopen**<br>
Använd `for`-loopen för att skriva ut jämna siffror från `2` till `10`.

**Övning 5. Ersätt "for"-loopen med "while"-loopen**<br>
Skriv om koden som ändrar `for`-loopen till `while`-loopen utan att ändra dess beteende (utgången ska förbli densamma).

```
for (let i = 0; i < 3; i++) {
  console.log( `number ${i}!` );
}
```

## 1.7 Switch-satsen

### Övningsuppgifter

**Övning 1. Skriv om "switch"-satsen till "if"-satser**<br>
Skriv koden med `if..else` som motsvarar följande switch:

```
switch (browser) {
  case 'Edge':
    console.log( "You've got the Edge!" );
    break;

  case 'Chrome':
  case 'Firefox':
  case 'Safari':
  case 'Opera':
    console.log( 'Okay we support these browsers too' );
    break;

  default:
    console.log( 'We hope that this page looks ok!' );
}
```

**Övning 2. Skriv om "if"-satserna till "switch"-satsen**<br>
Skriv im koden nedan med hjälp av ett enda `switch`-sats:

```
let a = +prompt('a?', '');

if (a == 0) {
  console.log( 0 );
}
if (a == 1) {
  console.log( 1 );
}

if (a == 2 || a == 3) {
  console( '2,3' );
}
```

## 1.8 Funktioner

### Övningsuppgifter

### **Övning 1.8.1 - Enkel adderingsfunktion**

1. Skapa en funktion `add` som tar in 1 parameter `x` och returnerar `x + x`
2. Anropa funktionen med värdet 5 och skriv ut resultatet med `console.log()`

### **Övning 1.8.2 - Funktioner med if-satser**

**Uppgift:** Följande funktion returnerar `true` om `age` är högre än 18, annars skriver den ut "Du är för ung tyvärr!":

```javascript
function checkAge(age) {
  if (age > 18) {
    return true;
  } else {
    console.log("Du är för ung tyvärr!");
  }
}
```

**Fråga:** Fungerar funktionen annorlunda om `else`-delen tas bort?

```javascript
function checkAge(age) {
  if (age > 18) {
    return true;
  }
  console.log("Du är för ung tyvärr!");
}
```

Testa båda varianterna och förklara skillnaden.

**Övning 2. Skriv om funktionen med '?' eller '||'**<br>
Följande funktion returnerar sant om parametern `age` är högre än 18.
Annars skriver den ut "Du är för ung tyvärr!":

```
function checkAge(age) {
  if (age > 18) {
    return true;
  } else {
    // ...
    console.log('Du är för ung tyvärr!');
  }
}
```

**Övning 3. Funktionen min(a, b)**<br>
Skriv en funktion `min(a, b)` som returnerar det minsta av två siffror `a` och `b`.
Till exempel:

```
min(2, 5) == 2
min(3, -1) == -1
min(1, 1) == 1
```

### **Övning 1.8.4 - Potens-funktion**

Skriv en funktion `pow(x, n)` som returnerar `x` upphöjt till `n`. Med andra ord: multiplicera `x` med sig själv `n` gånger.

**Exempel:**

```javascript
pow(2, 3) == 8; // 2 * 2 * 2
pow(3, 2) == 9; // 3 * 3
pow(5, 1) == 5; // 5
```

**Tips:** Använd en loop för att multiplicera `x` med sig själv `n` gånger.

## 1.9 Objekt

### Övningsuppgifter

**Övning 0. Ett djur-objekt**<br>

1. Skapa ett valfritt djur med minst 3 egenskapar, tex `cat` och egenskaperna: color, age, name.
2. Skapa några metoder på objektet också, tex sound och sleep som skriver ut något till konsolen.
3. Lägg till egenskapen `surname` med värdet `Smith`.
4. Skriv ut egenskaperna med console.log().
5. Anropa metoderna.

**Övning 1. Hello Objekt**<br>
Skriv koden, en rad för varje åtgärd:

1. Skapa en tom objekt `user`.
2. Lägg till egenskapen `name` med värdet `John`.
3. Lägg till egenskapen `surname` med värdet `Smith`.
4. Ändra på värdet av `name` till `Pete`.
5. Ta bort egenskapens `namn` från objektet.

**Övning 2. Kolla efter tomhet**<br>
Skriv funktionen `isEmpty(obj)` som returnerar `true` om objektet inte har några egenskaper, `false` annars.
Bör fungera så här:

```
let schedule = {};

console.log( isEmpty(schedule) ); // true

schedule["8:30"] = "get up";

console.log( isEmpty(schedule) ); // false
```

**Övning 3.Summera objekt egenskaper**<br>
Vi har ett objekt som lagrar löner för vårt team:

```
let salaries = {
  John: 100,
  Ann: 160,
  Pete: 130
}
```

Skriv koden för att summera alla löner och lagra den variabelb `sum`. Bör vara `390` i exemplet ovan.

Om `salaries` är tomma, måste resultatet vara `0`.

**Övning 4. Multiplicera numeriska egenskaper med 2**<br>
Skapa en funktion `multiplyNumeric(obj)` som multiplicerar alla numeriska egenskaper för `obj` med `2`.

Till exempel:

```
// before the call
let menu = {
  width: 200,
  height: 300,
  title: "My menu"
};

multiplyNumeric(menu);

// after the call
menu = {
  width: 400,
  height: 600,
  title: "My menu"
};
```

Observera att `multiplyNumeric` inte behöver returnera någonting. Det bör ändra objektet på plats.

P.S. Använd `typeof()` för att kontrollera ifall det är ett nummer.

## 1.10 Listor (Arrays)

### Övningsuppgifter

**Övning 1. Loopa igenom array med namnen i er grupp**<br>

1. Skapa en array med namn på alla gruppmedlemmar.
2. Använd en for-loop och loopa igenom alla gruppmedlemmar i arrayen/listan.
3. För varje medlem skriv ut namnet med `console.log()`.

### **Övning 1.10.2 - Array-referenser**

**Fråga:** Vad kommer denna kod att visa? Gissa först!

```javascript
let fruits = ["Apples", "Pear", "Orange"];

// Skapa en "kopia"
let shoppingCart = fruits;
shoppingCart.push("Banana");

// Vad finns i fruits nu?
console.log(fruits.length); // ?
```

**Kontroll:** Kör koden och förklara resultatet. Varför blev det så?

**Övning 3. Array operationer**<br>

Låt oss prova 5 arrayoperationer.

1. Skapa en array `styles` med "Jazz" och "Blues".
2. Lägg till "Rock-n-Roll" till slutet av listan.
3. Byt ut värdet i mitten med "Classics". Din kod för att hitta mittvärdet bör fungera för alla listor med udda längd.
4. Ta bort det första värdet i listan och visa det.
5. Lägg till `Rap` och `Reggae` längst fram i listan.

Så här ser resultatet ut i varje steg:

```
Jazz, Blues
Jazz, Blues, Rock-n-Roll
Jazz, Classics, Rock-n-Roll
Classics, Rock-n-Roll
Rap, Reggae, Classics, Rock-n-Roll
```

## 1.11 Arrow functions (pil-funktioner)

### Övningsuppgifter

### **Övning 1.11.1 - Max-funktion med arrow function**

Skriv en arrow function `max(a, b)` som returnerar det största av två siffror `a` och `b`.

**Exempel:**

```javascript
max(2, 5) == 5;
max(3, -1) == 3;
max(1, 1) == 1;
```

**Tips:** Använd syntaxen `const max = (a, b) => { ... }`

## 1.12 Array filter med arrow functions

### Övningsuppgifter

### **Övning 1.12.1 - Filtrera användare efter ålder**

Skapa en array med användarobjekt och använd `filter()` metoden med en arrow function för att hitta alla användare som är över 17 år.

**Exempel:**

```javascript
const users = [
  { name: "Anna", age: 25 },
  { name: "Karl", age: 16 },
  { name: "Sara", age: 18 },
  { name: "Erik", age: 15 },
];
const adults = users.filter(/* arrow function här */);
console.log(adults);
```

## 1.13 Asynkron JavaScript (Promises)

### Övningsuppgifter

### **Övning 1.13.1 - Skapa ett Promise**

Skapa en funktion `waitForSeconds(seconds)` som returnerar ett promise som resolvar efter det angivna antalet sekunder.

**Exempel:**

```javascript
function waitForSeconds(seconds) {
  // Returnera ett promise här
}

waitForSeconds(2).then(() => {
  console.log("2 sekunder har gått!");
});
```

**Tips:** Använd `setTimeout()` tillsammans med `new Promise()`.

### **Övning 1.13.2 - Använd Promises med .then()**

Skapa en funktion `getRandomNumber()` som returnerar ett promise. Promise ska resolva med ett slumpmässigt tal mellan 1-100 efter 1 sekund.

Använd `.then()` för att:

1. Ta emot talet
2. Skriva ut det till konsolen
3. Testa om talet är större än 50

**Exempel:**

```javascript
getRandomNumber().then((number) => {
  console.log("Slumpmässigt tal:", number);
  if (number > 50) {
    console.log("Talet är större än 50!");
  } else {
    console.log("Talet är mindre än eller lika med 50!");
  }
});
```

### **Övning 1.13.3 - Använd Promises med async/await**

Skapa en funktion `fetchUserData(userId)` som returnerar ett promise. Promise ska resolva med ett användarobjekt efter 1 sekund.

Skapa sedan en `async` funktion `displayUserInfo(userId)` som använder `await` för att:

1. Hämta användardata
2. Skriva ut användarens namn och ålder
3. Hantera fel med try/catch

**Exempel:**

```javascript
function fetchUserData(userId) {
  return new Promise((resolve) => {
    setTimeout(() => {
      resolve({
        id: userId,
        name: "Anna Andersson",
        age: 25,
      });
    }, 1000);
  });
}

async function displayUserInfo(userId) {
  try {
    // Använd await här
  } catch (error) {
    console.log("Något gick fel:", error);
  }
}

displayUserInfo(1);
```
