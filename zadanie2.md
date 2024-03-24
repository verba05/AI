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
    \\+lubi(X, Y),
    \\+lubi(Y,X).

niby_przyjazn(X, Y) :-
    (lubi(X, Y) , \\+lubi(Y, X));
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
rodzic(grzegorz, ola).
rodzic(ala, ola).
rodzic(jakub, jan). 
rodzic(monika, jan).
rodzic(jan, olek).
rodzic(ola, olek).
rodzic(ola, eva).
rodzic(jan, eva).
rodzic(jakub, alex).
rodzic(ola, alex).
rodzic(alex, dominika).
rodzic(katarzyna, dominika).

m(jan). 
m(jakub).
m(grzegorz).
m(olek).
m(kacper). 
m(alex).
m(jakub).
osoba(jan).
osoba(olek). 
osoba(ola). 
osoba(jakub). 
osoba(grzegorz).
osoba(ala).
osoba(monika).
osoba(alex).
osoba(eva).
osoba(dominika).
osoba(katarzyna).

k(X) :- \+m(X).

ojciec(X, Y) :- rodzic(X,Y) , m(X) , osoba(X), osoba(Y).

matka(X, Y) :- rodzic(X, Y), k(X), osoba(X), osoba(Y).

corka(X, Y) :- k(X), rodzic(Y, X), osoba(X), osoba(Y).

brat_rodzony(X, Y) :- matka(Matka, X), matka(Matka, Y), ojciec(Ojciec, Y),
    ojciec(Ojciec, X), m(X), osoba(X), osoba(Y).

brat_przyrodni(X, Y) :- ((matka(Matka, X), matka(Matka, Y), ojciec(Ojciec1, X), ojciec(Ojciec2, Y),
                          (Ojciec1 \= Ojciec2));
                          (ojciec(Ojciec, X), ojciec(Ojciec, Y), matka(Matka1, X), matka(Matka2, Y),
                          (Matka1 \= Matka2))), osoba(X), osoba(Y), m(X).

siostra_rodzona(X, Y) :- matka(Matka, X), matka(Matka, Y), ojciec(Ojciec, Y),
    ojciec(Ojciec, X), k(X), osoba(X), osoba(Y).

siostra_przyrodnia(X, Y) :- ((matka(Matka, X), matka(Matka, Y), ojciec(Ojciec1, X), ojciec(Ojciec2, Y),
                          (Ojciec1 \= Ojciec2));
                          (ojciec(Ojciec, X), ojciec(Ojciec, Y), matka(Matka1, X), matka(Matka2, Y),
                          (Matka1 \= Matka2))), osoba(X), osoba(Y), k(X).

rodzenstwo(X, Y) :-
    (   brat_rodzony(X, Y) ; brat_przyrodni(X, Y) ; siostra_rodzona(X, Y) ; siostra_przyrodnia(X, Y)   ), osoba(X), osoba(Y).



kuzyn(X, Y) :- ojciec(Ojciec1, X), matka(Matka1, X), ojciec(Ojciec2, Y), matka(Matka2, Y),
    (  rodzenstwo(Ojciec1, Ojciec2) ; rodzenstwo(Ojciec1, Matka2) ; rodzenstwo(Matka1, Ojciec2) ; rodzenstwo(Matka1, Matka2)  ),
    osoba(X), osoba(Y), m(X).

dziadek_od_strony_ojca(X, Y) :-
    ojciec(Ojciec, Y), ojciec(X, Ojciec).

dziadek_od_strony_matki(X, Y) :-
    matka(Matka, Y), ojciec(X, Matka), osoba(X), osoba(Y).

babcia(X, Y) :- 
    matka( Matka, Y ), ojciec(Ojciec, Y), ( matka(X, Matka) ; matka(X, Ojciec) ), osoba(X), osoba(Y).

wnuczka(X, Y) :- babcia(X, Y) ; dziadek_od_strony_ojca(X, Y); dziadek_od_strony_matki(X, Y).

przodek_do2pokolenia_wstecz(X,Y) :- ojciec(X, Y) ; matka(X, Y) ; babcia(X, Y) ; dziadek_od_strony_matki(X, Y) ; dziadek_od_strony_ojca(X, Y).

przodek_do3pokolenia_wstecz(X,Y) :- przodek_do2pokolenia_wstecz(X, Y) ; (   matka(Matka, Y) , przodek_do2pokolenia_wstecz(X, Matka) ) ;
    (  ojciec(Ojciec, Y) , przodek_do2pokolenia_wstecz(X, Ojciec) ).
