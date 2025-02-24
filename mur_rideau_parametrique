
;; LISP pour la génération automatique de murs rideaux paramétriques avec vitrages et quantitatif
(defun c:MURRIDEAU ()
  (setq largeur (getreal "\nEntrez la largeur totale du mur rideau (en mm) : ")
        hauteur (getreal "\nEntrez la hauteur totale du mur rideau (en mm) : ")
        module (getreal "\nEntrez la largeur du module de trame (en mm) : ")
        type_profil (getstring "\nEntrez le type de profil (ex : MB45, MB60) : ")
        epaisseur_verre (getreal "\nEntrez l'épaisseur du vitrage (en mm) : "))

  (setq nb_colonnes (fix (/ largeur module))
        espacement (/ largeur nb_colonnes)
        nb_niveaux (fix (/ hauteur module))
        pt_origine (getpoint "\nSélectionnez le point d'origine du mur rideau : ")
        longueur_profil 0
        surface_totale_verre 0)

  ;; Boucle pour générer les montants verticaux
  (setq pt_current pt_origine)
  (repeat (1+ nb_colonnes)
    (command "_line" pt_current (list (car pt_current) (+ (cadr pt_current) hauteur)) "")
    (setq longueur_profil (+ longueur_profil hauteur))
    (setq pt_current (list (+ (car pt_current) espacement) (cadr pt_current))))

  ;; Génération des traverses horizontales
  (setq pt_current pt_origine)
  (repeat (1+ nb_niveaux)
    (command "_line" pt_current (list (+ (car pt_current) largeur) (cadr pt_current)) "")
    (setq longueur_profil (+ longueur_profil largeur))
    (setq pt_current (list (car pt_current) (+ (cadr pt_current) module))))

  ;; Calcul des vitrages
  (setq surface_totale_verre (* nb_colonnes nb_niveaux (* module module 0.000001)))

  ;; Résultat
  (princ (strcat "\nMur rideau de type " type_profil " généré avec "
                 (itoa nb_colonnes) " colonnes et " (itoa nb_niveaux) " traverses."))
  (princ (strcat "\nLongueur totale des profils : " (rtos longueur_profil 2 2) " mm."))
  (princ (strcat "\nSurface totale de vitrage : " (rtos surface_totale_verre 2 2) " m²."))
  (princ)
)

(princ "\nCommande MURRIDEAU chargée. Utilisez-la pour générer un mur rideau paramétrique.")
