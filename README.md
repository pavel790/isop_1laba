# isop_1laba
Factorial1[arg1_] := 
  If[arg1 == 0, 1, 
   If[arg1 < 0, "Отрицательный", Factorial1[arg1 - 1]*arg1]];
arg1 = 6;
Print[Factorial1[arg1]];


P1 = 100;
P2 = 300;
P3 = 500;
Obl = Table[0, {100}, {100}];
signal = Table[0, {100}, {100}];
Vyshky = Table[RandomInteger[{1, 100}], {10}, {2}];
For[k = 1, k < 6, k++,
  For[i = 1, i < 101, i++,
   For[j = 1, j < 101, j++,
    If[i == Vyshky[[k, 1]] && j == Vyshky[[k, 2]], signal[[i, j]] = P1,
     Obl[[i, j]] = 
      P1/((i - Vyshky[[k, 1]])^2 + (j - Vyshky[[k, 2]])^2);
     If[Obl[[i, j]] > signal[[i, j]], 
      signal[[i, j]] = Obl[[i, j]]]]]]];

For[k = 6, k < 9, k++, 
  For[i = 1, i < 101, i++, 
   For[j = 1, j < 101, j++, 
    If[i == Vyshky[[k, 1]] && j == Vyshky[[k, 2]], 
     signal[[i, j]] = P2, 
     Obl[[i, j]] = 
      P2/((i - Vyshky[[k, 1]])^2 + (j - Vyshky[[k, 2]])^2);
     If[Obl[[i, j]] > signal[[i, j]], 
      signal[[i, j]] = Obl[[i, j]]]]]]];

For[k = 9, k < 11, k++, 
  For[i = 1, i < 101, i++, 
   For[j = 1, j < 101, j++, 
    If[i == Vyshky[[k, 1]] && j == Vyshky[[k, 2]], 
     signal[[i, j]] = P3, 
     Obl[[i, j]] = 
      P3/((i - Vyshky[[k, 1]])^2 + (j - Vyshky[[k, 2]])^2);
     If[Obl[[i, j]] > signal[[i, j]], 
      signal[[i, j]] = Obl[[i, j]]]]]]];

sum = 0;
People = Table[RandomInteger[{1, 1000}], {100}, {100}];
For[i = 1, i < 101, i++,
 For[j = 1, j < 101, j++,
  If[signal[[i, j]] > 1, sum += People[[i, j]]]]]
sum
SUM = 0;
For[i = 1, i < 101, i++,
 For[j = 1, j < 101, j++,
  If[signal[[i, j]] >= 0, SUM += People[[i, j]]]]]
SUM
N[sum/SUM]*100
ListPlot3D[signal]





M = Table[0, {i, 15}, {j, 15}];
M[[3, 2]] = 1;
M[[3, 13]] = 1;
M[[5, 13]] = 1;
M[[5, 15]] = 1;
M[[10, 15]] = 1;
M[[10, 2]] = 1;


inah = 0;
jnah = 0;
For[i = 1, i < 16, i++,
  For[j = 1, j < 16, j++,
   If[M[[i, j]] == 1, If[inah != 0, Break[], inah = i; jnah = j]]]];

Cycle = False;
nahPointi = inah;
nahPointj = jnah;

Print["M[", inah, ",", jnah, "]"];
While[Cycle == False,
  iPrev = inah;
  For[i = inah, i < 16, i++,
   If[M[[i, jnah]] == 1, inah = i]
   ];
  For[i = iPrev, i < inah, i++,
   If[M[[i, jnah]] == 0 && iPrev < i < inah, M[[i, jnah]] = 2]
   ];
  If[inah == iPrev,
   For[i = inah, i > 0, i--,
      If[M[[i, jnah]] == 1, inah = i]
      ]
     For[i = iPrev, i > inah, i--,
      If[M[[i, jnah]] == 0 && iPrev > i > inah, M[[i, jnah]] = 2]
      ];
   ];
  
  
  
  Print["M[", inah, ",", jnah, "]"];
  
  If[nahPointi == inah && nahPointj == jnah, Cycle = True];
  
  jPrev = jnah;
  
  For[j = jnah, j < 16, j++,
   If[M[[inah, j]] == 1, jnah = j]
   ];
  For[j = jPrev, j < jnah, j++,
   If[M[[inah, j]] == 0 && jPrev < j < jnah, M[[inah, j]] = 2]
   ];
  If[jnah == jPrev,
   For[j = jnah, j > 0, j--,
      If[M[[inah, j]] == 1, jnah = j]
      ]
     For[j = jPrev, j > jnah, j--,
      If[M[[inah, j]] == 0 && jPrev > j > jnah, M[[inah, j]] = 2]
      ];
   ];
  
  Print["M[", inah, ",", jnah, "]"];
  
  If[nahPointi == inah && nahPointj == jnah, Cycle = True];
  
  
  ];
Print[MatrixForm[M]];

