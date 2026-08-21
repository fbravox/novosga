# Diretrizes do projeto fork23

## Identidade do projeto

Este repositório é o fork público `fbravox/novosga`, denominado neste fluxo
como **fork23**. A branch default atual é `v2.3`, que representa a linha-base
do projeto.

O fork23 é a fonte canônica de código, branches, commits, pull requests,
issues, decisões e releases deste projeto. O upstream `novosga/novosga` deve
ser consultado somente para comparação técnica, referência histórica ou quando
isso for solicitado explicitamente.

Os bundles forkados, quando usados pelo `composer.json`, também devem ser
tratados como dependências controladas do fork23. Alterações em contratos,
interfaces ou configurações compartilhadas devem considerar a compatibilidade
entre a aplicação e os bundles correspondentes.

## Arquivos de fluxo e procedimentos

Este `AGENTS.md` é o arquivo principal de regras, fluxos e procedimentos do
projeto. Ele deve permanecer sincronizado entre a branch default `v2.3`, a
branch de integração `dev` e as branches de customização ativas.

Cada branch de customização pode possuir, na raiz, um arquivo secundário no
formato `AGENTS-NOME_DA_BRANCH`, por exemplo `AGENTS-TTS`. Esse arquivo registra
somente regras, decisões, escopo, validações e procedimentos específicos da
branch onde está inserido.

As regras podem ser refinadas dinamicamente durante o projeto. Quando uma regra
global for criada ou alterada, atualizar o `AGENTS.md` e sincronizar o arquivo
nas branches ativas por commit próprio ou pelo mecanismo de integração adotado
para a branch. O arquivo secundário não deve substituir nem duplicar
desnecessariamente as regras globais.

Os arquivos de fluxo fazem parte do contexto do projeto e devem ser lidos
antes de iniciar uma tarefa relevante. Não importar automaticamente arquivos
de fluxo, identidade, infraestrutura, bancos, portas ou releases de outro
projeto; importar apenas regras genéricas que tenham sido deliberadamente
adaptadas ao fork23.

## Branches

- `v2.3`: branch default e linha-base pública do fork23;
- `dev`: branch de integração do desenvolvimento;
- branches de customização: branches próprias para funcionalidades isoladas;
- `TTS`: branch da customização de painel e TTS relacionada à issue migrada
  correspondente à antiga issue #101.

Antes de alterar código, confirmar a branch atual e o estado do worktree.
Não misturar alterações de branches, pacotes ou funcionalidades diferentes.
Alterações de uma branch de customização devem ser integradas somente após
validação, revisão e aprovação do escopo correspondente.

## Issues, decisões e publicação

Antes de implementar uma issue:

1. consultar o texto principal e todos os comentários;
2. confirmar o escopo, dependências, critérios e decisões posteriores;
3. registrar a abordagem proposta quando houver risco ou ambiguidade;
4. alterar somente o escopo aprovado;
5. validar a implementação antes de considerar a issue concluída.

Quando uma issue for migrada entre repositórios, a nova issue deve preservar o
contexto essencial, indicar a origem, registrar a branch de implementação e
manter um link de referência entre as duas. A issue original só deve ser
fechada depois que a nova referência estiver publicada e validada.

Todo texto humano publicado no GitHub deve estar em português do Brasil,
incluindo títulos, descrições, comentários, commits, pull requests, releases e
notas. Identificadores técnicos, nomes de classes, métodos, comandos, branches
e arquivos permanecem em sua forma original quando necessário.

Antes de commit ou push:

- conferir `git status` e a branch atual;
- separar arquivos de outros trabalhos;
- adicionar somente os caminhos pertencentes ao escopo aprovado;
- revisar o diff e a mensagem em português;
- confirmar o destino do push.

## Fluxo Git e coordenação de trabalho

O GitHub é o registro público do projeto. Issues, comentários, commits, pull
requests, decisões de integração e releases devem permanecer rastreáveis no
repositório correto. Anotações locais podem apoiar o trabalho, mas não
substituem a issue nem devem ser tratadas como decisão publicada sem registro
no GitHub.

Antes de iniciar um ciclo de trabalho:

1. ler o `AGENTS.md` e o arquivo `AGENTS-NOME_DA_BRANCH`, quando existir;
2. confirmar branch, remotes, estado do worktree e identidade do repositório;
3. ler a issue completa e seus comentários, verificando dependências,
   duplicidades e decisões posteriores;
4. registrar na issue a abordagem, os riscos e as mudanças de escopo quando
   isso for necessário para a continuidade do trabalho.

Uma issue deve representar uma unidade de trabalho identificável. Agrupar
issues em um pacote só é aceitável quando houver relação técnica clara e o
agrupamento estiver registrado; caso contrário, manter commits, validações e
referências separados por issue.

Não misturar no mesmo branch ou commit alterações de outra issue, experimento,
pacote ou projeto. Se o worktree já contiver alterações que não pertencem à
tarefa atual, preservá-las e trabalhar apenas nos caminhos autorizados.

Alterações em dependências forkadas ou em outros repositórios devem ter escopo
próprio, referência explícita ao repositório/branch/tag/commit e verificação de
compatibilidade antes de serem incorporadas à aplicação.

## Commits, push, revisão e encerramento

Os commits devem ser pequenos, coerentes e reversíveis, com mensagem em
português do Brasil que descreva o resultado. Antes de criar o commit, revisar
o diff completo e confirmar que não há segredos, arquivos temporários ou
alterações de outra tarefa.

Depois do commit, publicar a branch de trabalho no remoto correto e conferir o
commit efetivamente publicado. Registrar na issue os commits, pull requests e
resultados de validação relevantes, usando links permanentes quando possível.

O commit ou o push não encerram uma issue por si só. Encerrar somente após a
implementação estar validada, a revisão ou integração prevista ter ocorrido e
as referências finais terem sido publicadas na issue. Se o escopo mudar,
registrar a decisão antes de continuar; não fechar e recriar uma issue apenas
para ocultar histórico ou perda de contexto.

Quando houver pull request, mantê-lo vinculado à issue e descrever claramente
escopo, dependências, testes, limitações conhecidas e procedimento de
validação. A integração em `dev` ou em outra branch de destino depende da
revisão e aprovação previstas para aquela mudança.

Falhas de autenticação, permissão, remoto ou publicação devem ser
diagnosticadas explicitamente. Não concluir que uma issue, branch ou arquivo
não existe apenas por causa de resposta de acesso negado, repositório errado
ou sessão não autenticada.

## Docker Desktop e stacks locais

O desenvolvimento e a validação local usam Docker Desktop com containers
Linux. O código da aplicação deve ser executado a partir de imagens
empacotadas, construídas pelo Dockerfile, sem bind mount das pastas de código
do Windows para dentro dos containers.

Após alterações em PHP, Twig, JavaScript, CSS, traduções, configurações,
bundles ou outros arquivos incorporados na imagem, reconstruir a imagem e
recriar somente o container da aplicação ou do serviço alterado. O banco e os
demais serviços persistentes não devem ser recriados sem necessidade explícita.

Volumes nomeados podem ser usados para dados persistentes, como banco,
cache controlado ou modelos aprovados. Eles não substituem o empacotamento do
código da aplicação ou do serviço.

A linha de portas reservada ao fork23 é:

- `9000`: stack DEV;
- `9001`: stack de VALIDAÇÃO;
- `9002`: serviço ou stack TTS;
- `900X`: novas stacks e serviços, conforme forem definidos.

As portas externas são referências do ambiente local. A comunicação entre
containers deve usar a rede interna e o nome do serviço Docker sempre que
possível. Não assumir que `localhost` dentro de um container representa outro
container.

Antes de liberar uma alteração para teste, confirmar:

1. imagem reconstruída quando houver alteração incorporada nela;
2. container recriado com a imagem nova;
3. cache e assets atualizados quando aplicável;
4. estado saudável do container;
5. arquivos ou endpoints servidos correspondem à versão nova;
6. ausência de bind mount de código na validação final.

## Qualidade, segurança e validação

Validar a sintaxe e os testes correspondentes ao escopo. Quando aplicável,
executar lint de PHP, Twig, YAML, JavaScript/CSS, testes unitários,
integração, migrations e verificação de rotas/configuração.

Não registrar segredos, tokens, senhas ou credenciais em arquivos versionados,
comandos persistidos, commits, issues ou logs públicos. Configurações externas
devem usar variáveis de ambiente ou mecanismos próprios de secrets.

Dados enviados a serviços auxiliares devem ser mínimos e justificados. Não
enviar dados pessoais ao serviço TTS quando a frase puder ser construída apenas
com senha, prioridade, serviço, local e número do local.

Licenças de bibliotecas, imagens, modelos de voz e demais artefatos externos
devem ser verificadas antes de sua distribuição em uma imagem ou release.

Falhas de serviços auxiliares, Mercure, áudio ou TTS não podem interromper o
fluxo visual principal quando houver uma estratégia de recuperação prevista.

## Evolução deste arquivo

Este arquivo é vivo. Novos fluxos de branch, Docker, validação, publicação,
licenciamento, migração de issues e releases devem ser incorporados aqui quando
forem regras globais. Procedimentos exclusivos de uma branch devem permanecer
no respectivo `AGENTS-NOME_DA_BRANCH`.
