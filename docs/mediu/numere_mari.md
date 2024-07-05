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

### Utilizarea bazelor mari

În unele situati, din cauza limitărilor de memorie sau de timp, este necesar să lucrăm cu baze mai mari decât $10$. În aceste situații, putem utiliza baza $10^9$ pentru a stoca numerele mari. Utilizarea acestei baze ne permite să lucrăm cu numere de până la $10^9 - 1$ într-o singură cifră, fiind mult mai eficientă decât lucrul cu baza $10$. Atunci când lucrăm cu baze mai mari, trebuie să avem grijă la citirea și afișarea numerelor deoarece acestea vor trebuie să fie convertite în baza $10$.

### Numere negative

Pentru numerele negative, putem folosi un bit de semn sau putem folosi complementul la 2. În ambele cazuri, trebuie să avem grijă la operațiile de adunare și scădere pentru a evita overflow-ul. In accest ghid nu vom discuta despre numerele negative intrucat acestea nu sunt folosite in majoritatea problemelor de algoritmica.

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

Penru a afișa un număr mare, vom parcurge vectorul de cifre de la cea mai semnificativă cifră la cea mai puțin semnificativă și vom afișa cifrele.

Toate implementările de mai jos presupun că numărul este stocat în vectorul `nr` în ordine inversă și că lungimea numărului este stocată în `nr[0]`, precum am menționat anterior.

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

### Transformarea unui număr într-un număr mare

In unele probleme, numărul este dat ca un număr întreg, iar noi trebuie să-l transformăm într-un număr mare. Pentru a face acest lucru, putem folosi o metodă similară cu cea de mai sus, dar în loc să citim numărul ca un șir de caractere, îl descompunem în cifre.

```cpp
#include <iostream>
#include <vector>
using namespace std;
int main(){
    int n;
    cin >> n;
    vector<int> nr;
    while(n){
        nr.push_back(n % 10);
        n /= 10;
    }
    for(int i = nr.size() - 1; i >= 0; i--)
        cout << nr[i];
}
```

### Adunarea numerelor mari

Pentru a aduna două numere mari, vom parcurge vectorii de cifre de la cea mai puțin semnificativă cifră la cea mai semnificativă și vom aduna cifrele corespunzătoare. Dacă suma cifrelor este mai mare decât $9$, atunci vom adăuga $1$ la cifra următoare.

```cpp
void adauga(vector<int> &a, vector<int> &b){
    if(a[0] < b[0]){
        // daca a are mai putine cifre decat b, adaugam cifre 0 la finalul lui a ca să ne asigurăm că a și b au aceeași lungime
        a.resize(b[0] + 1);
        a[0] = b[0];
    }


    int rest = 0; // ținem minte dacă suma cifrelor este mai mare decât 9

    for(int i = 1; i <= a[0]; ++i){

        // doar daca i <= b[0] adunam și cifra corespunzătoare din b altfel continuăm să adunăm doar restul

        if(i <= b[0])
            a[i] += b[i];
        
        a[i] += rest;
        rest = a[i] / 10;
        a[i] %= 10;
    }

    if(rest){
        a.push_back(rest);
        ++a[0];
    }
}
```

Această implementare poate fi vizualizată mai bine în următorul exemplu unde vom aduna numerele $468$ și $712$.

$$
\begin{array}{ccccc}
       & 0 & 1 & 0 & 1 & \text{(prin $1$ am marcat unde am avut un rest)} \\
\hline
       & 8 & 6 & 4 &   & \text{($468$ neinversat)} \\
+      & 2 & 1 & 7 &   & \text{($712$ neinversat)} \\
\hline
       & 0 & 8 & 1 & 1 & \text{($1180$ neinversat, rezultat)} \\
\end{array}
$$

!!! note "Observație"
    În cazul adunării, putem avea nevoie să adăugăm o cifră la finalul vectorului, dacă suma cifrelor este mai mare decât $9$.

### Scăderea numerelor mari

Pentru a scădea două numere mari, vom parcurge vectorii de cifre de la cea mai puțin semnificativă cifră la cea mai semnificativă și vom scădea cifrele corespunzătoare. Dacă diferența dintre cifre este negativă, atunci vom scădea $1$ de la cifra următoare. Următoarea implementare presupune că $a \geq b$.

```cpp
void scade(vector<int> &a, vector<int> &b){

    for(int i = 1; i <= a[0]; ++i){
        if(i <= b[0])
            a[i] -= b[i];
        
        if(a[i] < 0){
            a[i] += 10;
            --a[i + 1];
        }
    }

    while(a[a[0]] == 0 && a[0] > 1)
        --a[0];
}
```

### Înmulțirea unui număr mare cu un intreg

Pentru a înmulți un număr mare cu un număr întreg, vom parcurge vectorul de cifre de la cea mai puțin semnificativă cifră la cea mai semnificativă și vom înmulți fiecare cifră cu numărul întreg. Dacă produsul cifrei cu numărul întreg este mai mare decât $9$, atunci vom adăuga restul la cifra următoare.

```cpp
void inmulteste(vector<int> &a, int b){
    int rest = 0;
    for(int i = 1; i <= a[0]; ++i){
        a[i] = a[i] * b + rest;
        rest = a[i] / 10;
        a[i] %= 10;
    }

    while(rest){
        a.push_back(rest % 10);
        rest /= 10;
        ++a[0];
    }
}
```

!!! note "Observație"
    Implementarea de mai sus este foarte cu similară cu cea de adunare, cu excepția faptului că înmulțirea se face cu un număr întreg.

### Înmulțirea a două numere mari

Pentru a înmulți două numere mari, vom parcurge vectorii de cifre de la cea mai puțin semnificativă cifră la cea mai semnificativă și vom înmulți fiecare cifră a primului număr cu fiecare cifră a celui de-al doilea număr. Produsul cifrelor va fi adăugat la poziția corespunzătoare din vectorul rezultat. Dacă produsul cifrelor este mai mare decât $9$, atunci vom adăuga restul la cifra următoare.

```cpp
vector<int> inmulteste(vector<int> &a, vector<int> &b){
    vector<int> c(a[0] + b[0] + 2, 0);
    c[0] = a[0] + b[0]; // lungimea produsului este cel mult a[0] + b[0], dar poate fi și a[0] + b[0] - 1

    for(int i = 1; i <= a[0]; ++i)
        for(int j = 1; j <= b[0]; ++j){
            c[i + j - 1] += a[i] * b[j];
            c[i + j] += c[i + j - 1] / 10;
            c[i + j - 1] %= 10;
        }

    while(c[c[0]] == 0 && c[0] > 1) // eliminam zerourile nesemnificative dacă lungimea produsului nu este maximă
        --c[0];

    return c;
}
```

Această implementare poate fi vizualizată mai bine în următorul exemplu unde vom înmulți numerele $123$ și $456$.

$$
\begin{array}{cccccc}
       & 3 & 2 & 1 &   &   & \text{($123$ neinversat)} \\
\times & 6 & 5 & 4 &   &   & \text{($456$ neinversat)} \\
\hline
       & 8 & 3 & 7 &   &   & \text{($6 \times 123 = 738$, $j = 1$)} \\
       &   & 5 & 1 & 6 &   & \text{($5 \times 123 = 615$, $j = 2$)} \\
     + &   &   & 2 & 9 & 4 & \text{($4 \times 123 = 492$, $j = 3$)} \\
\hline
       & 8 & 8 & 0 & 6 & 5 & \text{($56088$ neinversat, rezultat)} \\
\end{array}
$$

!!! note "Observație"
    Se poate observa că înmulțirea a două numere mari e foarte similară cu înmulțirea clasică a numerelor învățată la școală, doar că aici lucrăm cu cifrele în ordine inversă.

    $$
    \begin{array}{cccccc}
           &   &   & 1 & 2 & 3 \\
    \times &   &   & 4 & 5 & 6 \\
    \hline
           &   &   & 7 & 3 & 8 & \text{($6 \times 123$, $j = 1$)} \\
           &   & 6 & 1 & 5 &   & \text{($5 \times 123$, $j = 2$)} \\
         + & 4 & 9 & 2 &   &   & \text{($4 \times 123$, $j = 3$)} \\
    \hline
           & 5 & 6 & 0 & 8 & 8 & \text{(Rezultat final)} \\
    \end{array}
    $$

### Impărțirea unui număr mare la un număr întreg

Penru a împărți un număr mare la un număr întreg, vom parcurge vectorul de cifre de la cea mai semnificativă cifră la cea mai puțin semnificativă și vom împărți fiecare cifră la numărul întreg. Restul împărțirii va fi adăugat la cifra următoare.

```cpp
void imparte(vector<int> &a, int b){
    int rest = 0;
    for(int i = a[0]; i > 0; --i){
        rest = rest * 10 + a[i];
        a[i] = rest / b;
        rest %= b;
    }

    while(a[a[0]] == 0 && a[0] > 1)
        --a[0];
}
```

## Probleme și resurse suplimentare

+ [Clasă de numere mari](https://github.com/stefdasca/CompetitiveProgramming/blob/master/Algorithms/bigints.cpp)
+ [Lucrul cu numere mari](https://infoarena.ro/lucrul-cu-nr-mari)
+ [Probleme cu numere mari](https://kilonova.ro/tags/379)
+ [perm3 de pe infoarena](https://www.infoarena.ro/problema/perm3)
+ [pastile, lot juniori 2015](https://kilonova.ro/problems/1663)
+ [număr, OJI 2010 IX](https://kilonova.ro/problems/794)
