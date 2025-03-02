---
nav_title: Relais privé d’Apple
article_title: Envoi d’e-mails au relais privé d’Apple
alias: /email_relay/
page_order: 9
description: "Le présent article explique le processus d’envoi d’e-mails au relais privé d’Apple."
channel:
  - e-mail
  
---

# Envoi d’e-mails au relais privé d’Apple

Avec la version iOS 13, Apple a introduit des fonctionnalités pour les clients Apple, ce qui a un impact sur la manière dont les e-mails leur sont envoyés. La fonctionnalité Authentification unique (SSO) d’Apple permet à leurs utilisateurs de partager leur adresse e-mail (`exemple@icloud.com`) ou pour de la dissimuler en masquant ce qui est transmis aux marques (`tq1234snin@privaterelay.appleid.com`) par opposition à leur adresse électronique personnelle.

Ces utilisateurs peuvent gérer les applications qui utilisent la connexion avec Apple à partir de leur page de paramètres Apple ID (voir [Documentation d’Apple](https://support.apple.com/en-us/HT210426)). Si un utilisateur décide de désactiver le transfert par e-mail vers l’e-mail de relais de votre application, Braze recevra des informations de rebond d’e-mail comme d’habitude. Afin d’envoyer des e-mails au relais privé d’Apple, vous devez enregistrer vos domaines d’envoi auprès d’Apple.

## Envoyer des e-mails pour SendGrid

Si vous utilisez SendGrid en tant que fournisseur de messagerie électronique, vous pouvez envoyer des e-mails à Apple sans avoir à effectuer des modifications au niveau du DNS. Accédez à la page de votre [Certificat Apple](https://help.apple.com/developer-account/?lang=en#/devf822fb8fc) et autorisez l’adresse e-mail que vous souhaitez utiliser pour envoyer depuis le service de relais d’e-mail d’Apple (votre adresse d’expédition).  

![Option permettant d’autoriser des adresses e-mail individuelles sur la page du certificat Apple.]({% image_buster /assets/img/email-relay-whitelabel-address.png %})

Pour trouver l’adresse, allez dans votre dossier DNS Sendgrid et copiez l’**UID**, le **Whitelabel Subdomain (Sous-domaine de Whitelabel)**, et le **Domaine** de la colonne **Host Value (Valeur hôte)**. 

![Colonne Valeur HÔTE dans la section des enregistrements DNS Sendgrid.]({% image_buster /assets/img/email-relay-dns-records.png %})

L’adresse doit être formatée comme suit : `bounces+<YOUR_UID>@<YOUR_WHITELABELED_SUBDOMAIN_AND_DOMAIN>`(par ex., `bounces+1234567@braze.online.docs.com`). Une fois ajoutés à votre page de certificat Apple, les e-mails provenant de ce domaine seront livrés depuis le système de relais privé d’Apple.

{% alert important %}
Si l’adresse d’« expédition » souhaitée est une adresse `abmail`, incluez-la dans votre sous-domaine. Par exemple, utilisez `abmail.docs.braze.com` au lieu de `docs.braze.com`. Ce n’est peut-être pas le cas de votre adresse. Vérifiez vos enregistrements DNS dans Sendgrid. 
{% endalert %}

### À partir des valeurs d’adresse

Reportez-vous à ce tableau pour les composants utilisés lors de l’ajout d’adresses e-mail avec le relais privé Apple.

| Valeur | Description |
|---|---|
| UID | Cette valeur est fournie par Sendgrid dans vos enregistrements DNS. N’incluez pas la lettre « u » dans votre UID dans l’adresse e-mail. Par exemple, si votre UID est présenté dans Sendgrid comme `u1234567.wl134.sendgrid.net`, alors `1234567` est la valeur UID. <br><br> Si vous n’avez pas accès à vos dossiers DNS, contactez votre gestionnaire du succès des clients Braze pour fournir votre UID. |
| Sous-domaine et domaine marqué comme Whitelabel | Le domaine et sous-domaine initiaux que vous avez saisis dans Sendgrid. Vous pouvez également utiliser la **HOST Value (Valeur HÔTE)** dans vos enregistrements DNS dans Sendgrid. |
{: .reset-td-br-1 .reset-td-br-2}

## Envoi d’e-mails pour Sparkpost

Pour configurer le relais privé Apple pour Sparkpost, procédez comme suit : 

1. Créez les fichiers de vérification nécessaires conformément à la documentation d’Apple, [Se connecter avec Apple](https://developer.apple.com/sign-in-with-apple/get-started/).
2. Hébergez les fichiers dans le répertoire `/.well-known/` des domaines donnés. Assurez-vous que votre réseau de diffusion de contenu (CDN) est accessible au public via Internet.
3. Ajoutez un enregistrement A dans le DNS qui pointe vers le domaine où votre fichier de vérification est hébergé. Il s’agit d’un processus de vérification unique.
4. Sélectionnez Verify on Apple's end (Vérifier sur Apple).

{% alert important %}
Assurez-vous de terminer ce processus dans les 2 à 3 jours qui suivent la création des fichiers de vérification, sinon ils disparaîtront. Apple ne divulgue pas leur durée de validité.
{% endalert %}

Si vous avez d’autres questions, ouvrez un [ticket d’assistance]({{site.baseurl}}/braze_support/).
