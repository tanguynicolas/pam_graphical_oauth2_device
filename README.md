# PAM module for OAuth 2.0 Device Authorization Grant

*Forked from [ICS-MU/pam_oauth2_device](https://github.com/ICS-MU/pam_oauth2_device)*

PAM module for user graphical authentication using
[OAuth 2.0 Device Authorization Grant](https://tools.ietf.org/html/rfc8628).

The following instructions have been tested on Debian 11.

## Make binary (.so)

Install build dependencies.

```bash
sudo apt install libldap2-dev libpam0g-dev libcurl4-openssl-dev make build-essential
```

Clone the repository, build and install the module.

```bash
git clone https://github.com/tanguynicolas/pam_graphical_oauth2_device
cd pam_graphical_oauth2_device
make
```

## Modifications apportées par ce fork

Ce fork permet d'utiliser ce module pour l'authentification par QRcode en mode graphique ; alors qu'il est conçu pour SSH à l'origine.

Les principales choses qui changent sont détaillés ci-après.

### Polling

Le polling est l'action de la workstation qui demande au serveur Keycloak si l'utilisateur s'est bien authentifié ou non.

Dans la version de base, il faut appuyer sur ENTRER pour effectuer un polling. Nous avons modifié ce comportement pour effectuer un polling automatique toutes nes N secondes. Cela est plus simple pour une authentification en mode graphique, cela évite de devoir appuyer sur une touche supplémentaire une fois le consentement donné par l'utilisateur.

### QRcode

Avec le module de base, le QRcode est formé par des caractères spéciaux noirs ou blanc dans une string. Cette string, une fois affiché dans la console prend la forme d'un QRcode. Cela est impossible en mode graphique. Nous avons donc fait en sorte que le QRcode soit généré au format d'un image (.png). Aussi nous avons désactivé tous les printf que le module de base fait dans la console, car inutilisable en mode graphique.
