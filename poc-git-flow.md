## Git Flow

- Git Flow é recomendado para **projetos que utilizam versionamento semântico (_semantic versioning_) ou que precisam oferecer suporte a várias versões de seu software.**
- Se o projeto exige entrega contínua, como normalmente ocorre em projetos, este modelo não é recomendado para esse tipo de cenário.
- Geralmente com o Git Flow são geradas branches de longa duração e branches de longa duração atrapalham a entrega contínua.

### Como funciona:

> Git Flow trabalha com duas branches principais, Develop e a Master, que duram para sempre; e três branches de suporte, Feature, Release e Hotfix, que são temporários e duram até realizar o merge com as branches principais.

> A branch Master armazena o histórico do lançamento oficial, e a branch Develop serve como uma ramificação de integração para recursos.
---
![GitFlow](https://www.alura.com.br/artigos/assets/git-flow-o-que-e-como-quando-utilizar/imagem3.png)

---

#### Branch Master/Main
Principal branch, aqui é onde temos todo o código de produção. Todas as novas funcionalidades que estão sendo desenvolvidas, em algum momento, serão mescladas ou associadas a Master. As formas de interagir com essa branch são através de uma Hotfix ou de uma nova Release.

#### Branch Develop

É a branch onde fica o código do próximo deploy. Ela serve como uma linha do tempo com os últimos desenvolvimentos, isso significa que ela possui funcionalidades que ainda não foram publicadas e que posteriormente vão ser associadas com a branch Master.

#### Branch Feature

São branches utilizadas para o desenvolvimento de funcionalidades específicas. É recomendável que essas branches sigam uma convenção de nome, a convenção mais utilizada é iniciar o nome das branches com feature, por exemplo, “feature/git-flow-poc”.

#### Branch Hotfix

É uma branch criada a partir da master para realizar correções imediatas encontradas no sistema em produção. Quando concluída, ela é excluída após realizar o merge com as branches Master e Develop.

#### Branch Release

Uma vez que uma etapa de desenvolvimento esteja concluída, teremos em nossa Branch Develop todas as features e Hotfix mesclados. Então, se quisermos ter todas essas novas funcionalidades na Branch Master, teremos que criar uma Branch de Release.

A Branch Release serve como ponte para fazer o merge da Develop para a Master. Ela funciona como ambiente de homologação e é removida após realizar os testes do merge com a Master. Caso seja encontrado algum bug e haja alguma alteração, ela também deve ser sincronizada com a Develop.

Por fim, quando fechamos uma Branch Release, temos que criar uma tag com a nova versão de lançamento do software, para que possamos ter um histórico completo do desenvolvimento.

### Implementação do Git Flow
- Existem duas formas de implementar o Git Flow, a primeira é utilizar os comandos básicos do Git, a outra é utilizar uma CLI que ajuda a simplificar o fluxo do Git Flow.

> Passo a passo:
> 
> **Processo de desenvolvimento**
> $ git checkout develop
> $ git checkout -b feature/novo-componente
> 
> $ git push origin feature/novo-componente
>
>Abre a PR, processo de code review e merge na develop
>
>**Processo de geração de release**
> $ git checkout develop
>$ git checkout -b release/v1.0.1 && git push origin release/v1.0.1
>
>$ git tag v1.0.1
>
>$ git show v1.0.1 && git push origin v1.0.1
> 
> **Processo para produção**
>  
>Abrir uma PR da branch release para master
>   
>   **Processo de hotfix**
>$ git checkout master
>    
>$ git checkout -b name-hotfix
>     
> $ git tag name-hotfix
>
> $ git show name-hotfix && git push origin name-hotfix
> 
>Abrir PR para **master** e para **develop** (Ou podemos abrir apenas na master e fazer um cherry pick do commit para develop)


## Vantagens
- Desenvolvimento paralelo (Isolamos os novos desenvolvimentos do que já está finalizado)
- Colaboração (Trabalho pode ser feito entre duas ou mais pessoas usando a mesma feature branch)
- Área de preparação (Branch de develop é nosso local onde podemos testar sem nos preocupar)
- Correções de emergência (Hotfix vai conter a correção de emergência, não corre risco de mesclar algo que não deveria em produção)

## Desvantagens
- Fluxo e processos complexos (Muitas alterações ocorrendo em diversas branchs ao mesmo tempo pode tornar esse processo todo chato e complicado de fazer)
- Independência de features (Uma branch pode conter alterações que impactam diretamente no desenvolvimento de outras e dependendo do tamanho pode ser uma tarefa difícil fazer o merge)

[Referência](https://nvie.com/posts/a-successful-git-branching-model/) 