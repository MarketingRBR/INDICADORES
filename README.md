# RBR Trade Marketing — Central de Acompanhamento

Dashboard de BI para acompanhamento da equipe de Trade Marketing da RBR Representações (Agosto/2026). Roda 100% no navegador — sem backend, sem banco de dados. Todos os dados vêm de dois arquivos Excel que você mesmo já usa no dia a dia.

🔗 **Acesse:** `https://SEU-USUARIO.github.io/NOME-DO-REPO/`

---

## Como funciona

```
Excel do Involves (relatório gerencial de visitas)
Excel manual (indicadores, metas, bônus)
            ↓
      Upload no dashboard
            ↓
  Leitura, cruzamento e cálculo (tudo no navegador)
            ↓
   Cards, gráficos, ranking, premiação
```

Nada é digitado dentro do dashboard. O Excel é a fonte oficial; o dashboard é só a camada de análise.

---

## Passo a passo de uso

1. Abra o link do site.
2. Na aba **"📥 Atualização dos Dados"**:
   - Envie o **relatório do Involves** (opcional — sem ele, alguns indicadores calculados automaticamente ficam indisponíveis, mas o dashboard funciona só com a planilha manual).
   - Envie a **planilha manual de acompanhamento** (obrigatória — é dela que vêm metas, realizado e bônus).
3. Confira a **Conferência de Colaboradores**, que tenta casar automaticamente os nomes do Involves com os 6 promotores da equipe.
4. Clique em **"🔄 Atualizar Dashboard"**.
5. Use **"🔍 Ver Dados Importados"** a qualquer momento para auditar exatamente o que o sistema leu de cada arquivo.

---

## O que o dashboard calcula

- **Visitas + Cadastros** (indicador principal de meta): para a maioria dos promotores é visitas do Involves + novos cadastros somados; para o **Fabrício**, visitas e cadastros são indicadores separados, com metas próprias, e mostrados sempre discriminados.
- **Ritmo do mês**: média diária atual, ritmo necessário para bater a meta, projeção de fechamento — considerando dias úteis reais do período (segunda a sábado, por padrão).
- **Premiação financeira**: lida direto da coluna BÔNUS da planilha manual. Reconhece dois formatos:
  - Valor fixo (ex.: `150`) → paga só se a meta do indicador foi atingida.
  - Fórmula por unidade (ex.: `=E20*300`) → paga realizado × valor unitário, sem depender de bater meta.
- **Ranking**: por % de meta atingida, por bônus acumulado ou por ritmo — nunca só por volume bruto.
- **Alertas gerenciais**: quem está abaixo do ritmo, quem está perto de liberar um novo bônus, etc. — gerados automaticamente.

**Regra de ouro:** se um valor não foi apurado (célula vazia na planilha), o dashboard mostra "—" / "aguardando apuração" — nunca transforma em zero.

---

## Estrutura esperada da planilha manual

O arquivo real usado pela RBR (`ACOMPANHAMENTO_INDICADORES_TRADE_AGOSTO_2026.xlsx`) tem um bloco por promotor, assim:

```
[Nome do promotor]
INDICADOR              | META | REALIZADO | FALTA | STATUS | % ATINGIDO | BÔNUS
Visitas Realizadas      | 119  |    ...    |  ...  |  ...   |    ...     |  150
Novos Cadastros         |      |           |       |        |            |
Distribuidores          |  9   |           |       |        |            |  150
...
BÔNUS PREVISTO          |      |           |       |        |            | =SOMA(...)
```

O sistema varre a planilha inteira procurando esse padrão — não precisa ser uma aba com nome específico.

---

## Fotos dos promotores

As fotos ficam embutidas no próprio `index.html` (em base64), então não há arquivos de imagem soltos para gerenciar. Para trocar uma foto, é preciso gerar um novo `index.html` (posso fazer isso a qualquer momento, é só enviar a foto nova).

---

## Privacidade

Todo o processamento acontece no navegador de quem está usando o link — os arquivos Excel enviados não passam por nenhum servidor. Os dados ficam salvos no **localStorage do navegador** (só naquele dispositivo/navegador específico), então fechar a aba ou voltar depois não apaga mais nada — a última planilha importada continua lá. Para limpar, use o botão "🗑 Limpar dados salvos" na tela de upload. Como cada navegador/dispositivo tem sua própria memória local, isso não substitui um banco de dados compartilhado: se duas pessoas acessarem o link em computadores diferentes, cada uma verá os dados que ela mesma importou.

---

## Publicando/atualizando no GitHub Pages

1. Repositório público no GitHub, com o `index.html` na raiz.
2. Settings → Pages → Branch: `main` / pasta `/ (root)` → Save.
3. O link fica em `https://SEU-USUARIO.github.io/NOME-DO-REPO/`.
4. Para atualizar: suba um novo `index.html` substituindo o antigo (Add file → Upload files → mesmo nome → Commit).
