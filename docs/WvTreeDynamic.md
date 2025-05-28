
  
T=(P,F,G,Fleaf,elements,r) avec :
1.elements(x)≡{y∣y∈x}.
2.F = G∪Fleaf, G∩Fleaf = ∅
3.r∈P,
4.∀p∈P,elements(p)⊆F∪{∅},
5.∀g∈G,elements(g)⊆P∪{∅},
6.∀f∈Fleaf,elements(f)=∅,
7.T est un arbre acyclique
8.Alternance P↔G: 
	∀v∈P∪G,si v∈P, alors elements(v)⊆G∪Fleaf
    si v∈G, alors elements(v)⊆P.
