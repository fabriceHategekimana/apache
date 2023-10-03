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

```
DocumentRoot /var/www/html
```

Puis modifier le fichier `index.html` correspondant:

```
nano /var/www/html/index.html
```

