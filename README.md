# TESTING
J
#soy jhocelyn
varon(winsor).
varon(jhonny).
varon(kevin).
varon(benjamin).
varon(jhonatan).
varon(jherson).
varon(alvaro).
varon(jhamil).
varon(cristian).
varon(eduardo).

mujer(carmen).
mujer(sara).
mujer(vicky).
mujer(jhoy).
mujer(jess).

padre_de(eduardo,winsor).
padre_de(eduardo,jhonny).
padre_de(eduardo,vicky).

padre_de(winsor,kevin).
padre_de(winsor,benjamin).
padre_de(winsor,sara).

padre_de(jhonny,jhonatan).
padre_de(jhonny,jherson).
padre_de(jhonny,alvaro).
padre_de(jhonny,jhamil).

madre_de(carmen,winsor).
madre_de(carmen,jhonny).
madre_de(carmen,vicky).

madre_de(vicky,jhoy).
madre_de(vicky,jess).
madre_de(vicky,cristian).
%REGLAS****************************

abuelo_de(X,Y):-padre_de(X,Z),((padre_de(Z,Y));(madre_de(Z,Y))).
abuela_de(X,Y):-madre_de(X,Z),((padre_de(Z,Y));(madre_de(Z,Y))).

hijo_de(X,Y):-varon(X),(padre_de(Y,X);madre_de(Y,X)).
hija_de(X,Y):-mujer(X),(padre_de(Y,X);madre_de(Y,X)).


hermano_de(X,Y):-(padre_de(Z,X),padre_de(Z,Y),not(X=Y),varon(X));(madre_de(Z1,X),madre_de(Z1,Y),not(X=Y),varon(X)),not(X=Y),varon(X).
hermana_de(X,Y):-(padre_de(Z,X),padre_de(Z,Y),not(X=Y),varon(X));(madre_de(Z1,X),madre_de(Z1,Y),not(X=Y),varon(X)),not(X=Y),mujer(X).

tio_de(X,Y):-varon(X),((padre_de(P,Y),hermano_de(X,P);madre_de(M,Y),hermano_de(X,M));(padre_de(X,M2),madre_de(AU,M2),(hermana_de(AU,M1),madre_de(M1,Y);hermana_de(AU,P1),padre_de(P1,Y)))).
tia_de(X,Y):-mujer(X),((padre_de(P,Y),hermana_de(X,P);madre_de(M,Y),hermana_de(X,M));(madre_de(X,M2),padre_de(AU,M2),(hermano_de(AU,M1),madre_de(M1,Y);hermano_de(AU,P1),padre_de(P1,Y)))).

sobrino_de(X,Y):-hijo_de(X,P),(hermano_de(P,Y);hermana_de(P,Y)).
sobrina_de(X,Y):-hija_de(X,P),(hermano_de(P,Y);hermana_de(P,Y)).


nieto_de(X,Y):-abuelo_de(Y,X);abuela_de(Y,X),varon(X).
nieta_de(X,Y):-abuela_de(Y,X);abuelo_de(Y,X),mujer(X).
