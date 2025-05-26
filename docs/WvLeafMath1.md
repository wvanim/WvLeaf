Version restrurée
Voici une réorganisation structurée avec chaque symbole mathématique explicitement lié à son concept, dans un format adapté à une publication théorique sur arXiv :

---

### **§2.1 - Fondements Structurels**

#### **Définition 2.1.1 (Pièce)**
Une **Pièce** est un nœud temporel noté :

$$
\pi = (\tau, \Phi)
$$

où :
- $\tau \subseteq \mathbb{R}^+$ (**timeline**) : ensemble d'instants contrôlant l'activation des faces  
- $\Phi \subseteq \mathcal{F}$ (**faces**) : ensemble des éléments visuels/sonores affichables  

*Exemple* :  
$\pi_{\text{bouton}} = (\{0, 0.5, 1\}, \{\phi_{\text{repos}}, \phi_{\text{clic}}\})$ gère un bouton à 2 états.

---

#### **Définition 2.1.2 (Groupe)**
Un **Groupe** est un nœud spatial noté :

$$
\gamma = (M, \Pi)
$$

où :
- $M \in \mathbb{R}^{4×4}$ (**matrice de transformation**) : applique translations/rotations/échelles  
- $\Pi \subseteq \mathcal{P}$ (**pièces enfants**) : sous-éléments temporels  

*Remarque* :  
$M$ utilise des coordonnées homogènes pour unifier les transformations affines.

---

### **§2.2 - Relations Structurelles**

#### **Contrainte 2.2.1 (Alternance)**
La relation parent-enfant $\rightarrow$ suit :

$$
\forall x \rightarrow y,\ 
\begin{cases}
x \in \mathcal{P} \Rightarrow y \in \{\mathcal{G} \cup \mathcal{F}\} \\
x \in \mathcal{G} \Rightarrow y \in \mathcal{P}
\end{cases}
$$

*Interprétation* :  
- Une Pièce ($\mathcal{P}$) ne peut contenir que des Groupes ($\mathcal{G}$) ou Faces ($\mathcal{F}$)  
- Un Groupe ($\mathcal{G}$) ne peut contenir que des Pièces ($\mathcal{P}$)

---

#### **Propriété 2.2.2 (Acyclicité)**
Le graphe orienté $G = (V, E)$ vérifie :

$$
\nexists (v_1 \rightarrow v_2 \rightarrow \dots \rightarrow v_k) \text{ tel que } v_1 = v_k
$$

*Conséquence* :  
Garantit l'absence de dépendances circulaires (ex : une Pièce ne peut être son propre parent).

---

### **§2.3 - Sémantique Opérationnelle**

#### **Fonction 2.3.1 (Rendu)**
L'évaluation à l'instant $t$ est donnée par :

$$
\text{eval}(t)(\pi)(M)(v) = \text{render}\left(
\underbrace{\text{current\_face}(\pi, t)}_{\text{Face active}}, 
\underbrace{M \circ \text{transform}(\pi, t)}_{\text{Matrice composite}}, 
v
\right)
$$

où :
- $\text{current\_face} : \mathcal{P} \times T \rightarrow \mathcal{F}$ sélectionne la Face à afficher  
- $\text{transform} : \mathcal{P} \times T \rightarrow S$ calcule la transformation locale  

---

### **Encadré Technique : Choix des Matrices 4×4**
*Pourquoi pas des quaternions ?*  
Les matrices homogènes 4×4 permettent :
1. **Unification** des transformations (rotation *et* translation)  
2. **Composition** via produit matriciel ($M_1 \circ M_2$ toujours définie)  
3. **Projection** 3D→2D intégrée (dernière ligne modifiable)

Contre-exemple :  
Les quaternions excellent pour les rotations pures mais échouent sur les translations.

---

### **Domaine d'Application**
Ce formalisme relève de :
1. **Informatique Théorique** (cs.IT) :  
   - Modèle de graphe alterné  
   - Complexité des opérations (Théorème 3.1)  
2. **Mathématiques Appliquées** (math.NA) :  
   - Algèbre des transformations affines  
   - Analyse asymptotique  

*Exemple concret* :  
L'animation d'un bouton ($\S$5) démontre comment ces fondements s'appliquent en pratique.

---

Cette structuration :
- Lie chaque symbole à un concept implémentable  
- Justifie les choix mathématiques (ex: matrices vs quaternions)  
- Positionne clairement le travail dans le paysage académique  

À adapter selon les normes de soumission arXiv (sections, bibliographie, etc.).