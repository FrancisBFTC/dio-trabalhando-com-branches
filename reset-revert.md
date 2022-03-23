# Comandos git reset e git revert

### Utilizando git reset orientado a HEAD

git reset HEAD~1 --soft

O comando acima move os arquivos para a Staging Area
Exemplo: O que foi após "git add"

git reset HEAD~1 --mixed

O comando acima move os arquivos para a Working directory
Exemplo: Untracked/Modified files, O que foi feito antes de "git add"

git reset HEAD~1 --hard

O comando acima torna inexistente o commit, deleta os arquivos
Exemplo: Estado anterior de modificação ou criação de um arquivo

### Utilizando git reset orientado a hash

echo > arquivoX.txt
echo > arquivoY.txt
echo > arquivoZ.txt

Acima é criado novos arquivos

git add arquivoX.txt
git commit -m "ArquivoX"

git add arquivoY.txt
git commit -m "ArquivoY"

git add arquivoZ.txt
git commit -m "ArquivoZ"

Acima é commitado cada um dos arquivos com mensagens diferentes

git log --oneline

Verá que a HEAD estará apontando pro último commit, ou seja, pro commit
no qual tem a mensagem "ArquivoZ", se quer mover para staging area via hash
basta copiar a hash do commit anterior, Exemplo:

git reset 2ccb04d --soft

Suponhamos que 2ccb04d é a hash do ArquivoY, então o HEAD vai andar 1 passo pra trás
resetando o último commit, sendo o mesmo que HEAD~1.. se quiser andar 2 passos para trás,
copie a hash do commit antes do ArquivoY, que é o arquivoX, sendo o mesmo que HEAD~2
e assim por diante, suponhamos que temos uma HASH 3ddb05d de um commit anterior do arquivoX,
se usássemos esta HASH, iríamos resetar os commits dos 3 arquivos, o mesmo que HEAD~3, então
vamos usar este exemplo movendo os 3 arquivos para a Working directory via HASH:

git reset 3ddb05d --mixed

O parâmetro --mixed move os arquivos para untracked/modified files, isto é, a working directory.

Se quiser literalmente apagar os 3 arquivos, tornando inexistente o commit, basta:

git reset 3ddb05d --hard

Agora poderá logar o histórico para verificar em qual commit está apontando:

git log --oneline
