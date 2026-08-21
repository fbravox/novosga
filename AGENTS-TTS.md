# Fluxo da branch TTS

## Identidade e objetivo

Esta branch é `TTS`, no fork público `fbravox/novosga`. Ela concentra a
preparação do painel do fork23 e a implementação da vocalização com dois
motores:

- Web Speech API no navegador;
- serviço TTS externo em container próprio.

O escopo foi originado na issue #101 do projeto `fbravox/novosga_tjrs` e será
acompanhado pela issue migrada para o fork23. A issue original só deve ser
considerada encerrada quando a nova referência estiver publicada e vinculada.

## Worktree e anotações da branch

O worktree oficial desta branch é:

`C:\Users\fbravo\Documents\Codex\fork23\fork23-tts`

O arquivo secundário desta branch é `AGENTS-TTS.md`. A extensão `.md` é
obrigatória para os arquivos secundários de fluxo; ele deve permanecer na
raiz do worktree TTS e acompanhar as regras globais do `AGENTS.md` sem
substituí-las.

Anotações, dumps, capturas, scripts de teste, modelos baixados para avaliação
e textos intermediários da TTS devem permanecer em subpastas identificadas de
`C:\Users\fbravo\Documents\Codex\fork23`, preferencialmente em `work`. A
pasta `work` é a exceção oficial à nomenclatura `fork23-<identificador>` e
segue o padrão do Codex. Não criar ou manter artefatos desta branch no workspace do
`novosga_tjrs` ou fora da raiz do fork23.

Anotações recebidas pela conversa de WhatsApp do responsável devem seguir o
fluxo global de importação pelo Chrome e somente entram no escopo da TTS após
triagem, comparação com a issue migrada e registro no GitHub. Não transformar
automaticamente uma mensagem do ZAP em alteração de código ou issue nova.

## Pré-requisito obrigatório: painel

Antes de iniciar a adição da funcionalidade TTS, o painel do fork23 deve
receber as customizações já presentes em:

`https://github.com/fbravox/novosga_tjrs/tree/feature/painel`

Essa referência deve ser adaptada para a arquitetura, bundles, entidades,
permissões, banco e contratos do fork23. Não copiar identidade visual,
infraestrutura, banco, autenticação, arquivos de fluxo ou procedimentos
específicos do `novosga_tjrs` sem decisão expressa.

A ordem de trabalho desta branch é:

1. consolidar a base do painel v2.3;
2. adaptar as customizações funcionais e visuais necessárias do painel;
3. validar layout, chamadas, histórico, Mercure, polling e alertas;
4. somente depois iniciar o TTS.

Não considerar a funcionalidade TTS pronta enquanto o painel-base dessa etapa
não estiver integrado e validado.

## Escopo do TTS

O SGA continua sendo a autoridade dos dados de chamada. O painel recebe a
chamada por Mercure/SSE e consulta HTTP quando necessário. A voz é uma etapa
independente da atualização visual.

O motor deve ser selecionável por painel, usando a configuração persistida no
metadata de painel existente. O contrato inicial deve contemplar:

- habilitação da vocalização;
- motor `web_speech` ou `external_tts`;
- idioma, inicialmente `pt-BR`;
- voz Web Speech e política de seleção;
- modelo/voz do TTS externo;
- velocidade e volume;
- tom quando o motor for Web Speech;
- pronúncia de zeros à esquerda;
- composição segura da frase;
- fallback e tratamento de indisponibilidade.

A configuração antiga do painel deve continuar válida. O MVP não deve exigir
migration apenas para adicionar esses campos ao metadata JSON.

## Serviço externo

O TTS externo será executado em container separado, com imagem empacotada e
sem bind mount do código. A porta local reservada é `9002`; a comunicação
entre containers deve usar o nome DNS interno do serviço.

O serviço deve possuir, no mínimo:

- endpoint de saúde;
- endpoint de vozes/modelos disponíveis;
- endpoint de síntese que retorne áudio WAV;
- modelo carregado de forma persistente na memória do processo;
- limites de tamanho, tempo e concorrência;
- logs sem texto pessoal desnecessário;
- licenças e modelo aprovados antes da distribuição.

Piper é a primeira opção de avaliação para o motor externo. O modelo `pt_BR`
deve ser escolhido e fixado somente após teste de qualidade, desempenho e
verificação do `MODEL_CARD` e da licença correspondente.

O navegador não deve chamar diretamente um host ou porta do container TTS. O
SGA deve atuar como intermediário, validando o painel e a `PainelSenha` antes
de solicitar ou entregar o áudio.

O fluxo de chamada não pode bloquear esperando síntese. Se o serviço estiver
indisponível, o painel deve continuar atualizando a chamada, registrar a falha
e aplicar o fallback configurado.

## Segurança e dados da frase

A frase deve ser construída a partir dos dados mínimos necessários. No MVP,
priorizar senha, prioridade, serviço, local e número do local. Não enviar nome,
documento ou outros dados pessoais do cliente ao serviço TTS sem decisão
específica e justificativa.

O endpoint de áudio deve validar que o registro pertence à unidade, ao painel
e aos serviços configurados. Não aceitar texto livre arbitrário do navegador
como entrada de síntese.

## Fila e comportamento do painel

Web Speech e áudio externo devem usar uma fila única, com:

- deduplicação de eventos;
- ordem correta para chamadas rápidas;
- ausência de sobreposição;
- tratamento de rechamada;
- timeout e recuperação;
- falha de voz sem interromper SSE, polling ou renderização.

As políticas de autoplay do navegador devem ser tratadas no ambiente de
exibição. Não criar dependência de um botão manual de desbloqueio como parte do
MVP sem decisão posterior.

## Bundles e dependências

Se a configuração exigir alteração em `PainelSettings`, o contrato deve ser
atualizado no `core` forkado. O formulário administrativo deve ser atualizado
no `panel-bundle` forkado. A aplicação `novosga` deve consumir versões ou
branches explicitamente controladas dessas dependências e atualizar o
`composer.lock` de forma reproduzível.

Alterações nesses repositórios devem manter compatibilidade com a base v2.3 e
ser registradas na issue migrada e neste arquivo quando afetarem o escopo da
branch.

## Stacks e validação da branch

Aplicar as portas globais do projeto:

- DEV integrada: `9000`;
- VALIDAÇÃO: `9001`;
- TTS local: `9002`.

As stacks devem usar imagens reconstruídas e containers recriados, sem
mapeamento do código-fonte. A validação deve confirmar:

1. painel visual funcional antes do TTS;
2. chamadas por Mercure e recuperação HTTP;
3. vocalização Web Speech;
4. vocalização pelo container externo;
5. funcionamento com o TTS parado ou lento;
6. fila, deduplicação e chamadas rápidas;
7. ausência de exposição indevida de dados;
8. healthcheck, logs e inicialização do container;
9. comportamento em monitor horizontal e janela alta/estreita.

O serviço MySQL auxiliar, quando necessário para diagnóstico ou integração,
deve ser acessado pelos túneis locais definidos no fluxo global, nas portas
`6000` (DEV) e `7000` (validação/segundo ambiente), usando os binários em
`C:\Users\fbravo\Documents\Codex\fork23\mysql-26.7.0-winx64\bin`. Isso não
substitui o PostgreSQL oficial do fork23 nem altera as portas HTTP da stack.

Os procedimentos globais de bcrypt no PowerShell, dados sintéticos, dumps
MySQL e responsividade devem ser aplicados somente com o contexto da TTS e sem
importar nomes, quantidades, bancos, portas ou dados específicos do
`novosga_tjrs`.

## Atualização do fluxo

Decisões sobre modelo, contrato, endpoints, configuração, fallback, licença,
portas e critérios de aprovação devem ser registradas neste arquivo quando
forem confirmadas. Regras que se tornarem globais devem ser promovidas para o
`AGENTS.md` principal e sincronizadas nas branches ativas.
