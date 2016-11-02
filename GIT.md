### Como usar o git-flow

#### Inicialização

Para inicializar um novo repositório com a estrutura básica do branch, use:

```console
$ git flow init [-d]
```

Este comando interativamente pedirá que você responda algumas perguntas sobre quais branches 
você gostaria de usar como branch de desenvolvimento e produção, e como você gostaria 
que seus prefixos sejam nomeado. Você pode simplesmente pressionar enter em qualquer uma 
dessas perguntas para aceitar as sugestões padrão.

O parametro `-d` fará com que o projeto seja criado com todos os valores padrões.

#### Criando feature/release/hotfix/support branches

Para listar, iniciar e finalizar uma feature branch, use:

```console
$ git flow feature
$ git flow feature start <nome> [<commit-base>]
$ git flow feature finish <nome>
```

Para a feature branchs, o parametro `<commit-base>` serve para informar que a iniciação do branch é apartir de um
determinado commit do branch `develop`.

Para fazer push e/ou pull de uma feature (função/característica) branch do repositório remoto, use:

```console
$ git flow feature publish <nome>
$ git flow feature pull <remote> <nome>
```

Para listar, iniciar e finalizar uma release (lançamento) branch, use:

```console
$ git flow release
$ git flow release start <release> [<commit-base>]
$ git flow release finish <release>
```

Assim como nas feature branchs, o parametro `<commit-base>` serve para informar que a iniciação do branch é apartir de um
determinado commit do branch `develop`.

Para listar, iniciar e finalizar uma hotfix (correção) branches, use:

```console
$ git flow hotfix
$ git flow hotfix start <release> [<commit-base>]
$ git flow hotfix finish <release>
```

Assim como nas realeses branchs, o parametro `<commit-base>` serve para informar que a iniciação do branch é apartir de um
determinado commit do branch `develop`.

Para listar e iniciar uma support (auxílio) branches, use:

```console
$ git flow support
$ git flow support start <release> <base>
```

Assim como nas hotfixs branchs, o parametro `<commit-base>` serve para informar que a iniciação do branch é apartir de um
determinado commit do branch `develop`.

#### Padrões de uso do Git

##### Branches

* Escolha nomes *curtos* e *descritivos*:

  ```shell
  # bom
  $ git flow feature start oauth-migration

  # ruim - muito vago
  $ git flow feature start login_fix
  ```

* Identificadores correspondentes de issues de um servidor git (Ex. Issues do GitHub)
também são bons candidatos para usar em nomes de branches. Por exemplo:

  ```shell
  # GitHub Issue #15
  $ git flow feature start issue-15
  ```

* Use *traços* para separar palavras.

* Quando várias pessoas estão trabalhando na *mesma* funcionalidade, pode ser conveniente
  ter um branch de funcionalidade *pessoal* e um branch de funcionalidade para a *equipe*.
  Use a seguinte convenção de nomenclatura:

  ```shell
  $ git flow feature start oauth-migration/master # Branch da equipe
  $ git flow feature start oauth-migration/maria  # Branch pessoal da Maria
  $ git flow feature start oauth-migration/joao   # Branch pessoal do João
  ```
  
  
[![Flattr this][2]][1]

[1]: http://flattr.com/thing/53771/git-flow
[2]: http://api.flattr.com/button/button-static-50x60.png


### Git sem utilizar o git-flow

- Introduzir novas funcionalidades **(feature)**
- Corrigir comportamento inesperado **(bug)**
- Alterar a forma, mantendo o comportamento **(refactor)**

Feature Branches são tipos de branches para cada tarefa/atividade do trabalho que deve ser criada com um tipo de *Feature Branch*, que irá
conter uma sequência de ações (na forma de Commits) necessárias para que a
finalidade seja atingida. O nome da Branch deve ser prefixado com o tipo de
alteração que será realizada: `feature`, `bug` ou `refactor`.

Por exemplo, suponha que Franklin tenha criado o Branch `feature/faca-alguma-coisa` apartir do `master`. Depois de alguns Commits, a funcionalidade já está pronta
para ser entregue. No entanto, o Branch `master` sofreu alterações desde que
`feature/faca-alguma-coisa` foi criada. Sendo assim, é necessário fazer um Rebase
para aplicar as mudanças da *Feature Branch* criada em cima da nova realidade do
`master`:

```sh
$ git checkout feature/faca-alguma-coisa
$ git rebase master
```

> Nesse passo do `rebase` você pode ter que corrigir alguns conflitos (e certamente irá, kkk), mas não é tão complicado, pode ficar tranquilo, só corrigir os erros de conflitos usando o seu editor de código. Contudo sempre verificando e perguntado sobre alguma parte do código que não tiver certeza do que deve ser inserido ou removido. Neste passo você pode precisar dar o comando `git add grails-app/caminho/para/o/arquivo/com/conflito/corrigido/file.gsp`, `File.groovy` ou `FileController.groovy` e `git rebase --continue` algumas vezes.

Após o Rebase, o Merge pode ser realizado:

```sh
$ git checkout master
$ git merge feature/faca-alguma-coisa
```

Dessa forma, nenhum Commit de Merge é criado. O resultado é um repositório fácil de ler, independente da quantidade de pessoas trabalhando nele:

Fazer o Rebase com frequência torna o processo de resolução de conflitos mais
simples. Para não perdemos dias inteiros resolvendo conflitos de Merge!
Para piorar, o **fardo** de que o Merge ficava a cargo de quem tinha mais
*coragem* (paciência) para fazê-lo. Hoje, esse esforço pode ser diluído: quem
cria a *Feature Branch* tem a responsabilidade de mantê-la atualizada em relação
ao `master`. Assim lidaremos com conflitos muito menores, e quem os resolve é quem tem
mais condições de julgar como esses conflitos devem ser resolvidos.


  Realizar o merge nos branchs pessoais para o branch da equipe (ver ["Merging"](#merging)).
  Eventualmente, o branch da equipe será integrado ao "master".

* Apague seu branch do upstream do repositório depois de integrado (a menos
  que haja uma razão específica para não fazê-lo).

  Dica: Use o seguinte comando quando estiver no "master" para listar os branches
  que foram feitos merge:

  ```shell
  $ git branch --merged | grep -v "\*"
  ```

##### Commits

* Cada commit deve ser uma *mudança lógica* simples. Não faça várias
  *mudanças lógicas* em um commit. Por exemplo, se uma alteração corrige um bug e
  otimiza a performance de uma funcionalidade, descreva no commit de forma sucinta todas alterações feitas.

* Não divida uma *mudança lógica* simples em vários commits. Por exemplo,
  a implementação de uma funcionalidade e os testes correspondentes à ela devem estar no mesmo commit.

* Commit *cedo* e *frequentemente*. Commits pequenos e autônomos são mais fáceis de entender e reverter
  quando algo dá errado.

* Commits devem ser ordenados *logicamente*. Por exemplo, se *commit X* depende
  de uma mudança feita no *commit Y*, então *commit Y* deve vir antes do *commit X*.

###### Descrição dos commits

* Use o editor, não o terminal, quando estiver escrevendo a mensagem do commit:

  ```shell
  # bom
  $ git commit

  # ruim
  $ git commit -m "Correção rápida"
  ```

  Committar do terminal encoraja uma ideia de ter que encaixar tudo em uma
  única linha, o que geralmente resulta em commits não informativos, mensagens ambíguas.

* O sumário (ie. a primeira linha da mensagem) deve ser
  *descritivo* ainda que *sucinto*. O ideal é que não seja maior que *50 caracteres*.
  Deve ser escrito com letra maiúscula e no modo imperativo.
  Não deve terminar com um ponto, uma vez que é efetivamente o título do *title*:

  ```shell
  # bom - modo imperativo, letra maiúscula, menos que 50 caracteres
  Marcar grandes registros como obsoleto quando insinuar falhas

  # ruim
  corrigido ActiveModel::Errors mensagens de depreciado falham quando o AR era usado fora do Rails.
  ```

* Depois disso deve aparecer uma linha em branco seguido de mais descrição.
  Deve possuir *72 caracteres* e explicar *por que*
  a mudança é necessária, *como* está relacionado com a issue e o quais *efeitos colaterais*
  podem ter.

  Também deve fornecer qualquer referência aos recursos relacionados (eg. link para a issue correspondente em um bug tracker):

  ```shell
  Curto (50 chars ou menos) sumário de mudanças

  Texto explanatório mais detalhado, se necessário. Deve possuir
  72 caracteres. Em alguns contextos, a primeira linha
  é tratado como o assunto de um email e o resto
  do texto como o corpo. A linha vazia separando o sumário
  do corpo é crucial (a menos que você omita inteiramente
  o corpo); ferramentas como rebase podem se confudir se você roda os dois juntos.

  Parágrafos adicionais vem depois das linhas vazias.

  - Marcador circulares são permitidos também

  - Use um hífen ou asterisco para o marcador, seguido por um espaço simples, com linhas vazias entre eles

  Fonte - http://tbaggery.com/2008/04/19/a-note-about-git-commit-messages.html
  ```

  Por fim, quando estiver escrevendo uma mensagem do commit, pense sobre o que você precisaria saber olhando para o commit daqui um ano.

* Se um *commit A* depende do *commit B*, a dependência deve ser evidenciada na mensagem
  do *commit A*. Use o hash do commit quando se referir a commits.

  Similarmente, se o *commit A* corrige um bug introduzido pelo *commit B*, deve ser evidenciada na mensagem
  do *commit A*.

* Se um commit sofrerá squash de outro commit use o `--squash` e
  `--fixup` sintaxes respectivamente, a fim tornar sua intenção clara:

  ```shell
  $ git commit --squash f387cab2
  ```

  *(Dica: Use a `--autosquash` marcação quando estiver realizando rebase. Os commits
  terão o squash realizado automaticamente.)*

##### Merging

* **Não reescreva histórico publicado.** O histórico do repositório é valioso a sua maneira e muito importante para permitir dizer *o que realmente aconteceu*. Alterar histórico publicado é uma fonte comum de problemas para qualquer um que trabalhe no projeto.

* Contudo, há casos em que reescrever o histórico é legítimo. Estes são quando:

  * Você é o único trabalhando no branch e não está sendo inspecionado.

  * Você quer arrumar seu branch (eg. commits squash ) e/ou realizar rebase dele para o "master" para
    realizar o merge depois.

  Dito isso, *nunca reescreva o histórico do branch "master"* ou quaisquer
  branchs especiais (ie. usado em produção ou servidores de Integração Contínua).

* Mantenha o histórico *limpo* e *simples*. *Bem antes de realizar o merge* em seu branch:

    1. Tenha certeza que está em conformidade com o guia de estilo e realize qualquer ação necessária
       se não (squash/reordenar seus commits, refazer mensagens etc.)

    2. Rebase em outro branch em que será feito:

       ```shell
       [meu-branch] $ git fetch
       [meu-branch] $ git rebase origin/master
       # então merge
       ```

       Isto resulta em um branch que pode ser diretamente aplicado no final do
       branch "master" e resulta em um histórico bem simples.

       *(Nota: Esta estratégia é mais adequada para projetos com branches
        recentes. Caso contrário é melhor ocasionalmente realizar o merge do
        branch "master" em vez de fazer rebase nele.)*

* Se seu branch inclui mais de um commit, não faça merge como um branch avançado:

  ```shell
  # bom - garante que o commit de merge seja criado
  $ git merge --no-ff meu-branch

  # ruim
  $ git merge meu-branch
  ```

##### Misc.

* Há vários fluxos de trabalho, e cada um tem suas forças e fraquezas.
  Se um fluxo de trabalho se encaixa para o seu caso, depende da equipe, do projeto e do seu
  processo de desenvolvimento.

  Dito isso, é importante escolher um fluxo de trabalho e permanecer com ele.

* *Seja consistente.* Isto é relacionado ao fluxo de trabalho, mas também se expande a coisas como, mensagens dos commits, nomes de branchs, tags. Ter um estilo consistente dentro do repositório torna as coisas mais fáceis para entender o que está acontecendo olhando no log, em uma mensagem do commit etc.

* *Teste antes de realizar o push.* Não suba trabalho não terminado.

* Use [Tags Anotadas](http://git-scm.com/book/en/v2/Git-Basics-Tagging#Annotated-Tags) para
  marcação de releases ou outros pontos importantes no histórico

  Prefira [lightweight tags](http://git-scm.com/book/en/v2/Git-Basics-Tagging#Lightweight-Tags) para uso pessoal, bem como para commit com marcações para referências futuras.

* Mantenha seu repositório em boa forma, realizando ocasionalmente tarefas de manutenção de performance em seu
  repositório local *e* remoto:

  * [`git-gc(1)`](http://git-scm.com/docs/git-gc)
  * [`git-prune(1)`](http://git-scm.com/docs/git-prune)
  * [`git-fsck(1)`](http://git-scm.com/docs/git-fsck)
