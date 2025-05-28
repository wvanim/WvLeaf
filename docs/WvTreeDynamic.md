Arbre à neoud alterné : temps/espace
TreeDynamic : Arbre temps/espace
	Noeud : DynamicDataProducer(temps)/IrlGroup alternés(espace)
	feuille : IrlMetier (espace)

2 formats de temps
	- temps asynchrone : dit "à la volée", à tout moment, envoie de données au DynamicDataProducer
	- temps de balayage : invocation linéaire, ou multithread.
		lock les événements du temps asynchrone, placés dans une plie d'attente
		un jeton suit les branches de DynamicDataProducer en IrlGroup
			pour terminer par une DynamicDataProducer et un IrlMetier

DynamicDataProducer DDP : service temporel de production d'IrlComponent et de données
	Seul composant traitant le temps. 
	Reçoit et stock les données en temps réel. 
 
DatasLocal : données traitées localement
PropagatedDatas : donnée transmise de noeud en noeud, valeurs agrégées durant le parcours de la branche.
IrlComponent : Composant concret. réuni les  IrlMetier et les IrlGroup
IrlMetier : Composant de terminaison de branche (feuille) transmise au métier
	Exemple image, texte, dessin vectoriel, son, vidéo...
IrlGroup : Composant groupant plusieurs DDP (noeud)
IrlCourant : component accroché au DynamicDataProducer lors du temps de balayage
	l'IrlCourant peut être soit IrlGroup IrlMetier
DynamicNode : noeud logique qui associe le DynamicDataProducer avec son IrlCourant
Scheduler : accompagne le groupe DynamicDataProducer pour définir l'ordre de traitement

Composition

Schéduler
	reçoit le jetons te les datas du Groupe container
	tranmet le jeton séquentiellement aux DynamicDataProducer de l'IrlGroup

DynamicDataProducer
	Temps asynchrone
		Pointe sur l'IrlCourant reçu
		Stock les dataLocal reçu
		Stock les PropagatedDatas reçu
	temps de balayage
		reception du jeton et des PropagatedDatas du groupe-container
		transmet les dataLocal et les PropagatedDatas à l'IrlCourant
		passe à l'IrlCurrent le jeton et les PropagatedDatas du groupe-container

IrlComponent
	temps de balayage uniquement 
		reception des DataLocal du DynamicDataProducer
		=> traite les Datalocal
		reception des PropagatedDatas du DynamicDataProducer
		
		reception du jeton et des PropagatedDatas du groupe-container
		calcul la fusion des PropagatedDatas du groupe-container avec les DataLocal du DynamicDataProducer
		
si UrlGroup
	transmet le jeton au Scheduler contenu dans le Groupe

si UrlMetier
	transmet cet UrlMetier et ces PropagatedDatas au Métier 