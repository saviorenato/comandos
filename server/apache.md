## Comandos Gerais
https://www.digitalocean.com/community/tutorials/como-configurar-apache-virtual-hosts-no-ubuntu-16-04-pt

Passo um - Criar a estrutura de diretórios
O primeiro passo que vamos tomar é criar uma estrutura de diretórios que irá armazenar os dados do site que estará servindo aos visitantes.

Nosso document root (o diretório de nível superior que o Apache olha para encontrar o conteúdo para servir) será definido para diretórios individuais sob o diretório /var/www. Vamos criar um diretório aqui para ambos os virtual hosts que estamos planejando fazer.

Dentro de cada um desses diretórios, vamos criar o diretório public_html que irá manter nossos arquivos reais. Isto nos dá certa flexibilidade em nossa hospedagem.

Por exemplo, para nossos sites, nós vamos criar nossos diretórios assim:

sudo mkdir -p /var/www/example.com/public_html
sudo mkdir -p /var/www/test.com/public_html
As partes em vermelho representam os nomes de domínio que estamos querendo servir através de nosso VPS.

Passo Dois - Conceder Permissões
Agora temos a estrutura de diretórios para nossos arquivos, mas eles são de propriedade de nosso usuário root. Se quisermos que nosso usuário regular esteja apto a modificar arquivos em nossos diretórios web, podemos alterar o proprietário fazendo isto:

sudo chown -R $USER:$USER /var/www/example.com/public_html
sudo chown -R $USER:$USER /var/www/test.com/public_html
A variável $USER terá o valor do usuário com o qual você está logado atualmente quando você pressionou ENTER. Fazendo isto, nosso usuário regular agora detém os sub-diretórios public_html onde estaremos armazenando nosso conteúdo.

Devemos também modificar um pouco nossas permissões para garantir que o acesso de leitura é permitido para o diretório web geral e todos os arquivos e pastas que ele contém de modo que a páginas possam ser servidas corretamente:

sudo chmod -R 755 /var/www
Seu servidor web agora deve ter as permissões que ele precisa para servir o conteúdo, e seu usuário deve ser capaz de criar conteúdo dentro das pastas necessárias.

Passo Três - Criar as Páginas Demo para cada Virtual Host
Temos nossa estrutura de diretório no lugar. Vamos criar algum conteúdo para servir.

Vamos fazer apenas uma demonstração, assim nossas páginas serão bastante simples. Vamos apenas fazer uma página index.html para cada site.

Vamos começar com example.com. Podemos abrir um arquivo index.html em nosso editor digitando:

nano /var/www/example.com/public_html/index.html
Nesse arquivo, crie um documento HTML simples que indica o site que está conectado. Meu arquivo se parece com isso:

/var/www/example.com/public_html/index.html
<html>
  <head>
    <title>Welcome to Example.com!</title>
  </head>
  <body>
    <h1>Success!  The example.com virtual host is working!</h1>
  </body>
</html>
Salve e feche o arquivo quando terminar.

Podemos copiar este arquivo para usá-lo como base para nosso segundo site digitando:

cp /var/www/example.com/public_html/index.html /var/www/test.com/public_html/index.html
Podemos, então, abrir o arquivo e modificar as informações pertinentes:

nano /var/www/test.com/public_html/index.html
/var/www/test.com/public_html/index.html
<html>
  <head>
    <title>Welcome to Test.com!</title>
  </head>
  <body> <h1>Success!  The test.com virtual host is working!</h1>
  </body>
</html>
Salve e feche o arquivo também. Agora você tem as páginas necessárias para testar a configuração de virtual host.

Passo Quatro - Criar novos arquivos de Virtual Hosts
Arquivos de virtual host são arquivos que especificam a configuração real do nosso virtual host e determina como o servidor web Apache irá responder às várias requisições de domínio.

O Apache vem com um arquivo padrão de virtual host chamado 000-default.conf que podemos usar como ponto de partida. Vamos copiá-lo para criar um arquivo de virtual host para cada um de nossos domínios.

Vamos começar com um domínio, configurá-lo, copiá-lo para nosso segundo domínio, e então fazer os pequenos ajustes necessários. A configuração padrão do Ubuntu requer que cada arquivo de virtual host termine em .conf.

Crie o primeiro arquivo de Virtual Host
Comece copiando o arquivo para o primeiro domínio:

sudo cp /etc/apache2/sites-available/000-default.conf /etc/apache2/sites-available/example.com.conf
Abra o novo arquivo em seu editor com privilégios de root:

sudo nano /etc/apache2/sites-available/example.com.conf
O arquivo será algo parecido com isso (eu removi os comentários aqui para tornar o arquivo mais legível):

/etc/apache2/sites-available/example.com.conf
<VirtualHost *:80>
    ServerAdmin webmaster@localhost
    DocumentRoot /var/www/html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
Como você pode ver, não há muito aqui. Vamos personalizar os itens aqui para nosso primeiro domínio e adicionar algumas diretivas adicionais. Esta seção de virtual host corresponde a quaisquer requisições que são feitas na porta 80, a porta padrão HTTP.

Em primeiro lugar, precisamos alterar a diretiva ServerAdmin para um e-mail que o administrador do site possa receber e-mails por ele.

ServerAdmin admin@example.com
Depois disso, precisamos adicionar duas diretivas. A primeira, chamada ServerName, estabelece o domínio de base que deve corresponder à esta definição de virtual host. Este provavelmente será o seu domínio. A segunda, chamada ServerAlias, define outros nomes que devem corresponder como se fossem o nome de base. Isto é útil para a correspondência dos hosts que você definiu, como www:

ServerName example.com
ServerAlias www.example.com
A outra única coisa que precisamos mudar para o arquivo de virtual host básico é a localização do documento raiz para este domínio. Nós já criamos o diretório que precisamos, então precisamos apenas alterar a diretiva DocumentRoot para refletir o diretório que criamos:

DocumentRoot /var/www/example.com/public_html
No total, nosso arquivo de virtualhost deve ficar assim:

/etc/apache2/sites-available/example.com.conf
<VirtualHost *:80>
    ServerAdmin admin@example.com
    ServerName example.com
    ServerAlias www.example.com
    DocumentRoot /var/www/example.com/public_html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
Salve e feche o arquivo.

Copie o primeiro Virtual Host e personalize-o para o Segundo Domínio
Agora que temos nosso primeiro arquivo de virtual host criado, podemos criar nosso segundo copiando esse arquivo e ajustando-o conforme necessário.

Comece copiando-o:

sudo cp /etc/apache2/sites-available/example.com.conf /etc/apache2/sites-available/test.com.conf
Abra o novo arquivo com privilégios de root em seu editor:

sudo nano /etc/apache2/sites-available/test.com.conf
Agora você precisa modificar todas as informações pertinentes para referenciar seu segundo domínio. Quando terminar, ele será algo parecido com isto:

/etc/apache2/sites-available/test.com.conf
<VirtualHost *:80>
    ServerAdmin admin@test.com
    ServerName test.com
    ServerAlias www.test.com
    DocumentRoot /var/www/test.com/public_html
    ErrorLog ${APACHE_LOG_DIR}/error.log
    CustomLog ${APACHE_LOG_DIR}/access.log combined
</VirtualHost>
Salve e feche o arquivo quando terminar.

Passo Cinco - Ativar os novos arquivos de Virtual Host
Agora que criamos nossos arquivos de virtual host, devemos ativá-los. O Apache inclui algumas ferramentas que nos permitem fazer isto.

Podemos utilizar a ferramenta a2ensite para ativar cada um de nossos sites assim:

sudo a2ensite example.com.conf
sudo a2ensite test.com.conf
Depois, desabilite o site padrão definido em 000-default.conf:

sudo a2dissite 000-default.conf
Quando terminar, você precisará reiniciar o Apache para fazer com que estas alterações tenham efeito:

sudo systemctl restart apache2
Em outras documentações, você também poderá ver um exemplo usando o comando service:

sudo service apache2 restart
Esse comando ainda funcionará, mas pode não dar a saída que você está acostumado a ver em outros sistemas, uma vez que agora ele é vinculado ao comando systemctl do systemd.

Passo Seis - Configurar o arquivo de hosts local (Opcional)
Se você não está utilizando os nomes de domínio reais que você possui para testar este procedimento e, em vez disso, está usando alguns domínios de exemplo, você pode testar ao menos a funcionalidade desse processo modificando temporariamente o arquivo hosts em seu computador local.

Isto irá interceptar quaisquer requisições para os domínios que você configurou e os apontará para o seu servidor VPS, da mesma forma que o DNS faria se você estivesse utilizando domínios registrados. Isto irá funcionar somente em seu computador, e é útil simplesmente para propósitos de testes.

Certifique-se de que você está operando em seu computador local para estas etapas e não no seu servidor VPS. Você precisará saber a senha administrativa do computador ou então, ser membro do grupo administrativo.

Se você está em um computador Mac ou Linux, edite seu arquivo local com privilégios administrativos digitando:

sudo nano /etc/hosts
Se você estiver em uma máquina Windows, você poderá encontrar instruções para alteração do seu arquivo hosts aqui.

Os detalhes que você precisa adicionar são o endereço IP público do seu servidor VPS seguido pelo domínio que você quer usar para alcançar esse VPS.

Para os domínios que eu utilizei neste guia, assumindo que o endereço IP do meu servidor VPS é 111.111.111.111, eu poderia adicionar as seguintes linhas no final do meu arquivo hosts:

/etc/hosts
127.0.0.1   localhost
127.0.1.1   guest-desktop
111.111.111.111 example.com
111.111.111.111 test.com
Isso irá direcionar quaisquer requisições para example.com e test.com em nosso computador e enviá-las para nosso servidor em 111.111.111.111. Isso é o que queremos se não somos na verdade os proprietários desses domínios, de forma a testar nossos virtual hosts.

Salve e feche o arquivo.

Passo Sete - Teste seus resultados
Agora que você tem seus virtual hosts configurados, você pode testar sua configuração facilmente indo para os domínios que você configurou em seu navegador web:

http://example.com
Você deve ver uma página parecida com esta:



Da mesma forma, você puder visitar sua segunda página:

http://test.com
Você verá o arquivo que você criou para seu segundo site: