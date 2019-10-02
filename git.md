## Comandos Gerais

Clonar um Repositório

    $ git clone 'nome-do-repositório'

Verificar status

    $ git status
    
Adicionar um arquivo ou todos que estão no working directory

    $ git add 'arquivo'
    $ git add .
	
Adicionar arquivos através de um menu interativo

    $ git add -i
	
Remover mudanças de determinado arquivo

    $ git checkout 'nome-do-arquivo'
	
Remover todas as mudanças feitas no working directory

    $ git reset --hard
	
Remover arquivos novos que não estão commitados no repositório

    $ git clean -d -f
	
Retirar um arquivo do repositório

    $ git rm -r --cached 'arquivo'
	
Descobrir qual usuário mecheu em determinada linha

    $ git blame 'nome do arquivo'

## Commits

Efetuar um commit

    $ git commit -m 'mensagem'

Apagar o último commit

    $ git reset HEAD~1 --hard
	
Voltar para determinado commit

    $ git merge 'sha1 do commit'

Desfazer um commit, sem perder as modificações efetuadas:

    $ git reset --soft HEAD~1
	
Reescrever os commits no repositório remoto para refletir o que você fez localmente

    $ git push --force
	
Reescrever o histórico local pelo histórico remoto

    $ git pull --rebase
	
Recuperar commit que foram deletados e recolocalos juntamente ao repositório local

    $ git reflog
    $ git merge 'sha1 do commit'
	
Editar a mensagem do último commit

    $ git commit --amend
	
## Branchs

Fazer checkout para outro branch

    $ git checkout 'nome do branch'

Criar um novo branch e selecionar ele com padrão

    $ git checkout -b 'nome do branch'
	
Criar um novo branch a partir de um determinado commit

    $ git checkout -b 'nome do branch' 'sha1 do commit'
	
Enviar o branch local para o repositório remoto

    $ git push origin 'nome do branch':'nome do branch'

## Stashs

Criando um stash anônimo

    $ git stash

Listando os stashs atuais

    $ git stash list
	
Para voltar ao desenvolvimento após corrigir o bug descrito na situação acima

    $ git stash apply
	
Removendo o stash criado

    $ git stash clear
	
Criando stash com um nome específico

    $ git stash save 'fazendo algo'
	
Outros comandos para stash  

    $ git stash apply stash@[0]
    //volta para o stash desejado
    $ git stash pop
    //tira da lista, aplica e apaga o stash
    $ git stash drop stash{0}
    
Desfazer Commit

    $ git reset --hard 'xxxxx'
    $ git clean -f -d
    $ git push -f
    
    
##Permissões    

	$ git config credential.helper store
	
	$ git config core.filemode false
	
	$ git pull
