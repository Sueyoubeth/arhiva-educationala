---
title: Numere mari
tags:
    - vectori
    - matematica
---

**Autori**: Susan, Ștefan-Cosmin Dăscălescu

Fie $\overline{a_{n-1} a_{n-2} \ldots a_1 a_0}$ un număr în baza $10$, format
din $n$ cifre. Aici, $a_i$ pentru $0 \leq i < n$ sunt cifrele numărului, cu
fiecare $a_i$ satisfăcând $0 \leq a_i \leq 9$, și $a_{n-1} \neq 0$. Valoarea
numărului este dată de:

$$
\overline{a_{n-1} a_{n-2} \cdots a_1 a_0} = \sum_{k=0}^{n-1} a_k \cdot 10^k
$$

Această sumă poate fi descompusă în:

$$
\overline{a_{n-1} a_{n-2} \cdots a_1 a_0} = a_{n-1} \cdot 10^{n-1} + a_{n-2}
\cdot 10^{n-2} + \ldots + a_1 \cdot 10^1 + a_0 \cdot 10^0
$$

Similar, fie $(\overline{a_{n-1} a_{n-2} \ldots a_1 a_0})_b$ un număr în baza
$b$, format din $n$ cifre, unde $a_i$ îndeplinește aceleași condiții ca mai sus.
Valoarea numărului este dată de:

$$
\overline{a_{n-1} a_{n-2} \ldots a_1 a_0}_b = \sum_{k=0}^{n-1} a_k \cdot b^k
$$

Această sumă poate fi descompusă în:

$$
\overline{a_{n-1} a_{n-2} \ldots a_1 a_0}_b = a_{n-1} \cdot b^{n-1} + a_{n-2}
\cdot b^{n-2} + \ldots + a_1 \cdot b^1 + a_0 \cdot b^0
$$

Numerele mari sunt esențiale pentru calcule ce depășesc limita de $2^{63} - 1$.
Acestea se bazează pe reprezentarea cifrică a numerelor. De exemplu, să
reprezentăm numărul $82534$ folosind definiția numerelor în baza $10$:

$$
\begin{align*}
82534 &= 80000 + 2000 + 500 + 30 + 4\\
&= 8 \cdot 10000 + 2 \cdot 1000 + 5 \cdot 100 + 3 \cdot 10 + 4 \cdot 1\\
&= 8 \cdot 10^{4} + 2 \cdot 10^3 + 5 \cdot 10^2 + 3 \cdot 10^1 + 4 \cdot 10^0 \\
\end{align*}
$$

## Reprezentarea numerelor în memorie

Reprezentarea pe cifre a numerelor ne duce cu gândul la reprezentarea numărului
folosind un vector. Astfel, o abordare comună pentru manipularea numerelor mari
în algoritmică este reprezentarea acestora prin intermediul unui vector de
cifre. Considerăm un număr mare, pe care îl descompunem în cifrele sale
componente și le stocăm într-un vector.

!!! example "Exemplu"
    De exemplu, numărul $82534$ poate fi stocat într-un vector $v$ astfel:

    $$
    \begin{array}{r|cccccccc}
    i & 0 & 1 & 2 & 3 & 4 \\
    \hline
    v[i] & 8 & 2 & 5 & 3 & 4 \\
    \end{array}
    $$

### Reprezentarea inversă

O metodă comună de a stoca numerele mari este reprezentarea inversă a acestora. Accest lucru se datorează faptului că adăugarea unui element la începutul unui vector este o operație mai costisitoare decât adăugarea la sfârșitul acestuia. Prin urmare, pentru a evita această operație, putem reprezenta numărul în ordine inversă, astfel încât cifra unităților să fie stocată pe prima poziție a vectorului.

!!! example "Stocare inversă"
    De exemplu, numărul $82534$ poate fi stocat într-un vector $v$ astfel:

    $$
    \begin{array}{r|cccccccc}
    i & 0 & 1 & 2 & 3 & 4 \\
    \hline
    v[i] & 4 & 3 & 5 & 2 & 8 \\
    \end{array}
    $$

<!--
Fie un număr natural $N$ cu cifrele $\overline{a_{n-1} a_{n-2} \ldots a_1 a_0}
$ în baza 10. Reprezentarea inversă a lui $N$ într-un vector $v$ de dimensiune
$n$ este definită astfel:

$$
v[i] = a_{n-i},\,\forall\ 0 \leq i < n
$$

unde $n$ este numărul de cifre ale numărului natural $N$, iar $v[0]$ reprezintă
cifra unităților, $v[1]$ cifra zecilor ș.a.m.d.

!!! note "Observație"

    Numerotarea cifrelor de la coadă, ca în exemplul anterior, este opțională, dar
    este indicată pentru simplificare, deoarece este mult mai simplu să efectuăm
    operațiile dacă păstrăm numărul în memorie în ordine inversă față de cum l-am
    scrie în mod obișnuit. Practic, adăugarea unor valori la pozițiile mai
    nesemnificative este o operație mult mai des întâlnită decât adăugarea la
    începutul numărului, iar când e nevoie, putem crește lungimea numărului plasând
    noua cifră pe poziția $n$, $v[n]$ ținând această valoare.

-->

### Stocarea lungimii în **v[0]**

Pentru a simplifica operațiile cu numere mari, putem stoca lungimea numărului în prima poziție a vectorului. Astfel, pentru un număr $N$ cu $n$ cifre, vectorul $v$ va avea dimensiunea $n+1$, iar $v[0]$ va reprezenta lungimea numărului.

### Cum stocăm numerele mari în C++?

În continuare vom folosi un `vector<int>` pentru a ține cifrele numărului, folosind stocarea inversă a acestora și $v[0]$ pentru a ține lungimea numărului.

!!! note "Observație"
    Există și alte metode de a stoca un număr mare. Ca exemplu se poate folosi `deque` care ne permite să stocăm cifrele în ordinea lor naturală, fără a le inversa cu posibilitatea de a adăuga cifre la începutul numărului.

## Operații de bază pe numere mari

### Citirea și afișarea

Pentru citirea unui număr mare, vom citi lungimea numărului (numărul de cifre)
și apoi cifrele sale, începând de la cea mai puțin semnificativă cifră (cifra
unităților). Pentru afișare, procedăm invers, începând de la cea mai
semnificativă cifră.

În funcție de problema dată, putem citi numărul într-un vector de cifre direct sau va trebui să-l citim ca un șir de caractere și să-l convertim într-un vector de cifre. În continuare, vom prezenta metoda a doua, ambele fiind foarte similare.

```cpp
#include <iostream>
using namespace std;

int main(){
    int n; /* n este lungimea numărului, adică numărul de cifre
    dacă numărul este specificat ca un string atunci n == s.size()
    */
    string s;

    // Citirea numărului din șirul de caractere
    cin >> n >> s;

    vector<int> nr(s.size());
    for(int i = s.size() - 1; i >= 0; i--)
        nr[s.size() - i - 1] = s[i] - '0';

    // Afisarea numărului
    for(int i = nr.size() - 1; i >= 0; i--)
        cout << nr[i];
}
```

## Probleme și resurse suplimentare

* [Clasă de numere mari](https://github.com/stefdasca/CompetitiveProgramming/blob/master/Algorithms/bigints.cpp)
* [Lucrul cu numere mari](https://infoarena.ro/lucrul-cu-nr-mari)
* [Probleme cu numere mari](https://kilonova.ro/tags/379)
* [perm3 de pe infoarena](https://www.infoarena.ro/problema/perm3)
* [pastile, lot juniori 2015](https://kilonova.ro/problems/1663)
* [număr, OJI 2010 IX](https://kilonova.ro/problems/794)
