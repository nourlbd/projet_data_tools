#Projet Data Science Tools

Scrapping des sites sens-critique et IMDB.  
Ce travail relève d'un projet réalisé par des étudiants de  l'ESME Sudria.

##La problématique

L'objectif de ce projet était de proposer un programme répertoriant les meilleurs films de l'histoire selon plusieurs sources, et ensuite d'utiliser ces données pour établir un profil type de films à succès.


##Scrapped website 
        - https://www.imdb.com/
        
        - https://www.senscritique.com/
Nous avons décidé de pratique le scrapping non pas sur 1 mais bien sur 2 sites 
possédant des bases de données sur des films et ceux afin de mutltiplier les sources et de pouvoir faire des comparaisons.


Pour cela il suffit de lancer le fichier **Scrapping.py** dont on peut avoir un aperçu en sélectionnant le fichier *Scrapping.ipynb*

Avec les url des sites nous avons pu demander des requests et ainsi obtenir de nombreuses informations quant aux films exposés sur la plateforme.

Nous avons ensuite fait un DataFrame pour réunir les données et pouvoir les traiter plus facilement.

On a donc un DataFrame avec pour colonnes :

            -  Titres des filmes
            -  Année de sortie des films
            -  Les notes obtenues par ces films
            -  Les liens menant à la page de ces films
            -  Le nom du réalisateur 
            -  Le genre du film
            -  La durée du film
            -  Les noms des trois acteurs principaux 
            -  Le budget aloué au film
            -  La description du film 

Pour obtenir ces informations il fallait scrapper en recherchant les balises adéquates et en ajoutant toutes ces données à des liste, que l'on fusionnera plus tard en DataFrame. 

    def get_genres(link):
    all_genres=[]
    for links in link:
        html = requests.get(links)
        soup = BeautifulSoup(html.text)
        all_genre_div = soup.find_all("div", { "class" : "see-more inline canwrap"})
        for liste_genres in all_genre_div:
            if liste_genres.h4.text=="Genres:":
                genre=(liste_genres.a.text)
                all_genres.append(genre)
    return all_genres

Voici la fonction utilisée pour récupérer les genres des films, le processus pour récupérer les autres attribut est identique à ceci près qu'il faut modifier les balises.

Avec ces DataFrame on a réalisé des classements, notamment des classements de popularité comme on a pu le faire avec le genre des films
            
    group=df.groupby(["genres"]).agg(
        Classement=("classement","sum"))

Ainsi on a pu comparer sur les deux sites quels genres sont les plus populaires.

En utilisant la méthode du scrapping sur les deux sites et en réalisant des DataFrame identiques, une comparaison était simple à réaliser et les résultats n'en sont que plus précis.
