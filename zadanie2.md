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
