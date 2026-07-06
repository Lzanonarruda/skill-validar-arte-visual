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

- **Lê:** caminho da imagem a validar, fornecido pelo usuário ou pela skill que chamou (qualquer PNG/JPG do vault — sem acoplamento a cliente ou estrutura de pastas específica)
- **Escreve:** nada
- **Cria:** nada — o output é só o relatório de texto

## Dependências externas

Nenhuma. Usa a capacidade nativa de leitura de imagem do agente — não depende de MCP nem serviço externo.

---

## Protocolo

1. Receber o caminho da imagem a validar (obrigatório) e, se disponível, o contexto de marca (paleta, tipografia, princípios de design) — usado no critério 7
2. Abrir a imagem de verdade e observá-la — nunca avaliar só pelo código-fonte (HTML/CSS) que a gerou, mesmo que ele esteja disponível. Julgamento visual exige ver o resultado renderizado
3. Avaliar os 12 critérios obrigatórios (abaixo), item por item
4. Aplicar as 5 regras complementares (A–E)
5. Montar o relatório no formato obrigatório (6 seções)
6. Entregar o relatório. Se a chamada veio de outra skill, ela decide o que fazer com o resultado — esta skill não corrige a arte, só avalia

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
11. **Chamada para ação** — o CTA é claro, visível, e parece consequência natural da peça — não um bloco desconectado?
12. **Percepção de confiança** — a arte transmite profissionalismo, organização, credibilidade e coerência com o objetivo da marca?

### Regras complementares

**A — Elementos decorativos só existem se tiverem função visual clara.** Se uma linha, borda ou detalhe estiver fraco/sutil demais pra comunicar algo, decidir entre reforçar a presença ou remover por completo — nunca deixar num meio-termo ambíguo (existe, mas não comunica nada).

**B — Em fotos com pessoas, preservar rostos, expressões e partes essenciais.** Não cortar olhos, boca, queixo ou topo da cabeça de forma desconfortável. Pequenos cortes em cabelo, ombros, braços ou fundo são aceitáveis quando melhoram a composição sem causar estranheza — nem todo corte é defeito, só o que afeta elementos humanos essenciais.

**C — Foto-fonte limitada não deve ser "corrigida" à força.** Quando a imagem original é limitada (ex: selfie muito próxima, pouca margem ao redor das pessoas, enquadramento original restritivo), não tentar consertar com distorção, esticamento ou invenção artificial de área. Compor bem ao redor da limitação e registrar isso na seção 5 do relatório, como observação sobre o insumo — não como defeito da arte a ser forçado.

**D — O CTA precisa estar visualmente conectado ao texto e ao objetivo da arte.** Se estiver muito distante do conteúdo, ou desproporcional a outros elementos do rodapé (ex: minúsculo perto de um logo grande, ou gigante perto de um logo minúsculo), solicitar ajuste antes de aprovar.

**E — Bonita não é sinônimo de aprovada.** Só aprovar quando a arte parecer coesa, intencional, legível, equilibrada e bem acabada. Cumprir os 12 critérios isoladamente não basta se os blocos não se relacionarem bem entre si (ver critério 10 — Equilíbrio visual).

### Formato obrigatório da resposta

Responder sempre com estas 6 seções, nesta ordem exata:

**1. Resultado geral** — uma classificação: `Cumpre` / `Cumpre parcialmente` / `Não cumpre`

**2. Veredito final** — uma decisão: `Aprovada` / `Aprovada com observações` / `Solicitar ajustes antes de aprovar` / `Reprovada`

**3. Avaliação por critério** — para cada um dos 12 critérios: Status, o que cumpre ou não cumpre, por que, e o que é necessário pra cumprir (se houver ajuste)

**4. Ajustes prioritários** — separados em Prioridade alta / Prioridade média / Prioridade baixa. Se não houver ajustes relevantes, declarar explicitamente que a arte está pronta pra publicação

**5. Observações sobre a imagem-fonte** — se houver limitação real (selfie muito próxima, baixa margem ao redor das pessoas, enquadramento original restritivo), registrar aqui como limitação do insumo (ver Regra C) — nunca como defeito a corrigir à força no layout

**6. Conclusão final** — frase objetiva dizendo se a arte pode ser publicada ou não, e por quê

## Verificação

- [ ] Abriu e observou a imagem de verdade (não só o código-fonte)
- [ ] Os 12 critérios foram avaliados individualmente, com status explícito
- [ ] As 5 regras complementares (A–E) foram checadas
- [ ] O relatório segue as 6 seções, na ordem exata
- [ ] Limitação de imagem-fonte (se houver) foi registrada como observação, não como defeito forçado

## Casos especiais

**Chamada por outra skill (não diretamente pelo usuário):** devolver o relatório completo pra skill que chamou. Essa skill decide se corrige a arte e chama de novo, ou se repassa o relatório ao usuário — `validar-arte-visual` não decide isso sozinha, só avalia.

**Sem contexto de marca disponível:** se não houver paleta, tipografia ou princípios de design fornecidos, avaliar o critério 7 (Consistência visual) só pela coerência interna da peça (as cores e fontes usadas conversam entre si), sem comparar contra um padrão de marca externo. Registrar essa limitação na Avaliação por critério.

**Quando usar veredito "Reprovada":** reservar para casos graves — rosto cortado de forma desconfortável (Regra B), mensagem incompreensível, texto ilegível, ausência de elemento obrigatório (ex: logo, CTA). A maioria dos ajustes de refinamento cabe em "Solicitar ajustes antes de aprovar", não em reprovação total.
