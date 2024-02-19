# Marstermind
projet NSI



![image](https://github.com/Lfolcher/Marstermind/assets/157314656/16c236e3-1b6c-4167-86db-5b47b5bbeec9)

# le code:

import time
import pygame
from random import *
import math

pygame.init()

def draw_circle(COULEUR, pcercle, rcercle):
    pygame.draw.circle(screen, COULEUR, pcercle, rcercle, 4)
    pygame.draw.circle(screen, COULEUR, pcercle, 23)

song = pygame.mixer.Sound("E:\projet top secret\musiquee.mp3")
NOK = pygame.mixer.Sound("E:\projet top secret\lNOK.mp3")
OK = pygame.mixer.Sound("E:\projet top secret\OK.mp3")
win = pygame.mixer.Sound("E:\projet top secret\win.mp3")
lose = pygame.mixer.Sound("E:\projet top secret\lose.mp3")
commencer = pygame.mixer.Sound("E:\projet top secret\commencer.mp3")
liam = pygame.mixer.Sound("E:\projet top secret\liam.mp3")
bouton = pygame.mixer.Sound("E:\projet top secret\lebouton.mp3")

jouer = True
while jouer == True:

    song.play(10, 144000, 2000)

    scren = pygame.display.set_mode((1200, 650))
    pygame.display.set_caption("Mastermind")
    fenetre = pygame.display.set_mode((1201, 665))
    fond = pygame.image.load("E:\projet top secret\omega medusa.jpg")
    fond = fond.convert()
    icon_32x32 = pygame.image.load("E:\projet top secret\icon.jpg")
    pygame.display.set_icon(icon_32x32)
    fermer = True
    x = 10  # taille des ronds
    button = pygame.Rect(0, 650, x, 15)

    continuer = True
    while continuer:
        liam.play(0, 7000, 2000)
        for i in range(1):  # carré de la pseudo barre de chargement
            for evenement in pygame.event.get():
                if evenement.type == pygame.QUIT:
                    continuer = False
                    fermer = False
                    jouer = False
                    continue
            if x >= 1200:
                continuer = False
            pygame.display.flip()
            fenetre.blit(fond, (0, 0))
            button = pygame.Rect(0, 650, x, 15)
            x += 1
            pygame.draw.rect(scren, (228, 228, 228), button)

    pygame.display.quit()

    screen = pygame.display.set_mode((0, 2850))
    pygame.display.set_caption("Mastermind")
    fenetre = pygame.display.set_mode((600, 1000))
    font = pygame.image.load("E:\projet top secret\dfond.jpg")
    font = font.convert()
    icon_32x32 = pygame.image.load("E:\projet top secret\icon.jpg")
    pygame.display.set_icon(icon_32x32)
    bord = pygame.Rect(460, 0, 140, 860)
    button = pygame.Rect(500, 650, 70, 70)
    buttonR = pygame.Rect(500, 750, 70, 70)
    nombre_essai = 0
    gagner = False
    nombre_essai_X4 = 0
    positionX = 50
    position3 = 0
    positionY = 1
    couleur = ["yellow", "blue", "red", "green", "white", "black"]
    resultat = [0, 0, 0, 0]
    code_couleur_codificateur = []
    code_couleur_decodeur = []
    continuer2 = True
    mapolice1 = pygame.font.SysFont("unicod", 40)
    mapolice2 = pygame.font.SysFont("unicod", 35)
    label_victoire1 = mapolice1.render("OK", True, (255, 255, 255), None)
    label_victoire2 = mapolice2.render("NOK", True, (255, 255, 255), None)

    ligne = pygame.Rect(245, 20, 15, 800)  # ligne de séparation
    ligne2 = pygame.Rect(30, 820, 390, 15)

    bordimage = (pygame.image.load("E:\projet top secret\dfondcote.jpg"))
    bordimage = bordimage.convert()

    gagner_fin = False

    rayon_cercle = 30
    position_cercle1 = (530, 50)
    position_cercle2 = (530, 150)
    position_cercle3 = (530, 250)
    position_cercle4 = (530, 350)
    position_cercle5 = (530, 450)
    position_cercle6 = (530, 550)

    attendre = False

    for i in range(4):  # choix code couleur par le bot
        coleur_alleatoire = choice(couleur)
        code_couleur_codificateur.append(coleur_alleatoire)
    copie_code_couleur_codificateur = code_couleur_codificateur.copy()
    time.sleep(1)
    commencer.play(0, 1000)

    while continuer2 == True:  # boucle principal algo
        for evenement in pygame.event.get():  # si 1er fenetre 2eme aussi
            if evenement.type == pygame.QUIT or fermer == False:
                continuer2 = False
                fermer = False
                jouer = False
                attendre = False
                continue

        if nombre_essai >= 14 and gagner == False:
            continuer2 = False
            gagner_fin = False
            attendre = True
            pygame.draw.circle(font, code_couleur_codificateur[0], (100, 930), 40)
            pygame.draw.circle(font, code_couleur_codificateur[1], (230, 930), 40)
            pygame.draw.circle(font, code_couleur_codificateur[2], (370, 930), 40)
            pygame.draw.circle(font, code_couleur_codificateur[3], (500, 930), 40)


        if gagner == True:
            continuer2 = False
            gagner_fin = True
            attendre = True
            pygame.draw.circle(font, code_couleur_codificateur[0], (100, 930), 40)
            pygame.draw.circle(font, code_couleur_codificateur[1], (230, 930), 40)
            pygame.draw.circle(font, code_couleur_codificateur[2], (370, 930), 40)
            pygame.draw.circle(font, code_couleur_codificateur[3], (500, 930), 40)

        pygame.display.flip()

        pygame.draw.circle(font, "WHITE", (100, 930), 50, 5)
        pygame.draw.circle(font, "WHITE", (230, 930), 50, 5)
        pygame.draw.circle(font, "WHITE", (370, 930), 50, 5)
        pygame.draw.circle(font, "WHITE", (500, 930), 50, 5)

        fenetre.blit(font, (0, 0))
        # rectangle a droite
        fenetre.blit(bordimage, (460, 0))
        pygame.draw.rect(screen, (241, 196, 15), bord, 5)

        draw_circle("BLUE", position_cercle1, rayon_cercle)
        draw_circle("RED", position_cercle2, rayon_cercle)
        draw_circle("GREEN", position_cercle3, rayon_cercle)
        draw_circle("YELLOW", position_cercle4, rayon_cercle)
        draw_circle("WHITE", position_cercle5, rayon_cercle)
        draw_circle("BLACK", position_cercle6, rayon_cercle)

        bouton_sourieb = pygame.mouse.get_pressed()  # traqué le mouvement de la souris
        a, b = pygame.mouse.get_pos()
        if button.x <= a <= button.x + 70 and button.y <= b <= button.y + 70:
            pygame.draw.rect(screen, (88, 214, 141), button)
            pygame.draw.rect(screen, (34, 153, 84), button, 3)

            if bouton_sourieb[0] and nombre_essai_X4 >= 4:  # nombre_essai_X4 sert faire en sorte de mettre que 4 couleur
                OK.play(0, 2000)
                time.sleep(0.3)
                nombre_essai_X4 = 1

                positionX += 55  # dessiner les couleur bien placé et mal placé et 55 pour descendre d'une ligne
                positionY = 1  # parreil mais en y

                resultat = [0, 0, 0, 0]
                code_couleur_codificateur_sans_double = []
                code_couleur_decodeur_sans_double = []

                x = 0
                for i in range(4):
                    if code_couleur_decodeur[i] == code_couleur_codificateur[i]:
                        resultat[x] = 2
                        x += 1
                    else:
                        code_couleur_decodeur_sans_double.append(code_couleur_decodeur[i])
                        code_couleur_codificateur_sans_double.append(code_couleur_codificateur[i])

                code_couleur_decodeur_sans_double1 = set(code_couleur_decodeur_sans_double)
                code_couleur_decodeur_sans_double2 = list(code_couleur_decodeur_sans_double1)

                code_couleur_codificateur_sans_double1 = set(code_couleur_codificateur_sans_double)
                code_couleur_codificateur_sans_double2 = list(code_couleur_codificateur_sans_double1)

                for k in range(len(code_couleur_codificateur_sans_double2)):
                    for j in range(len(code_couleur_decodeur_sans_double2)):
                        if code_couleur_decodeur_sans_double2[j] == code_couleur_codificateur_sans_double2[k]:
                            resultat[x] = 1
                            x += 1

                code_couleur_decodeur = []
                code_couleur_codificateur = copie_code_couleur_codificateur.copy()
                resultat.sort(reverse=True)

                position = 50
                for z in range(15):
                    if z == nombre_essai:
                        position = 55 * z + 50

                nombre_essai += 1
                A = 0
                for a in range(4):
                    if int(resultat[a]) == 2:
                        pygame.draw.circle(font, "RED", (300 + A, position), 10)
                    if int(resultat[a]) == 1:
                        pygame.draw.circle(font, "WHITE", (300 + A, position), 10)
                    A += 30

                if resultat == [2, 2, 2, 2]:
                    gagner = True
                    pygame.draw.circle(font, "RED", (300, position), 10)
                    pygame.draw.circle(font, "RED", (330, position), 10)
                    pygame.draw.circle(font, "RED", (360, position), 10)
                    pygame.draw.circle(font, "RED", (390, position), 10)
                else:
                    gagner = False

        else:
            pygame.draw.rect(screen, (34, 153, 84), button)
            pygame.draw.rect(screen, (34, 153, 84), button, 3)

        if buttonR.x <= a <= buttonR.x + 70 and buttonR.y <= b <= buttonR.y + 70:
            pygame.draw.rect(screen, (236, 112, 100), buttonR)
            pygame.draw.rect(screen, (200, 70, 55), buttonR, 4)
            if bouton_sourieb[0]:
                NOK.play(0,15000)
                if nombre_essai_X4 == 1:
                    positionY = 1
                    nombre_essai_X4 = 0
                    code_couleur_decodeur = []

                elif nombre_essai_X4 == 2:
                    premiere_couleur = code_couleur_decodeur[0]
                    positionY = 2
                    nombre_essai_X4 = 1
                    code_couleur_decodeur = []
                    code_couleur_decodeur.append(premiere_couleur)

                elif nombre_essai_X4 == 3:
                    premiere_couleur = code_couleur_decodeur[0]
                    desieme_couleur = code_couleur_decodeur[1]
                    positionY = 3
                    nombre_essai_X4 = 2
                    code_couleur_decodeur = []
                    code_couleur_decodeur.append(premiere_couleur)
                    code_couleur_decodeur.append(desieme_couleur)

                elif nombre_essai_X4 >= 4:
                    premiere_couleur = code_couleur_decodeur[0]
                    desieme_couleur = code_couleur_decodeur[1]
                    troisieme_couleur = code_couleur_decodeur[2]
                    positionY = 4
                    nombre_essai_X4 = 3
                    code_couleur_decodeur = []
                    code_couleur_decodeur.append(premiere_couleur)
                    code_couleur_decodeur.append(desieme_couleur)
                    code_couleur_decodeur.append(troisieme_couleur)
                time.sleep(0.3)

        else:
            pygame.draw.rect(screen, (200, 70, 55), buttonR)
            pygame.draw.rect(screen, (200, 70, 55), buttonR, 4)

        if nombre_essai_X4 < 4:
            pygame.draw.circle(screen, (255, 0, 255), (position3, positionX+25), 5)
            pygame.draw.circle(screen, (255, 255, 255), (position3, positionX+25), 5, 1)#point rouge

        # Récupérer la position de la souris
        position_souris = pygame.mouse.get_pos()
        bouton_sourie = pygame.mouse.get_pressed()

        # Calculer la distance entre le centre du cercle et la position de la souris
        distance1 = math.sqrt(
            (position_souris[0] - position_cercle1[0]) ** 2 + (position_souris[1] - position_cercle1[1]) ** 2)
        distance2 = math.sqrt(
            (position_souris[0] - position_cercle2[0]) ** 2 + (position_souris[1] - position_cercle2[1]) ** 2)
        distance3 = math.sqrt(
            (position_souris[0] - position_cercle3[0]) ** 2 + (position_souris[1] - position_cercle3[1]) ** 2)
        distance4 = math.sqrt(
            (position_souris[0] - position_cercle4[0]) ** 2 + (position_souris[1] - position_cercle4[1]) ** 2)
        distance5 = math.sqrt(
            (position_souris[0] - position_cercle5[0]) ** 2 + (position_souris[1] - position_cercle5[1]) ** 2)
        distance6 = math.sqrt(
            (position_souris[0] - position_cercle6[0]) ** 2 + (position_souris[1] - position_cercle6[1]) ** 2)

        # Tester si la distance est inférieure au rayon du cercle
        est_touche1 = distance1 < rayon_cercle
        est_touche2 = distance2 < rayon_cercle
        est_touche3 = distance3 < rayon_cercle
        est_touche4 = distance4 < rayon_cercle
        est_touche5 = distance5 < rayon_cercle
        est_touche6 = distance6 < rayon_cercle

        if positionY == 1:
            position3 = 50
        if positionY == 2:
            position3 = 100
        if positionY == 3:
            position3 = 150
        if positionY == 4:
            position3 = 200

        if nombre_essai_X4 <= 4:
            # Afficher le résultat dans la console
            if est_touche1 and bouton_sourie[0]:
                bouton.play()
                code_couleur_decodeur.append("blue")
                nombre_essai_X4 += 1
                positionY += 1
                pygame.draw.circle(font, "BLUE", (position3, positionX), 18)
                time.sleep(0.2)

            elif est_touche2 and bouton_sourie[0]:
                bouton.play()
                code_couleur_decodeur.append("red")
                nombre_essai_X4 += 1
                positionY += 1
                pygame.draw.circle(font, "RED", (position3, positionX), 18)
                time.sleep(0.2)

            elif est_touche3 and bouton_sourie[0]:
                bouton.play()
                code_couleur_decodeur.append("green")
                nombre_essai_X4 += 1
                positionY += 1
                pygame.draw.circle(font, "GREEN", (position3, positionX), 18)
                time.sleep(0.2)

            elif est_touche4 and bouton_sourie[0]:
                bouton.play()
                code_couleur_decodeur.append("yellow")
                nombre_essai_X4 += 1
                positionY += 1
                pygame.draw.circle(font, "YELLOW", (position3, positionX), 18)
                time.sleep(0.2)

            elif est_touche5 and bouton_sourie[0]:
                bouton.play()
                code_couleur_decodeur.append("white")
                nombre_essai_X4 += 1
                positionY += 1
                pygame.draw.circle(font, "WHITE", (position3, positionX), 18)
                time.sleep(0.2)

            elif est_touche6 and bouton_sourie[0]:
                bouton.play()
                code_couleur_decodeur.append("black")
                nombre_essai_X4 += 1
                positionY += 1
                pygame.draw.circle(font, "BLACK", (position3, positionX), 18)
                time.sleep(0.2)

        fenetre.blit(label_victoire1, (515, 675))
        fenetre.blit(label_victoire2, (508, 775))

        # ligne du tableau
        pygame.draw.rect(screen, (236, 240, 241), ligne)
        pygame.draw.rect(screen, (236, 240, 241), ligne2)

        position = 50
        for i in range(14):
            pygame.draw.circle(screen, (236, 240, 241), (50, position), 18, 3)
            pygame.draw.circle(screen, (236, 240, 241), (100, position), 18, 3)
            pygame.draw.circle(screen, (236, 240, 241), (150, position), 18, 3)
            pygame.draw.circle(screen, (236, 240, 241), (200, position), 18, 3)

            pygame.draw.circle(screen, (236, 240, 241), (300, position), 12, 2)
            pygame.draw.circle(screen, (236, 240, 241), (330, position), 12, 2)
            pygame.draw.circle(screen, (236, 240, 241), (360, position), 12, 2)
            pygame.draw.circle(screen, (236, 240, 241), (390, position), 12, 2)
            position += 55

        pygame.display.flip()
    if attendre == True:
        time.sleep(5)
    pygame.display.quit()

    screeen = pygame.display.set_mode((500, 2600))
    pygame.display.set_caption("Mastermind")
    fenetre = pygame.display.set_mode((1354, 667))

    fondwin = pygame.image.load("E:\projet top secret\win.jpg")
    fondwin = fondwin.convert()
    fondlose = pygame.image.load("E:\projet top secret\lose.jpg")
    fondlose = fondlose.convert()

    icon_32x32 = pygame.image.load("E:\projet top secret\icon.jpg")
    pygame.display.set_icon(icon_32x32)

    button_fin = pygame.Rect(617, 400, 140, 80)

    mapolice3 = pygame.font.SysFont("unicod", 40)  # police de rejouer a la fin
    label_victoire2 = mapolice3.render("Rejouer", True, (255, 255, 255), None)

    song.stop()

    if gagner_fin == True:
        win.play()
    else:
        lose.play()

    continuer3 = True
    while continuer3:
        for evenement in pygame.event.get():  # si on ferme le jeu avec la croix
            if evenement.type == pygame.QUIT or fermer == False:
                continuer3 = False
                jouer = False
                continue

        if gagner_fin == True:
            fenetre.blit(fondwin, (0, 0))
            screeen = fondwin
        else:
            fenetre.blit(fondlose, (0, 0))
            screeen = fondlose

        fenetre.blit(label_victoire2, (635, 425))

        bouton_sourieb = pygame.mouse.get_pressed()
        a, b = pygame.mouse.get_pos()
        if button_fin.x <= a <= button_fin.x + 140 and button_fin.y <= b <= button_fin.y + 80:
            pygame.draw.rect(screeen, (88, 214, 141), button_fin)
            pygame.draw.rect(screeen, (34, 153, 84), button_fin, 5)

            if bouton_sourieb[0]:
                time.sleep(0.5)
                jouer = True
                continuer3 = False
        else:
            pygame.draw.rect(screeen, (34, 153, 84), button_fin)
            pygame.draw.rect(screeen, (34, 153, 84), button_fin, 3)

        pygame.display.flip()
    pygame.display.quit()
