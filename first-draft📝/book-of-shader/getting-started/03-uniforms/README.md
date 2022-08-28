# Uniforms

> Bien que chaque thread soit aveugle, nous devons être capables de passer certaines valeurs depuis le CPU vers le GPU et les threads en question. Du fait de l'architecture des cartes graphiques, ces valeurs vont devoir être également (ou uniform-ément) distribuées sur tous les threads et - comme décrit au chapitre 1 - utilisées en lecture seule. Autrement dit, tous les threads reçoivent les mêmes données, chacun peut les lire mais pas les modifier.
