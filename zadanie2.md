# Wstęp.
plec(bartek, m).
plec(krzysztof, m).
plec(pawel, m).
plec(jan, m).
plec(ala, k).
plec(ola, k).
plec(ania, k).
lubi(jan, pawel).
lubi(pawel, krzysztof).
lubi(pawel, jan).
lubi(jan, pawel).
lubi(bartek, jan).
lubi(ola, pawel).
lubi(pawel, ola).



nieprzyjazn(X, Y) :-
    \+lubi(X, Y),
    \+lubi(Y,X).

niby_przyjazn(X, Y) :-
    (lubi(X, Y) , \+lubi(Y, X));
    (lubi(Y, X) , lubi(X, Y)).

loves(X, Y):-
    lubi(X, Y) , ((plec(X, m) , plec(Y, k)) ; (plec(X, k) , plec(Y, m))).

true_love(X, Y) :-
    loves(X, Y) , loves(Y, X).
    
    
# 1.1
a) rodzeństwo
b) kuzyni
c) swaci
d) pasierb-ojczym
e) rodzeństwo przyrodnie
f) bratowa - brat

# 2
rodzic(jan, olek).
rodzic(ola, olek).
rodzic(ola, kacper).
rodzic(jan, kacper).
rodzic(jakub, jan).
rodzic(grzegorz, ola).
rodzic(ala, ola).
rodzic(monika, jan).
m(jan).
m(jakub).
m(grzegorz).
m(olek).
m(kacper).
osoba(jan).
osoba(olek).
osoba(ola).
osoba(jakub).
osoba(grzegorz).
osoba(ala).
osoba(monika).
osoba(kacper).

k(X) :-
    \+m(X).

ojciec(X, Y) :-
    rodzic(X,Y) , m(X) , osoba(X), osoba(Y).

matka(X, Y) :-
    rodzic(X, Y), k(X), osoba(X), osoba(Y).

corka(X, Y) :-
    k(X), rodzic(Y, X), osoba(X), osoba(Y).

brat_rodzony(X, Y) :-
    matka(Matka, X), matka(Matka, Y), ojciec(Ojciec, Y), ojciec(Ojciec, X), m(X), osoba(X), osoba(Y).
