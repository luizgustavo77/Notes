# GIT
***COMIT VERSAO***  
``` shell
git tag - mostra versoes do projeto
git checkout -b NOME - cria branch
git checkout NOME - troca branch
git diff NOME NOME - busca mudancas nas branchs
git init - torna a pasta um repositorio do git
git is-files - mostra arquivos controlados pelo git
git status - mostra status do repositorio atual
git add NOME - da controle ao git
git commit -m "COMENTARIO" - grava alteracoes no repositorio
``` 
***PULL, PUSH, BRANCH, CHECKOUT***  
``` shell
git log - historico de commits
git whatchanged -d - detalha alteracao de commit
git remote - mostra repositorios remotos
git remote add NOME https://... - adiciona repositorio remoto que e uma copia
git push origin NOME - envia alteracoes o NOME costuma ser master
git pull origin NOME - puxa alteracoes para seu repositorio
gir branch -d - deleta branch local
git branch -r - mostra branchs remotas
``` 
***REBASE, STASH***
``` bash
git rebase --skip - joga fora oque vc fez
git checkout - sozinho volta ao estado anterior
git reset NOMEDOCOMIT - retira mais tem q ser o ultimo
git revert NOMDECOMIT - volta ao estado anterior um commit antigo
git stash - pausa ultima modificacao
git stash-list - mostra stashs
git stash apply NUMERODOSTASH - volta o stash para frente para usar
git stash drp NUMERODOSTASH - apaga stash
git merge NOMEDOBRANCH - junta oque foi feito nessa branch com a atual
git remote add NOME https://doclone - para adicionar repositorio
```
