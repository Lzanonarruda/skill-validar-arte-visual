---
description: Valida se uma arte/peça visual (post, thumbnail, carrossel) tem aparência profissional antes de publicar — 12 critérios + relatório estruturado.
when_to_use: valida essa arte, revisa essa peça, essa arte tá pronta pra publicar, autoavaliação visual, checklist de arte, validação de post antes de aprovar
---

# Skill: Validar Arte Visual

## Gatilho
Usuário pede pra validar ou revisar uma peça visual antes de publicar ("valida essa arte", "essa peça tá pronta?", "revisa esse post antes de aprovar", "essa thumbnail tá profissional?"). Também é invocada automaticamente por outras skills de geração de arte como etapa de autoavaliação, antes de apresentar uma versão ao usuário.

---

## Por que esta skill existe

Gerar uma arte que cumpre critérios técnicos isolados (fonte legível, cor de marca certa, dimensão correta) não garante que ela pareça uma peça profissional acabada. Uma arte pode passar em cada critério individual e ainda parecer "quase pronta" se os blocos não se relacionarem bem entre si — CTA gigante ao lado de logo minúsculo, respiro concentrado num único vazio, elemento decorativo fraco demais pra ter função. O critério real de "arte profissional" está tanto na qualidade de cada parte quanto na coerência do conjunto.

Esta skill nasceu como uma etapa de autoavaliação dentro de uma skill de geração de posts, mas o que define "arte profissional" não depende do cliente, da marca ou da ferramenta usada pra gerar a peça — então foi extraída como skill própria. Isso evita duplicar o mesmo checklist em cada skill de geração visual (e, principalmente, evita que ele fique desatualizado em algumas delas quando é refinado numa só).

---

## Acesso ao vault

- **Lê:** a imagem a validar — caminho local, anexo, URL interna ou referência fornecida pela skill que chamou, conforme o ambiente de execução (sem acoplamento a cliente ou estrutura de pastas específica)
- **Escreve:** nada
- **Cria:** nada — o output é só o relatório de texto

## Dependências externas

Nenhuma. Usa a capacidade nativa de leitura de imagem do agente — não depende de MCP nem serviço externo.

---

## Protocolo

1. Receber a imagem a validar — caminho local, anexo, URL interna ou referência fornecida pela skill chamadora
2. Identificar o contexto disponível da peça: objetivo da arte, canal de publicação (feed, story, thumbnail, anúncio, carrossel, capa), público-alvo, elementos obrigatórios, restrições do pedido (manter cores, fontes, textos, imagem) e contexto de marca (paleta, tipografia, princípios de design — usado no critério 7). Se essas informações não estiverem disponíveis, avaliar com base no uso mais provável e registrar a limitação no relatório
3. Abrir e observar a imagem **renderizada final** — nunca avaliar só pelo código-fonte, HTML, CSS, SVG, JSON ou prompt que gerou a peça. Esses materiais podem servir de apoio pra entender uma decisão, mas o julgamento visual precisa ser sobre o resultado percebido, não sobre a intenção do código
4. Avaliar os 12 critérios obrigatórios (abaixo), item por item, sempre à luz do contexto identificado no passo 2 (o padrão de exigência muda conforme canal/objetivo — ver Regra F)
5. Aplicar as 6 regras complementares (A–F)
6. Classificar cada achado por severidade: **problema impeditivo** (compromete a publicação) · **ajuste recomendado** (melhora a peça, mas não impede publicar) · **microajuste opcional** (refinamento óptico, não necessário pra aprovar). Nunca solicitar nova versão quando só restarem microajustes opcionais
7. Montar o relatório no formato obrigatório (6 seções)
8. Entregar o relatório. Se a chamada veio de outra skill, ela decide o que fazer com o resultado — esta skill não corrige a arte, só avalia

### Critérios obrigatórios de validação

1. **Clareza da mensagem** — a arte comunica rapidamente o tema principal? A pessoa entende sem esforço o que está sendo mostrado e qual é a informação central?
2. **Hierarquia visual** — existe ordem clara de leitura? A composição guia o olhar naturalmente entre imagem, título, texto de apoio, CTA e assinatura da marca?
3. **Alinhamento** — os elementos parecem posicionados com intenção? Margens, consistência de grade visual, ausência de elementos soltos?
4. **Espaçamento e respiro** — a arte não parece apertada nem vazia demais? Os espaços ajudam a leitura, a separação entre blocos e a sensação de acabamento?
5. **Legibilidade** — o texto é fácil de ler no celular? Tamanho de fonte, contraste, peso visual, entrelinha, leitura rápida?
6. **Contraste** — as cores ajudam a leitura e o destaque das informações mais importantes, sem competir entre si?
7. **Consistência visual** — a arte parece parte da identidade da marca? Coerência entre cores, fontes, formas, assinatura visual e estilo geral?
8. **Qualidade da imagem** — a imagem está nítida, bem enquadrada e coerente com a mensagem? (se a foto-fonte tiver limitação real, ver Regra C)
9. **Acabamento visual** — sombras, cantos, bordas, logo, proporções e posicionamento parecem finalizados, não improvisados?
10. **Equilíbrio visual** — os elementos têm pesos proporcionais? Nem CTA, nem título, nem foto, nem logo dominam ou desaparecem de forma incoerente?
11. **Chamada para ação** — se a peça tiver CTA (nem toda tem, ver regra de obrigatoriedade condicional), ele é claro, visível, e parece consequência natural da peça — não um bloco desconectado?
12. **Percepção de confiança** — a arte transmite profissionalismo, organização, credibilidade e coerência com o objetivo da marca?

### Regras complementares

**A — Elementos decorativos só existem se tiverem função visual clara.** Se uma linha, borda ou detalhe estiver fraco/sutil demais pra comunicar algo, decidir entre reforçar a presença ou remover por completo — nunca deixar num meio-termo ambíguo (existe, mas não comunica nada).

**B — Em fotos com pessoas, preservar rostos, expressões e partes essenciais.** Não cortar olhos, boca, queixo ou topo da cabeça de forma desconfortável. Pequenos cortes em cabelo, ombros, braços ou fundo são aceitáveis quando melhoram a composição sem causar estranheza — nem todo corte é defeito, só o que afeta elementos humanos essenciais.

**C — Foto-fonte limitada não deve ser "corrigida" à força.** Quando a imagem original é limitada (ex: selfie muito próxima, pouca margem ao redor das pessoas, enquadramento original restritivo), não tentar consertar com distorção, esticamento ou invenção artificial de área. Compor bem ao redor da limitação e registrar isso na seção 5 do relatório, como observação sobre o insumo — não como defeito da arte a ser forçado.

**D — O CTA precisa estar visualmente conectado ao texto e ao objetivo da arte.** Se estiver muito distante do conteúdo, ou desproporcional a outros elementos do rodapé (ex: minúsculo perto de um logo grande, ou gigante perto de um logo minúsculo), solicitar ajuste antes de aprovar.

**E — Bonita não é sinônimo de aprovada.** Só aprovar quando a arte parecer coesa, intencional, legível, equilibrada e bem acabada. Cumprir os 12 critérios isoladamente não basta se os blocos não se relacionarem bem entre si (ver critério 10 — Equilíbrio visual).

**F — Estilo visual intencional não é erro.** Uma arte pode ser assimétrica, editorial, tipo colagem, popular, ousada ou expressiva e ainda ser profissional, desde que a escolha pareça coerente, legível, funcional e alinhada ao objetivo/canal identificado no passo 2 do protocolo. O problema não é fugir da grade clássica — é parecer acidental, desorganizado ou improvisado. Antes de reprovar por "falta de alinhamento" ou "hierarquia incomum", considerar se aquilo é uma escolha de estilo coerente com o contexto (ex: thumbnail de YouTube aceita contraste/exagero maior que post institucional; story aceita CTA mais forte; post de prova social pode depender mais da foto que do texto).

### Formato obrigatório da resposta

Responder sempre com estas 6 seções, nesta ordem exata:

**1. Resultado geral** — uma classificação: `Cumpre` / `Cumpre parcialmente` / `Não cumpre`

**2. Veredito final** — uma decisão: `Aprovada` / `Aprovada com observações` / `Solicitar ajustes antes de aprovar` / `Reprovada`

**3. Avaliação por critério** — para cada um dos 12 critérios: Status, o que cumpre ou não cumpre, por que, e o que é necessário pra cumprir (se houver ajuste)

**4. Ajustes prioritários** — separados em Prioridade alta (problema impeditivo — compromete a publicação) / Prioridade média (ajuste recomendado — melhora a peça, mas não impede publicar) / Prioridade baixa (microajuste opcional — refinamento óptico). Nunca solicitar nova versão só por causa de itens de prioridade baixa. Se não houver ajustes de prioridade alta ou média, declarar explicitamente que a arte está pronta pra publicação

**5. Observações sobre a imagem-fonte** — se houver limitação real (selfie muito próxima, baixa margem ao redor das pessoas, enquadramento original restritivo), registrar aqui como limitação do insumo (ver Regra C) — nunca como defeito a corrigir à força no layout

**6. Conclusão final** — frase objetiva dizendo se a arte pode ser publicada ou não, e por quê

## Verificação

- [ ] Contexto da peça (objetivo, canal, público, elementos obrigatórios, restrições) foi identificado ou a limitação de não tê-lo foi registrada
- [ ] Abriu e observou a imagem renderizada final (não só o código-fonte)
- [ ] Os 12 critérios foram avaliados individualmente, com status explícito, à luz do contexto identificado
- [ ] As 6 regras complementares (A–F) foram checadas
- [ ] Cada achado foi classificado por severidade (impeditivo / recomendado / microajuste opcional)
- [ ] O relatório segue as 6 seções, na ordem exata
- [ ] Limitação de imagem-fonte (se houver) foi registrada como observação, não como defeito forçado

## Casos especiais

**Chamada por outra skill (não diretamente pelo usuário):** devolver o relatório completo pra skill que chamou. Essa skill decide se corrige a arte e chama de novo, ou se repassa o relatório ao usuário — `validar-arte-visual` não decide isso sozinha, só avalia.

**Sem contexto de marca disponível:** se não houver paleta, tipografia ou princípios de design fornecidos, avaliar o critério 7 (Consistência visual) só pela coerência interna da peça (as cores e fontes usadas conversam entre si), sem comparar contra um padrão de marca externo. Registrar essa limitação na Avaliação por critério.

**Quando usar veredito "Reprovada":** reservar para casos graves — mensagem incompreensível, texto ilegível, corte desconfortável em rostos ou partes essenciais de pessoas (Regra B), desalinhamento estrutural grave, composição claramente improvisada, contraste que impede a leitura, ou ausência de um elemento definido como **obrigatório pelo briefing** (logo, CTA, data, preço, produto, identificação da marca — só quando o objetivo/canal/padrão de marca exige, não por padrão). A maioria dos ajustes de refinamento cabe em "Solicitar ajustes antes de aprovar" ou "Aprovada com observações", não em reprovação total.

**CTA e logo não são obrigatórios por padrão.** Nem toda arte precisa de CTA — peças institucionais, comemorativas, informativas, topo de carrossel, posts de relacionamento, capas e thumbnails sem chamada comercial direta costumam não ter. Nem toda peça precisa de logo visível — ex: arte pra story com perfil já identificado, ou quando a marca aparece no cabeçalho da própria plataforma. Validar a obrigatoriedade desses elementos pelo contexto identificado no passo 2 do protocolo (objetivo, canal, briefing), nunca como regra fixa aplicada a toda arte.
