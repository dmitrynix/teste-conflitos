# Criar um ``branch`` para a mudança

    [master] % git branch conflito
    [master] % git checkout conflito
    [conflito] %

# Fazer as mudanças e "commitar"

    [conflito] % git add conflito.txt
    [conflito] % git commit -m 'Modificando o arquivo de conflito'

# Fazendo "merge"

Antes de fazer um merge/rebase é necessário certificar-se de que tem as
últimas modificações do branch **master**:

    [conflito] % git checkout master
    [master] % git pull

Agora tem que voltar ao branch **conflito** para pegar as últimas mudanças
do **master**:

    [master] % git checkout conflito
    [conflito] % git rebase master
    First, rewinding head to replay your work on top of it...
    Applying: Modificando a primeira linha do arquivo conflito
    Using index info to reconstruct a base tree...
    Falling back to patching base and 3-way merge...
    Auto-merging conflito.txt
    CONFLICT (content): Merge conflict in conflito.txt
    Failed to merge in the changes.
    Patch failed at 0001 Modificando a primeira linha do arquivo conflito

    When you have resolved this problem run "git rebase --continue".
    If you would prefer to skip this patch, instead run "git rebase --skip".
    To restore the original branch and stop rebasing run "git rebase
    --abort".

    [no-branch*] %

A mensagem acima explica o que é necessário fazer para aplicar resolver
este problema.

# Resolvendo o conflito

Depois de feito as devidas modificações no arquivo conflito.txt, apenas
precisa adicionar o arquivo e "continuar".

    [no-branch*] % git add conflito.txt
    [no-branch*] % git rebase --continue
    Applying: Modificando a primeira linha do arquivo conflito
    [conflito] %

# Enviar para o master

Agora só é necessário enviar o que foi feito para o branch **master**:

    [conflito] % git checkout master
    Switched to branch 'master'
    [master] % git merge conflito
    Updating ced568e..3078314
    Fast-forward
     conflito.txt |    2 +-
     1 files changed, 1 insertions(+), 1 deletions(-)
    [master^1] % git push
    Counting objects: 5, done.
    Delta compression using up to 4 threads.
    Compressing objects: 100% (3/3), done.
    Writing objects: 100% (3/3), 370 bytes, done.
    Total 3 (delta 0), reused 0 (delta 0)
    To git@github.com:dmitrynix/teste-conflitos.git
       ced568e..3078314  master -> master

Opcionalmente pode-se apagar o branch **conflito**:

    [master] % git branch -d conflito
