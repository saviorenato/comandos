https://certbot.eff.org/lets-encrypt/ubuntuxenial-apache

#Instalando SSL

$ sudo apt-get update

$ sudo apt-get install software-properties-common

$ sudo add-apt-repository universe

$ sudo add-apt-repository ppa:certbot/certbot

$ sudo apt-get update

$ sudo apt-get install certbot python-certbot-apache 

#Iniciar Processo

$ sudo certbot --apache

$ sudo certbot --apache certonly

$ sudo certbot -a dns-plugin -i apache -d "*.example.com" -d example.com --server https://acme-v02.api.letsencrypt.org/directory

#Automatizando renovação

$ sudo certbot renew --dry-run



#Regerar Chaves

$ rm /etc/apache2/sites-enabled/000-default-le-ssl.conf

$ sudo certbot --apache

$ Alterar domínio redirecionamento do http pra https em /etc/apache2/sites-enabled/000-default.conf
