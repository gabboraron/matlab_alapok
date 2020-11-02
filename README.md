# Alap matlab függvények

Egy kis irodalom: http://www.mit.bme.hu/oktatas/targyak/vimia305/matlab

**Változók, vektorok, mátrixok, komplex számok**
```MATLAB
%változók
a = 5
b = 2
c = a + b %7

%vektorok
a = [1 2 3 4]

%mátrixok
a = [1 2 3; 4 5 6; 7 8 10]
%     1     2     3
%     4     5     6
%     7     8    10

%nullmátrix/vektor:
z = zeros(5,1) %(sor,oszlop)

%egységmátrix/vektor:
z_ones = ones(5,5)

%random értékekkel mátrix/vektor
z_rand = rand(5,5)

%mátrix transzponált:
a'

%mátrix inverz:
inv(a)

%mátrixok szorzása
mat_b = [2 2;2 2]
mat_c = [3 3; 3 3]
mat_b*mat_c
%    12    12
%    12    12  

%mátrixok elemenkénti szorzása:
mat_b.*mat_c
%     6     6
%     6     6

%hasonló elven lehet hatvnyozni, osztani stb, pl:
mat_b.^2
%     4     4
%     4     4

%mátrixok összefűzése:
BC = [mat_b, mat_c]
%     2     2     3     3
%     2     2     3     3
     
%függőleges összefűzés
Bc = [mat_b;mat_c]
%     2     2
%     2     2
%     3     3
%     3     3


%komplex számok
sqrt(-1)
%ans = 0.0000 + 1.0000i

C = [3 + 4i, 4 + 3j; -i, 10]
%   3.0000 + 4.0000i   4.0000 + 3.0000i
%   0.0000 - 1.0000i  10.0000 + 0.0000i
```

**Vektorok indexelése**
```Matlab
A = magic(4)
%    16     2     3    13
%     5    11    10     8
%     9     7     6    12
%     4    14    15     1

A(4,2)
%14

% részvektor kiválasztása:
% A(kezdő_sor_index:tartomány_végső_sor_index,oszlopindex)
A(1:3,2)
%     2
%     11
%     7

%hasonlóan sorokra is, vagy teljes sorokra:
A(3,:)
%      9     7     6    12     0

%vektor definiálása kezdőindex:lépésmérték:végeindex formában
B = 0:10:100
%     0    10    20    30    40    50    60    70    80    90   100
```

**használt változók, stb figyelése**
```Matlab
% összes kiiratása
whos

% Name        Size            Bytes  Class     Attributes

%   A           4x4               128  double              
%   B           1x8                64  double              
%   BC          2x4                64  double              
%   Bc          4x2                64  double              
%   C           2x2                64  double    complex   
%   a           3x3                72  double              
%   ans         1x1                 8  double              
%   b           1x1                 8  double              
%   c           1x1                 8  double              
%   e           1x1                 8  double              
%   mat_b       2x2                32  double              
%   mat_c       2x2                32  double              
%   p           3x3                72  double              
%   z           5x5               200  double              
%   z_ones      5x5               200  double              
%   z_rand      5x5               200  double              

%változók kimentése
save myfile.mat

% változók törlése
clear 

% betöltés fájlból
load myfile.mat
```

**Szövegek**
```Matlab
t = "Hello, world";
q = "Something ""quoted"" and something else." %duplán kell "-be tenni az " jeleket ha meg akarjuk tartani karakterként
%    "Something "quoted" and something else."

whos t
%  Name      Size            Bytes  Class     Attributes
%
%  t         1x1               174  string     

% összefűzés
f = 71;
c = (f-32)/1.8;
tempText = "Temperature is " + c + "C"
%    "Temperature is 21.6667C"

% karaktertömbök hasonlóan:
seq = 'GCTAGAATCC';
seq(4)
%    'A'

seq2 = [seq 'ATTAGAAACC']
%    'GCTAGAATCCATTAGAAACC'
```

**Függvények és függvényhívások**
```Matlab

```
