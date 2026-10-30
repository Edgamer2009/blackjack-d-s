# blackjack-d-s
import random
def lancerde() -> int:
    return random.randint(1,6)


def adepasse(score : int) -> bool:
    return score > 11
    score += lancerde()
    b = adepasse(score + lancerde())
    print(b)

def valideractionjoueur():
    RED: str = "\u001B[31m"
    while True :
        commande = input("veuillez appuyez sur r pour rester et entrée pour arreter: ")
        if commande == "" or commande == "r":
            return commande
        else:
            print(f"{RED} saisie invalide")

def tourjoueur():
    continuer = True
    RED: str = "\u001B[31m"
    BLUE: str = "\u001B[34m"
    totaltour = 0
    while continuer == True :
        commande = valideractionjoueur()
        if commande == "r":
            score = lancerde()
            print(f"vous avez eu {score}")
            totaltour += score
            print(f"votre total est de {totaltour}")
            if totaltour > 11:
                print(f"{RED}vous avez perdu")
                continuer = False
            else :
                print(valideractionjoueur)
        elif adepasse(totaltour):
            print(f"{RED} vous avez perdu")
            continuer = False
        elif commande == "":
            print(f"{BLUE} vous avez arrêté")
            continuer = False
        else:
            print(f"{RED} saisie invalide")
    return totaltour


import random
import time

    
def tourcroupier():
    RED: str = "\u001B[31m"
    GREEN: str = "\u001B[32m"
    scorecroupier = 0
    while scorecroupier <= 11:
        score = random.randint(1, 6)
        scorecroupier += score
        if scorecroupier > 11:
            print(f"{GREEN} le croupier a perdu")
        elif scorecroupier == 11:
            print(f"{RED} le croupier a gagné")
        else:
            print(f"le croupier a tiré {score}")
            print(f"le score du croupier est de: {scorecroupier}")
        time.sleep(0.2)
    return scorecroupier

def afficheresultatmanche(score_joueur : int, score_croupier : int) -> int:
    print(f"votre score est de : {score_joueur}")
    print(f"le score du croupier est de : {score_croupier}")
    RED: str = "\u001B[31m"
    BLUE: str = "\u001B[34m"
    GREEN: str = "\u001B[32m"
    if score_joueur > 11 and score_croupier <= 11:
        print(f"{RED} le croupier gagne (-5$)")
    elif score_joueur > 11 and score_croupier > 11:
        print(f"{BLUE}vous avez tous les deux dépassé 11 votre prime reste stable")
    elif score_joueur == score_croupier:
        print(f"{BLUE} égalité")
    elif score_joueur <= 11 and score_croupier > 11:
        print(f"{GREEN} vous gagnez la manche! (+5$)")
    elif score_joueur > score_croupier:
        print(f"{GREEN} vous gagnez la manche! (+5$)")
    else:
        print(f"{RED} le croupier gagne! (-5$)")

    
def determineresultat(score_joueur: int, score_croupier: int) -> int:
    if score_joueur > 11 and score_croupier > 11:
        resultat = 0
    elif score_joueur > 11 or score_joueur < score_croupier:
        resultat = -1
    elif score_croupier > 11 or score_joueur > score_croupier:
        resultat = 1
    else:
        resultat = 0

    return resultat


def validerejouer() -> str:
    commande = ""

    while commande != "o" and commande != "n":
        commande = input(f"{BLUE} voulez-vous rejouer ? o pour oui, n pour non : ")

        if commande != "o" and commande != "n":
            print("saisie invalide")

    if commande == "n":
        print(f"{BLUE} vous avez arrêté")

    return commande
def calculertauxvictoire(nbvictoires: int, nbmanches: int) -> int:
    if nbmanches == 0:
        return 0
    else:
        taux = (nbvictoires / nbmanches) * 100
        print(f"{GREEN} le taux de victoire est : round{taux:.2f}")

def afficherstatistiques(nb_manches: int, nb_victoires: int, nb_defaites: int, nb_egalites: int):
    RESET: str = "\u001B[0m"
    RED: str = "\u001B[31m"
    BLUE: str = "\u001B[34m"
    GREEN: str = "\u001B[32m"
    egalites = nb_manches - (nb_victoires + nb_defaites)
    print(f"{BLUE} ---statistiques---")
    print(f"{GREEN} victoires : {nb_victoires}")
    print(f"{RED} défaites: {nb_defaites}")
    print(f"{BLUE} égalité : {egalites}")
    print(f"{GREEN} taux de victoires: {tauxvictoire}")
    print(f"{GREEN} votre argent est à: {argent}$")
    return afficherstatistiques
resultat : int = 0
argent : int = 15
choix : str = "o"
nb_manches = 0
nb_victoires = 0
nb_defaites = 0
nb_egalites = 0
BLUE: str = "\u001B[34m"
while argent != 30 and argent != 0 and choix  != "n" :
    if nb_manches == 0:
        tauxvictoire = 0
    else:
        tauxvictoire = (nb_victoires / nb_defaites) * 100
    scorjoueur = tourjoueur()
    scorcroupier = tourcroupier()
    afficheresultatmanche(scorjoueur, scorcroupier)
    if scorjoueur < scorcroupier:
        argent -= 5
    elif scorjoueur == scorcroupier:
        print(f"{BLUE} votre prime reste stable")
    elif scorjoueur > 11:
        argent -= 5
    else :
        argent += 5
        resultat = determineresultat(scorjoueur, scorcroupier)
    nb_manches += 1

    if resultat == 1:
        nb_victoires += 1
        argent += 5
    elif resultat == -1:
        nb_defaites += 1
        argent -= 5
    else:
        nb_egalites += 1
        print(f"{BLUE} prime neutre")

    choix = validerejouer()
afficherstatistiques(nb_manches, nb_victoires, nb_defaites, nb_egalites)
