# PROJECT_STATUS.md — Plateforme d'invitations (nom de travail : Entrelacs)

## Architecture retenue (budget limité)
- **Front** : Next.js (React) + Tailwind, hébergé sur Vercel (gratuit au départ).
- **Base de données + comptes + stockage** : Supabase (offre gratuite).
- **Paiement** : Stripe Checkout (cartes). Option locale à étudier : CMI / Payzone (Maroc).
- **PDF imprimable** : génération côté serveur (Puppeteer / @react-pdf), format 13×18 cm + fond perdu.
- **Invitation animée** : une page `/i/[slug]` par invitation ; lien individuel `/i/[slug]?g=[id_invité]`.
- **E-mails automatiques** : Resend. **QR code** : librairie `qrcode`. **Carte** : lien/embed Google Maps.

## Fichiers créés
| Fichier | Contenu |
|---|---|
| `index.html` | Page d'accueil + éditeur (maquette visuelle autonome, route `#editeur`) |
| `PROJECT_STATUS.md` | Ce document |

## Terminé (étape 1)
- Identité visuelle : prune profond, laiton, rose pâle ; Cormorant Garamond + Jost + Pinyon Script.
- Page d'accueil : hero avec carte interactive (prénoms en direct), 6 modèles, 2 types d'invitation, 3 formules.
- Éditeur : choix du modèle, textes, date/heure/lieu, police, fond, accent, aperçu en direct, bascule Imprimer/Animée.

## Pas encore fait
- Étape 2 : plus de modèles, décorations, export PDF réel.
- Étape 3 : formules + paiement Stripe + livraison automatique.
- Étape 4 : page animée publique, musique, lien partageable.
- Étape 5 : RSVP, tableau de bord, liens individuels, QR code, compte à rebours, Maps, galerie.
- Comptes clients, sauvegarde des brouillons (Supabase).

## Prochaine étape proposée
Étape 2 : export PDF haute qualité depuis l'éditeur + 4 modèles supplémentaires.

---
## Mise à jour : version "site-invitations.html" (remplace la maquette de l'étape 1)
**Décisions** : cliente étudiante sans statut pro ; paiement par carte souhaité (prestataire marocain à confirmer : YouCan Pay / CMI / Payzone, conditions pour particulier NON vérifiées) ; prix en MAD (19 / 39 / 69 DH).

**Fonctionne réellement (côté navigateur, sans serveur)** : 8 modèles inspirés de l'image fournie ; édition en direct (titre, phrase, noms, date, heure, lieu, ville, phrase finale, police, couleur) ; français et arabe avec affichage RTL ; PDF A5 via Imprimer > Enregistrer au format PDF.

**PAS encore fait (nécessite serveur + base de données)** : comptes clients, enregistrement des invitations, lien unique partageable, page animée avec musique, RSVP, liens individuels, tableau de bord, QR code, compte à rebours, Google Maps, photos, paiement, espace administrateur.

**Prochaine étape** : GitHub + Supabase + Next.js (comptes, sauvegarde des invitations, page publique /i/slug), puis paiement quand le prestataire est confirmé.

---
## Mise à jour : exemples par pack
- `premium.html` = exemple du pack Premium (39 DH). `prestige.html` = exemple du pack Prestige (69 DH). Starter : exemple à créer.
- Le site `index.html` relie chaque pack à son exemple. Tout fonctionne côté navigateur ; RSVP automatique, tableau de bord en ligne, paiement et comptes restent à construire (serveur).
- Prestige : liens du type `prestige.html#CODE` (5 invités d'exemple). Pour ajouter des invités ou renseigner le numéro WhatsApp, modifier `CFG` dans le fichier.

## Mise à jour : création Prestige
- `creer-prestige.html` : formulaire (prénoms, date, lieu, invités, photos, WhatsApp) qui génère un fichier d'invitation complet avec codes et liens par invité.
- `prestige.html` est maintenant piloté par un bloc CFG (noms, date, lieu, invités, photos).
- NON fait : accès réservé aux clients payants (comptes + paiement), publication automatique du lien, réponses RSVP automatiques.

## Mise à jour : parcours aperçu puis paiement
- creer-prestige.html : aperçu avec filigrane « NON PAYÉ » ; SHOP.mode 'test' (téléchargement gratuit) ou 'live' (bloqué, bouton de paiement si SHOP.payUrl renseigné).
- Un verrou côté navigateur peut être contourné ; la vraie protection exige un serveur qui génère le fichier propre après confirmation du paiement.
