## Server Hardening with Apache 2

#### Mettre à jour le système linux (debian based)

```bash
sudo apt update
sudo apt upgrade
```

#### Il faut installer apache2 sur la machine:

```bash
sudo apt-get install apache2
```

#### Démarage du service httpd

```bash
sudo service apache2 start
```

#### Ouvrir la page d'accueil

```bash
firefox http://localhost:80
```

#### Configuration:

Les configurations d'appache se font à des endroits différents.

Vous pouvez créer un site dans `/etc/apache2/sites-available/`

Vous pouvez visiter le fichier de configuration:

```bash
nano /etc/apache2/sites-available/000-default.conf
```

La configuration se fait à l'aide de **directives**:


| directive    | description                            | exemple                      |
|--------------|----------------------------------------|------------------------------|
| ServerAdmin  | Le mail à contacter en cas de problème | nom@gmail.com                |
| DocumentRoot | L'emplacement du site web              | /var/www/html                |
| ErrorLog     | L'emplacement des logs d'erreur        | ${APACHE_LOG_DIR}/error.log  |
| CustomLog    | L'emplacement des logs personnels      | ${APACHE_LOG_DIR}/access.log |


#### Défis: changer la page d'accueil dans apache

##### Question:
Modifier la page d'accueil du site par une page html de votre choix.
Vous pouvez la télécharger ou la générer avec chatGPT.
Pour ce faire vous devez trouver le fichier index.html de l'hôte virtuel déployé par Apache2.


##### Réponse:

Ouvrir simplement le fichier de configuration de l'hôte virtuel par défaut:

```bash
nano /etc/apache2/sites-available/000-default.conf
```

Trouver l'emplacement du fichier avec la directive `DocumentRoot`:

```bash
DocumentRoot /var/www/html
```

Puis modifier le fichier `index.html` correspondant:

```bash
nano /var/www/html/index.html
```

### Limiter le nombre de requêtes par seconde

#### Défi:
Écrire un script (python/bash) qui fait 20 requêtes par secondes sur le site que nous avons fait (localhost).
Vous pouvez déjouer ce script en limitant le nombre de requêtes par seconde à l'aide du module mod_qos.

#### Installer le module QoS

```bash
sudo a2enmod qos
```

#### Relancer le service Apache

```bash
service apache2 restart
```

#### Ajouter la directive dans le fichier de configuration du site

```
<IfModule mod_qos.c>
    # Limitez le nombre de requêtes par seconde à 10
    QS_LocRequestLimitMatch ^/ 10
</IfModule>
```

#### Redémarrer apache

```
service apache2 restart.
```

#### Limiter par le nombre de champ d'une requête 

Vous pouvez inspecter le nombre de champs d'une requête avec wireshark ou firefox.

Pour trouver le nombre de champs sur wireshark, il nous faut lire l'interface loopback et filter les requêtes http puis suivre le flux http pour voir la conversation faite sur la machine.

```
LimitRequestFields 50
```
