

## 1.1 Nomi delle variabili
I nomi delle variabili sono composti da lettere e numeri, si iniziano sempre con una lettera. 
`_` è considerato un carattere, spesso sconsigliato utilizzarlo come inizio di una variabile perchè sono utilizzati da molti variabili delle librerie.
Alcune parole come `if, else, int, float` e così via sono riservati ad uso esclusivo del linguaggio.

## 1.2 Tipi dimensioni dei dati
| Tipo      | Descrizione                                                                                                                         | Note                                                             | Size  |
| --------- | ----------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------- | ----- |
| char      | un singolo byte in grado ti contenere un carattere dell'ambiente in cui risiede il compilatore                                      | Usato per il testo MA è un numero! `'A'=65`, `'a'=97`, `'0'=48`. | 8bit  |
| int       | un intero, solitamente pari alla dimensioe naturale degli interi sulla macchina                                                     |                                                                  | 32bit |
| float     | numero con virgola mobile, precisione singola                                                                                       |                                                                  |       |
| double    | numero con virgola mobile, precisazione doppia                                                                                      |                                                                  |       |
| short int | più corto di int, idea 16bit e non deve superare int. (spesso va bene anche dichiarazione solo `short`, senza `int`)                |                                                                  | 16bit |
| long int  | spesso più lungo di int, idea 32bit e non può essere superato da int. (spesso va bene anche dichiarazione solo `long`, senza `int`) |                                                                  | 64bit |
L'attributo signed (con segno) o unsigned (privo di segno) può essere applicato a char o a qualunque intero.
_"Se in un'operazione c'è un `float` e un `int`, il C converte tutto in `float` prima di calcolare."_

## 1.3 Costanti
### Interi
- **Decimali:** `1234` (int).
- **Long:** `1234L` (long).
- **Unsigned:** `1234U` (unsigned).
- ⚠️ **Ottale (Base 8):** Inizia con `0`. Esempio: `037` **NON** è 37! È $3 \cdot 8^1 + 7 \cdot 8^0 = 31$. 111111111
- ⚠️ **Esadecimale (Base 16):** Inizia con `0x`. Esempio: `0x1F`. 2222
### Caratteri (`char`)

- Si scrivono con **apici singoli**: `'x'`.
- **TRUCCO ESAME:** Sono **numeri interi**!
    - `'0'` vale **48** (non zero!).
    - `'A'` vale **65**.
    - `'a'` vale **97**.
- **Escape:** `'\n'` (a capo), `'\0'` (fine stringa, vale 0).
### Stringhe

- Si scrivono con **doppi apici**: `"ciao"`.
- Sono array di caratteri che finiscono **sempre** con `'\0'` nascosto.
- `"x"` è diverso da `'x'` (la prima è un array di 2 byte: 'x' + '\0', il secondo è un intero).
### Enum (Enumerazioni)

- Lista di costanti intere. Se non specifico valori, parte da 0.
- Esempio: `enum boolean {NO, YES};` -> `NO` vale 0, `YES` vale 1.
- Utile per definire tipi personalizzati (es. `ColoreSemaforo` negli esercizi pag 24, esercizio 3). 


## 1.4 Dichiarazioni e Inizializzazioni

### Variabili Semplici
- **Dichiarazione:** Si può fare su una riga o su più righe.
    - `int a, b, c;` (risparmio spazio).
    
	- `int a;`
    - `int b;` (più leggibile).
- **Inizializzazione:** Assegnare un valore subito.
    - `int a = 0;`
    - `char esc = '\\';`
    - ⚠️ **Importante:** Se non inizializzi una variabile locale (dentro una funzione), il suo valore è **spazzatura** (random), non zero!
- 
### Qualificatore `const`
- Indica che la variabile **non cambierà mai**.
- `const double PIGRECO = 3.14159;`
- Utile per rendere il codice più sicuro (se provi a cambiarlo, il compilatore ti dà errore).
### Array (Vettori)
È una lista di variabili dello stesso tipo.
- **Dichiarazione:** `tipo nome[dimensione];`
    - Esempio: `int giorni[12];`
- **Indici:** Partono sempre da **0**!
    - Se dichiari `a[3]`, gli elementi sono `a[0]`, `a[1]`, `a[2]`.
    - `a[3]` non esiste (errore classico d'esame: _buffer overflow_).
- **Inizializzazione Array:**
    - Completa: `int a[3] = {10, 20, 30};`
    - Parziale: `int a[10] = {1, 2};` (mette 1 e 2 nei primi due posti, e **riempie di 0 tutto il resto**).
    - Senza dimensione (solo se inizializzi subito): `int a[] = {1, 2, 3, 4};` (il compilatore conta da solo che sono 4).
- 

## 1.5 Operatori Aritmetici
### Elenco Operatori
- **`+`** (somma), **`-`** (sottrazione).
- **`*`** (moltiplicazione).
- **`/`** (divisione).
- **`%`** (modulo / resto).

### Regole d'Oro per l'Esame (DA IMPARARE A MEMORIA)
**1. La Divisione Intera (Il "Troncamento")**
- Se entrambi gli operandi sono `int`, il risultato è **troncato** (perde la virgola, non arrotonda!).
- Esempio K&R: `5 / 2` fa **2**, non 2.5!
- _Esercizio PDF:_ In un frammento di codice, c'è `val / 2`. Se `val` è dispari (es. 9), il risultato è 4. Sapere questo è l'unico modo per prevedere l'output corretto. (pag. 24, esercizio 4.)

**2. L'Operatore Modulo (`%`) - Il Re degli Esercizi**
- Restituisce il **resto** della divisione intera.
- **Non funziona** con `float` o `double` (solo interi!).
- **A cosa serve?(nel PDF)**
    - **Pari/Dispari:** `x % 2 == 0` (pari), `x % 2 != 0` (dispari).
    - **Multipli:** `x % 5 == 0` (è multiplo di 5).
    - **Estrarre cifre:** `x % 10` ti dà l'ultima cifra di un numero (es. `123 % 10 = 3`). Fondamentale per gli esercizi ricorsivi sulle cifre. (pag 192.)
    - **Conversioni:** Usato per convertire decimale in binario/ottale.

**3. Comportamento con i Negativi**

- Il troncamento di `/` e il segno di `%` con numeri negativi dipendevano dalla macchina nel vecchio C (K&R).
- _Nota moderna:_ Oggi (C99 in poi) la divisione tronca verso zero (`-5 / 2 = -2`).

**4. Traboccamento (Overflow/Underflow)**
- **Overflow:** Quando il risultato è troppo grande per il contenitore (es. superi 2 miliardi in un `int` positivo). Il numero "riparte" dal valore minimo negativo (comportamento ciclico).
- **Underflow:** Quando scendi sotto il minimo.
- _Esercizio PDF:_ È implicito quando ti chiedono "numero minimo di bit per rappresentare X": se usi meno bit, vai in overflow!
### Gerarchia delle Precedenze (Chi vince?)

1. **Parentesi `( )`** (Vincono su tutto).
2. **Unari `+ -`** (Es. `-5`, il segno).
3. **Moltiplicazione, Divisione, Modulo `* / %`** (Si eseguono da sinistra a destra).
4. **Addizione, Sottrazione `+ -`** (Si eseguono da sinistra a destra).

> **Esempio trabocchetto:** `a = 2 + 5 % 2;` Prima si fa `5 % 2` (che fa 1). Poi `2 + 1`. Risultato: **3**. Se sbagli la precedenza faresti `7 % 2` = 1. Risultato diverso!

## 1.6 Operatori relazionali e logici
**Gli Operatori Relazionali:**
`>`   `>=`    `<`    `<=`
Hanno tutti pari precedenza tra di loro, un po più basso rispetto gli operatori di **eguaglianza**: `==` e `!=`
Invece l'operatore logico `&&` ha diritto di precedenza rispetto a `||`, entrambi eseguono dopo altre operazioni (Relazionali, Aritmetici, Eguaglianza).

**1. Controllo di Flusso: Evitare && complessi** 

(Es 2.2) Quando un ciclo `for` o `while` ha troppe condizioni con `&&`, è meglio usare la **logica inversa** con `break` per rendere il codice più leggibile. 
**Logica:** Invece di dire "Continua SE A e B e C", diciamo "Fermati SE non A, oppure SE non B...". 
#### Esempio Pratico Originale (illeggibile): 
```c 
for(i=0; i<lim-1 && (c=getchar()) != EOF && c != '\n'; i++)

//DIVENTA
while (i < lim - 1) {
    c = getchar();
    if (c == EOF) break;  // Controllo fine file
    if (c == '\n') break; // Controllo invio
    
    s[i] = c;
    i++;
}
```


## 1.7 Conversione di Tipo
**La Regola della Promozione** 
Il C cerca sempre di non perdere dati. 
Se mischio tipi diversi in un'operazione, il tipo "piccolo" diventa "grande". 
* `char` diventa `int`. 
* `int` diventa `float` (se c'è di mezzo un float). 
**Maiuscole vs Minuscole** (La funzione `lower`)
In C non esiste "trasforma in minuscolo". 
Esiste solo la matematica. 
Le lettere ASCII sono numeri ordinati. 
* 'A' = 65 ... 'Z' = 90 
* 'a' = 97 ... 'z' = 122 

**La logica:** Tra la 'A' (maiuscola) e la 'a' (minuscola) c'è una **distanza fissa**. 
Per trasformare 'C' in 'c', devo aggiungere quella distanza.  
**Formula Universale:** 
`minuscola = maiuscola + ('a' - 'A');`
**Esempio di codice (Simil-K&R):** 
```c 
int lower(int c) { 
	if (c >= 'A' && c <= 'Z') { // Se è una lettera maiuscola 
		return c + 'a' - 'A'; // Aggiungo il "gap" per arrivare alle minuscole 
	} else { 
	return c; // Altrimenti la lascio com'è 
	} 
}
```

*Questa logica funziona SOLO se il set di caratteri è **ASCII** (dove le lettere sono tutte vicine). Su vecchi sistemi IBM (EBCDIC), le lettere non sono consecutive e questo codice si romperebbe. Ma per il 99% dei computer moderni, funziona.*


//Jumped nel capitolo 3 del libro AHAH