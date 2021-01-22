# Alap matlab függvények

Egy kis irodalom: http://www.mit.bme.hu/oktatas/targyak/vimia305/matlab illetve sok jó leírás itt: https://youproof.hu/blog/

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

**Függvényhívások**
```Matlab
% maximum kiválasztás
max() %argumentumként sorvektort beadva egy értéket akpunk vissza maximumként
      %argumentumként mátrixot beadva minden egyes oszlop maximumát kapjuk meg sorvektorként
      
% B =  0     2     4     6     8    10    12    14
max(B)
%   14

%A =
%    16     2     3    13
%     5    11    10     8
%     9     7     6    12
%     4    14    15     1

max(A)
%    16    14    15    13

%két vektor maximuma/minimuma
BB = rand(1,8)
% BB =    0.2760    0.6797    0.6551    0.1626    0.1190    0.4984    0.9597    0.3404
max(B,BB)
%     0.2760    2.0000    4.0000    6.0000    8.0000   10.0000   12.0000   14.0000
min(B,BB)
%         0    0.6797    0.6551    0.1626    0.1190    0.4984    0.9597    0.3404

% egyszerre több visszatérési érték változóba mentése
[max, location] = max(B)
%maxA =
%    14
%
%location =
%     8
```

**Ábrázolások, grafikonok**
**Vonal görbék**
```MATLAB
% 0-tól 2PI-ig a szinusz függvény:
x = 0:pi/100:2*pi;
y = sin(x);
plot(x,y)

% tengelyek feliratának hozzáadása
xlabel('x')
ylabel('sin(x)')
title('Plot of the Sine Function')

% színes szaggatott vonallal rajzolás, pl piros szaggatottal
plot(x,y,'r--')

% Két grafikon egymásra tétele
x = 0:pi/100:2*pi;
y = sin(x);
plot(x,y)

hold on

y2 = cos(x);
plot(x,y2,':')
legend('sin','cos')

hold off

% 3D grafikon
[X,Y] = meshgrid(-2:.2:2);    % koordinátarendszer, méretek, -tól - -ig ábrázolás                            
Z = X .* exp(-X.^2 - Y.^2);   % 3. függvény

surf(X,Y,Z)                   % kirajzolás


% több grafikon egyyben
% alább 2 sorban
%       2 oszlopban
%       rajzolunk ki rafikonokat, a harmadik input azt adja meg, hogy melyik aktív

t = 0:pi/10:2*pi;
[X,Y,Z] = cylinder(4*cos(t));
subplot(2,2,1); mesh(X); title('X');
subplot(2,2,2); mesh(Y); title('Y');
subplot(2,2,3); mesh(Z); title('Z');
subplot(2,2,4); mesh(X,Y,Z); title('X,Y,Z');
```

**Programozhatóság és scriptelhetőség**
scriptek készítéséhez csinálunk egy script fájlt:
```Matlab
edit mysphere       %edit fájlnév
```
Ekkor kreálódik egy `mysphere.m.` fájl.
```Matlab
% Create and plot a sphere with radius r.
[x,y,z] = sphere;       % Create a unit sphere.
r = 2;
surf(x*r,y*r,z*r)       % Adjust each dimension and plot.
axis equal              % Use the same scale for each axis. 
 
% Find the surface area and volume.
A = 4*pi*r^2;
V = (4/3)*pi*r^3;
```
Futtatásához írjuk be a script nevét a parancssorba: `mysphere`

A készített grafikon átkonvertálható `MATLAB live code file (*.mlx)`-á ami egy `live script`. Ehhez a `save as` menüponton keresztül jutunk el. A készített függvényekhez dokumentációkat írhatunk a `doc` parancsal, pl a `mean` függvéyn dokumentációja ami a `mean(`begépelése után jelenik meg í]y adható meg:
```Matlab
doc mean
```

**Ciklusok, feltételek**
```Matlab
N = 100;
f(1) = 1;
f(2) = 1;

for n = 3:N
    f(n) = f(n-1) + f(n-2);
end
f(1:10)

num = randi(100)
if num < 34
   sz = 'low'
elseif num < 67
   sz = 'medium'
else
   sz = 'high'
end
```

