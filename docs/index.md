# Vers l'infini et au-delà

Dans ce TP, on s'intéresse à l'étude de quelques suites qui convergent vers le nombre $e$.

<center>
    <img src="./images/buzz.png" alt="image" width="500" height="auto">
</center>

## Une suite explicite

### Calcul de termes

On note dans un premier temps $u$ la suite définie pour $n \geqslant 1$ par

$$u_n = \left(1+\frac{1}{n}\right)^n$$

!!! note "Quelques manipulations"

    1. Ouvrez le logiciel Thonny ;
    2. Complétez la fonction `u` ci-dessous pour qu'elle génère les termes de la suite $u$ :

        ``` python title="Implantation de la suite u" linenums="1"
        def u(n):
            return ...
        ```
    3. Enregistrez le fichier puis exécutez le grâce au bouton  <img src="./images/run.png" alt="image" style="vertical-align:middle">
    4. Générez les dix premiers termes de la suite grâce à la commande `[u(k) for k in range(1, 10)]`

Afin de pouvoir comparer avec la véritable valeur de $e$, on se propose de l'importer.  
Au début du script, saisissez la ligne :

``` python title="Importation de e" linenums="1"
from math import e    
```

### Recherche de seuil

1. Vérifiez que l'instruction `abs(u(10)-e)` renvoie `0.12453936835904278`.

    !!! important

        L'instruction `abs(u(10)-e)` correspond mathématiquement à la valeur $\left|u_{10}-e\right|$ qui permet de connaître la distance entre
        le terme $u_{10}$ et la valeur de $e$.

2. L'écart entre le terme $u_{100}$ et $e$ est-il inférieur à $0,001$ ?
3. Déterminer à partir de quel terme, l'écart entre la suite $u$ et le nombre $e$ est inférieur à $0,001$.

    !!! tip

        On peut déterminer ce terme par tatônement en testant les instructions comme `abs(u(800)-e)`.

4. Pour généraliser la recherche d'un terme situé à une certaine distance $d$ de $e$, on propose la fonction suivante :

    ``` python title="Recherche de seuil" linenums="1"
    def seuil(d):
        n = 1

        while abs(u(n)-e) > d:
            n = n + 1

        return n
    ```

5. Testez alors l'instruction `seuil(0.0001)`

### Accélération de la convergence

La méthode de Aitken (ou Delta-2) permet à partir d'une suite convergente de construire une autre suite qui converge plus rapidement vers la même limite.

Avec la suite $u$ définie précédemment par $u_n = \left(1+\frac{1}{n}\right)^n$, on introduit la nouvelle suite $v$ définie par :

$$v_n = u_n - \frac{(u_{n+1}-u_n)^2}{u_n-2u_{n+1}+u_{n+2}}$$

1. Comparez les termes $u_{100}$ et $v_{100}$ avec le nombre $e$.
2. Complétez le code de la fonction `seuil2` adaptée à la suite $v$ :

    ``` python title="Recherche de seuil" linenums="1"
    def seuil2(d):
        n = 1

        while               :
            n = n + 1

        return n
    ```
    
3. Vérifiez la meilleure convergence de $v$ par rapport à $u$ en comparant par exemple `seuil(0.0001)` et `seuil2(0.0001)`.

## Une suite récurrente

Dans cette partie, on modélise des suites pour mettre en avant la formule suivante :

$$e = \frac{1}{0!} + \frac{1}{1!} + \frac{1}{2!} + \frac{1}{3!} + \cdots$$

où $n! = n\times (n-1) \times (n-2) \times \cdots \times 2\times 1$ s'appelle la factorielle de $n$.  

Pour la suite, sauvegardez votre travail et créez un nouveau script vierge.

### Factorielle

<center>
    <img src="./images/fact.png" alt="image" width="100" height="auto">
</center>

On peut définir la factorielle par une suite récurrente assez facilement car pour tout entier naturel $n$ :

$$(n+1)! = (n+1)\times n!$$

On note alors $u$ la suite définie par :

$$\left\lbrace\begin{array}{lcl}u_0&=&1\\ u_{n+1}&=&(n+1)\times u_n\end{array}\right.$$

1. Proposez une fonction `u` définie en Python qui génère la factorielle.
2. Calculez $4!$ de tête et vérifiez votre résultat avec l'instruction `u(4)`.
3. Générez les dix premiers termes de la suite $u$ à l'aide de l'instruction `[u(k) for k in range(10)]`
4. Générez les inverses des dix premières factorielles à l'aide de l'instruction `[1/u(k) for k in range(10)]`
5. Sommez l'ensemble à l'aide de la fonction `sum` avec l'instruction `sum([1/u(k) for k in range(10)])`

### Sans la fonction somme

La formule $\frac{1}{0!} + \frac{1}{1!} + \frac{1}{2!} + \frac{1}{3!} + \cdots$ peut se générer avec une suite récurrente.  

Si pour tout entier naturel $n$, on pose $v_n = \frac{1}{0!} + \frac{1}{1!} + \cdots + \frac{1}{n!}$, on a alors :

$$v_{n+1} = v_n + \frac{1}{(n+1)!}$$

avec $v_0 = 1$ pour initialiser.

1. Proposez une fonction `v` définie en Python qui génère les termes de $v$.
2. Vérifiez que l'instruction `v(10)` renvoie une valeur approchée de $e$.
3. Écrivez une fonction `seuil` qui détermine le premier terme de la suite $v$ située à une distance inférieur à $d$ de $e$.
4. Comparez la valeur de `seuil(0.0001)` avec les valeurs obtenues pour la suite explicite et la suite accélérée de la partie I.