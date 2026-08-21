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
formato `AGENTS-NOME_DA_BRANCH.md`, por exemplo `AGENTS-TTS.md`. A extensão
`.md` é obrigatória para todos os arquivos secundários de fluxo. Esse arquivo
registra somente regras, decisões, escopo, validações e procedimentos
específicos da branch onde está inserido.

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

1. ler o `AGENTS.md` e o arquivo `AGENTS-NOME_DA_BRANCH.md`, quando existir;
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

## Anotações do WhatsApp e conexão com o Chrome

Quando o responsável solicitar a importação de anotações do ZAP para o fork23,
a fonte será a conversa indicada no WhatsApp Web autenticado no Google Chrome
do usuário. A conversa é uma fonte auxiliar de pendências e contexto; o
GitHub, este arquivo e os arquivos secundários continuam sendo o registro
canônico das decisões do projeto.

Para essa operação, usar o controle do Chrome externo do usuário. O navegador
integrado do Codex não substitui essa sessão autenticada. Se a conexão falhar:

1. confirmar que o Chrome do usuário está aberto;
2. abrir ou reutilizar `https://web.whatsapp.com/` no perfil correto;
3. confirmar que a sessão está autenticada e repetir a conexão uma vez;
4. registrar objetivamente o que foi verificado antes de declarar bloqueio.

Não substituir a conversa por buscas no workspace, exportações antigas ou
outra sessão sem autorização. Durante uma importação, começar pela mensagem
mais recente e seguir para trás até o marcador mais recente
`ATÉ AQUI TUDO FOI ENCAMINHADO`, incluindo textos, imagens e legendas apenas
do trecho posterior ao marcador.

As anotações importadas devem ser tratadas primeiro como pendências. Para cada
item, classificar como issue nova, complemento de issue existente, duplicidade,
pendência operacional ou item já tratado. Comparar com as issues existentes e
apresentar uma triagem numerada antes de criar issues ou alterar escopo. Se uma
issue fechada receber novo requisito, reabrir a issue antes de registrar o
complemento. Depois de o ciclo aprovado ser encaminhado ao GitHub, registrar o
marcador na conversa quando essa ação fizer parte da solicitação.

## Publicação no GitHub e operação do terminal

Para GitHub e Docker Hub, dar preferência a `git`, `gh`, Docker CLI e APIs
autenticadas. Usar navegador somente quando a operação depender de uma sessão
web, como a importação do WhatsApp, ou quando o terminal não for confiável.

Antes de operações administrativas, confirmar o repositório, branch, remoto e
autenticação com `git remote -v`, `git branch --show-current` e `gh auth
status`. Se houver falha de credencial, `schannel`, sandbox ou permissão,
repetir pela execução autorizada disponível. Respostas `404`, ausência de
resultados ou `Validation Failed` não provam sozinhas que um repositório,
branch, issue ou arquivo não existe; verificar autenticação, visibilidade e
destino antes de concluir.

Todo texto humano publicado no GitHub deve estar em português do Brasil,
incluindo commits, issues, comentários, pull requests, releases e notas. Os
comentários devem usar quebras reais de linha, preferencialmente preparados em
arquivo UTF-8. Ao encerrar uma issue pelo terminal, publicar primeiro o
comentário com `gh issue comment --body-file` e somente depois executar
`gh issue close`; validar no GitHub o texto, os links e o estado final.

## Workspace local e organização de arquivos

A raiz exclusiva de trabalho do fork23 é:

`C:\Users\fbravo\Documents\Codex\fork23`

Nenhuma worktree, pasta auxiliar, dump, script, log, captura de tela, arquivo
de issue, análise externa ou outro artefato relacionado ao fork23 deve ser
criado fora dessa raiz. Worktrees e pastas auxiliares devem usar nomes que
identifiquem o projeto, preferencialmente o padrão `fork23-<identificador>`.

Worktrees oficiais:

- DEV: `C:\Users\fbravo\Documents\Codex\fork23\fork23-dev`;
- TTS: `C:\Users\fbravo\Documents\Codex\fork23\fork23-tts`.

Artefatos que não fazem parte do repositório devem ficar em uma pasta auxiliar
identificada, como `fork23-work`, dentro da raiz. Eles não devem entrar em
commits por engano. Análises de upstream, ferramentas de apoio e dumps devem
ser mantidos em subpastas igualmente identificadas, sem reutilizar pastas ou
arquivos de outro projeto.

Os binários do cliente MySQL destinados aos túneis locais ficam em:

`C:\Users\fbravo\Documents\Codex\fork23\mysql-26.7.0-winx64`

Esse diretório é ferramenta local e não deve ser versionado no repositório.

## Modelo padrão de desenvolvimento e teste

O modelo padrão do fork23 é executar a aplicação e os serviços a partir de
imagens Docker reconstruídas, com containers Linux no Docker Desktop e sem
bind mount do código-fonte do Windows. O bind mount pode ser usado somente
como diagnóstico temporário, com o motivo registrado, e deve ser removido
antes da validação final.

Após alterações em PHP, Twig, JavaScript, CSS, traduções, configurações,
bundles, dependências incorporadas ou arquivos do serviço TTS:

1. validar a sintaxe e os arquivos alterados;
2. reconstruir a imagem correspondente;
3. recriar somente o container alterado;
4. atualizar cache e assets quando aplicável;
5. confirmar saúde, versão servida e ausência de bind mount de código.

O banco, Mercure e demais serviços persistentes devem permanecer ativos e não
ser recriados sem necessidade explícita. Volumes nomeados podem preservar
dados ou modelos aprovados, mas não substituem o empacotamento do código.

As portas externas seguem a linha do fork23: `9000` para DEV, `9001` para
validação, `9002` para TTS e `900X` para novas stacks. Entre containers, usar o
nome do serviço na rede interna; `localhost` dentro de um container não é o
host nem outro container.

## Segurança operacional no PowerShell

Hashes bcrypt contêm caracteres `$`, normalmente no formato `$2y$12$...`.
Nunca inserir um hash bcrypt diretamente em SQL delimitado por aspas duplas no
PowerShell, pois a shell pode interpretar os `$` como variáveis.

Quando for necessário gerar ou atualizar uma senha de teste, gerar o hash no
container da aplicação e transportá-lo em base64, ou usar outro mecanismo que
preserve literalmente os bytes. Depois, validar o tamanho do hash, o algoritmo
e o login efetivo dentro do container. Nunca registrar senha, hash completo,
token ou credencial em arquivo versionado, issue, commit ou log público.

## Injeção de dados sintéticos

Uma injeção sintética só pode ocorrer mediante solicitação explícita e deve
ser limitada ao ambiente DEV autorizado. Nunca executar em produção nem usar
os dados gerados para compor dumps de entrega, releases ou validação de
produção.

Antes de escrever, confirmar stack, container, porta, banco e branch de código.
Preferir serviços internos da aplicação, migrations ou scripts controlados,
com transação e integridade referencial. A massa deve respeitar o modelo de
dados do fork23, ser identificável e ter quantidades e estados definidos pelo
caso de teste; não importar as quantidades, usuários ou entidades específicas
do `novosga_tjrs`.

Após a execução, conferir os totais esperados, estados do fluxo, relatórios,
acentuação, ausência de duplicidades e a inexistência de qualquer escrita fora
do DEV. Scripts e evidências devem permanecer em `fork23-work` ou subpasta
equivalente dentro da raiz do projeto, nunca em pastas externas.

## Restauração de dumps MySQL

O banco oficial da aplicação fork23 permanece sendo o PostgreSQL definido pelo
projeto. Esta seção se aplica somente a stacks auxiliares, legadas ou de
integração que utilizem MySQL, quando tal stack for explicitamente criada.

Ao restaurar um dump MySQL, nunca enviar o arquivo por pipeline textual do
PowerShell (`Get-Content`, `type`, `cat` ou equivalentes), pois isso pode
corromper bytes UTF-8 e acentuação. O procedimento obrigatório é:

1. confirmar inequivocamente o container e o banco de destino;
2. copiar o dump para dentro do container com `docker cp`;
3. importar dentro do container usando redirecionamento do shell Linux;
4. informar o charset esperado, normalmente `utf8mb4`;
5. aplicar migrations/configurações necessárias;
6. limpar cache, recriar somente a aplicação e aguardar estado saudável;
7. validar acentuação, caracteres especiais, consultas e relatórios.

Não sobrescrever bancos, volumes ou dumps sem confirmar o alvo. O arquivo
original deve permanecer em `fork23-work` ou em outra subpasta da raiz, e
credenciais devem ser fornecidas por mecanismo seguro, nunca incorporadas ao
comando persistido ou ao Git.

## Contexto de telas e responsividade

O fork23 deve ser validado no contexto real dos monitores e janelas usados no
projeto, sem importar nomes de unidades, setores, dimensões ou fluxos
específicos do `novosga_tjrs`. Para cada mudança de interface, registrar as
dimensões relevantes quando forem conhecidas e testar pelo menos uma janela
desktop em paisagem e uma janela alta e estreita, representando o uso em
retrato.

Priorizar grades flexíveis, redução dinâmica de larguras e consultas pelo
tamanho do container quando apropriado. Não empilhar quadros apenas por um
breakpoint genérico; empilhar quando as larguras mínimas funcionais não
couberem. Preservar ações e informações principais, evitando sobreposição,
rolagem horizontal e rolagem vertical desnecessária.

Para o painel e as telas relacionadas ao TTS, validar também chamadas rápidas,
alertas, fila de áudio e comportamento com o serviço externo indisponível,
sempre nos ambientes reservados do fork23.

## Túneis locais e cliente MySQL

As conexões do cliente MySQL aos túneis locais do fork23 usam as portas:

- `6000`: túnel local MySQL DEV;
- `7000`: túnel local MySQL de validação ou segundo ambiente autorizado.

Usar os binários em
`C:\Users\fbravo\Documents\Codex\fork23\mysql-26.7.0-winx64\bin`,
confirmando host, porta, banco e ambiente antes de qualquer consulta de
escrita. As portas `6000` e `7000` são túneis de administração e não alteram a
linha de portas HTTP do fork23. Nunca assumir que um túnel está conectado ao
ambiente correto sem verificar a identidade do banco.

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
no respectivo `AGENTS-NOME_DA_BRANCH.md`.
