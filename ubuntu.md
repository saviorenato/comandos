## UNIX

Copiar

    $ cp -r 'local' 'destino'

Remover Arquivo

    $ rm 'caminho/arquivo'

Remover Pasta 

    $ rm -rf 'caminho/pasta'

Criar Pasta

    $ mkdir 'caminho/nome_da_pasta'

Verificar Dados Arquivo

    $ wc 'arquivo'

Permissões de Pasta 

    $ chmod -R 775 'pasta'  

Permissões de Propriedade

    $chown -R www-data:www-data 'pasta'

Remover Versões Antigas do PHP
    
    $ sudo apt-get purge php5 php5-cli libapache2-mod-php5 php5-mysql phpmyadmin
    $ sudo rm -rf /etc/php5
    
Terminator
    $sudo add-apt-repository ppa:gnome-terminator
    $sudo apt-get update
    $sudo apt-get install terminator
    $sudo apt-get install zsh
    $cd 
    sh -c "$(curl -fsSL https://raw.github.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
    
    $cd
    wget https://github.com/powerline/powerline/raw/develop/font/PowerlineSymbols.otf
    wget https://github.com/powerline/powerline/raw/develop/font/10-powerline-symbols.conf
    mkdir ~/.fonts/
    mv PowerlineSymbols.otf ~/.fonts/
    mkdir -p .config/fontconfig/conf.d
    
    $fc-cache -vf ~/.fonts/
    $mv 10-powerline-symbols.conf ~/.config/fontconfig/conf.d/
    $nano ~/.zshrc
    
    # Change [ZSH_THEME="robbyrussell"] to [ZSH_THEME="agnoster"]
    #ZSH_THEME="agnoster"
    
    $cd ~
    $git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
    
    #Add the plugin to the list of plugins for Oh My Zsh to load (inside ~/.zshrc): plugins=(zsh-autosuggestions)
    $nano ~/.zshrc
    $prompt_context() {}
    
