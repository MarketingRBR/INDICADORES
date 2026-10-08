# RBR Trade Marketing — Central de Acompanhamento

Dashboard de BI para acompanhamento da equipe de Trade Marketing da RBR Representações, mês a mês (Agosto, Setembro, Outubro/2026...). Roda 100% no navegador — sem backend, sem banco de dados próprio. Todos os dados vêm dos arquivos Excel que você já usa no dia a dia.

🔗 **Acesse:** `https://SEU-USUARIO.github.io/NOME-DO-REPO/`

---

## Como funciona

```
Tela de escolha do mês (Agosto / Setembro / Outubro...)
            ↓
Excel do Involves (relatório gerencial de visitas) — opcional
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

1. Abra o link do site — a primeira tela pede pra você **escolher o mês**. Cada mês guarda seus próprios dados (local e, se configurado, na nuvem), então trocar de mês nunca apaga o anterior. Um selo "✓ Dados salvos" aparece nos meses que já têm algo importado.
2. Depois de escolher o mês, na aba **"📥 Atualização dos Dados"**:
   - Envie o **relatório do Involves** (opcional — sem ele, alguns indicadores calculados automaticamente ficam indisponíveis, mas o dashboard funciona só com a planilha manual).
   - Envie a **planilha manual de acompanhamento daquele mês** (obrigatória — é dela que vêm metas, realizado e bônus).
3. Confira a **Conferência de Colaboradores**, que tenta casar automaticamente os nomes do Involves com os promotores da equipe.
4. Clique em **"🔄 Atualizar Dashboard"**.
5. Use **"🔍 Ver Dados Importados"** a qualquer momento para auditar exatamente o que o sistema leu de cada arquivo.
6. Pra trocar de mês depois, use o seletor no topo ou o botão **"🏠 Trocar mês"**, que volta pra tela inicial.

### Metas e indicadores variam por mês

Agosto e Setembro/2026 já vêm com as metas oficiais pré-carregadas (usadas como padrão sempre que a planilha manual não trouxer um valor). Outubro em diante começa **zerado de propósito** — o dashboard não inventa meta nenhuma; tudo vem da aba METAS do Excel daquele mês. Setembro introduziu indicadores que não existiam em Agosto (Bate-papo/Treinamento Promotor separado de Palestras com o Técnico, Homologação Linha Pesada por fábrica específica, Acompanhamento Pós-Homologação) — o sistema reconhece esses nomes automaticamente, não precisa configurar nada.

### Promotores da equipe

Severino, Fabrício, Lucas, Jorge, Taylor, Vanderson e Juliana (com metas), mais Alexandre e a Promotora de Merchandising (sem metas: aparecem com foto e visitas, mas ficam fora dos totais da equipe, do ranking e dos alertas). Se o nome da Promotora de Merchandising no Involves não contiver a palavra "merchandising", vincule-a manualmente na Conferência de Colaboradores. Para que o reconhecimento automático de nomes funcione (tanto no relatório do Involves quanto na planilha manual), o primeiro nome de cada um precisa aparecer em algum lugar do campo "Colaborador"/"Notificante"/"Promotor" do arquivo.

---

## O que o dashboard calcula

- **Visitas + Cadastros** (indicador principal de meta): para a maioria dos promotores é visitas do Involves + novos cadastros somados; para o **Fabrício**, visitas e cadastros são indicadores separados, com metas próprias, e mostrados sempre discriminados.
- **Ritmo do mês**: média diária atual, ritmo necessário para bater a meta, projeção de fechamento — considerando dias úteis reais do período (segunda a sábado, por padrão).
- **Premiação financeira**: lida direto da coluna BÔNUS da planilha manual. Reconhece dois formatos:
  - Valor fixo (ex.: `150`) → paga só se a meta do indicador foi atingida.
  - Fórmula por unidade (ex.: `=E20*300`) → paga realizado × valor unitário, sem depender de bater meta.
- **Ranking**: por % de meta atingida, por bônus acumulado ou por ritmo — nunca só por volume bruto.
- **Alertas gerenciais**: quem está abaixo do ritmo, quem está perto de liberar um novo bônus, etc. — gerados automaticamente.
- **Semana Foco (automático)**: se você subir a exportação da pesquisa "Semana Foco" do Involves (terceiro upload, opcional), o REALIZADO desse indicador é contado automaticamente por promotor (via campo "Notificante"), com detalhamento de Fábrica / Cliente / Cidade na página individual — a Cidade vem do cruzamento com o relatório do Involves. Sem esse arquivo, o indicador continua funcionando normalmente com o valor da planilha manual.

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

Todo o processamento acontece no navegador de quem está usando o link. Os dados ficam salvos no **localStorage do navegador** (só naquele dispositivo/navegador específico) como cópia local — fechar a aba ou voltar depois não apaga nada. Para limpar, use o botão "🗑 Limpar dados salvos" na tela de upload.

Sem a nuvem configurada (veja abaixo), cada pessoa que abre o link só vê os dados que ela mesma importou naquele navegador — não é compartilhado com o resto da equipe.

---

## Compartilhar com a equipe toda (sem cada um subir Excel) — Firebase

Por padrão, cada navegador guarda seus próprios dados. Para que **todo mundo veja o mesmo dashboard**, atualizado automaticamente, é preciso conectar uma nuvem compartilhada. Usamos o **Firebase** (Google), que tem plano gratuito e não exige cartão de crédito. Leva uns 5 minutos:

### Passo a passo

1. Acesse **https://console.firebase.google.com** e faça login com uma conta Google.
2. Clique em **"Adicionar projeto"** → dê um nome (ex.: `rbr-trade-dashboard`) → pode desativar o Google Analytics → **Criar projeto**.
3. No menu lateral, clique em **"Firestore Database"** → **"Criar banco de dados"**.
   - Escolha a localização (ex.: `southamerica-east1` — São Paulo).
   - Em "Regras de segurança", escolha **"Iniciar no modo de teste"** (permite leitura/escrita por 30 dias — depois ajustamos a regra para ficar permanente, ver abaixo).
4. Ainda no console, clique no ícone de engrenagem (topo esquerdo) → **"Configurações do projeto"**.
5. Role até "Seus apps" → clique no ícone **"</>"** (Web) → dê um apelido (ex.: `dashboard`) → **Registrar app**.
6. O Firebase vai mostrar um bloco de código com um objeto `firebaseConfig` parecido com este:
   ```js
   const firebaseConfig = {
     apiKey: "AIzaSy...",
     authDomain: "rbr-trade-dashboard.firebaseapp.com",
     projectId: "rbr-trade-dashboard",
     storageBucket: "rbr-trade-dashboard.appspot.com",
     messagingSenderId: "123456789",
     appId: "1:123456789:web:abcdef123456"
   };
   ```
7. Copie esses 6 valores e cole no arquivo `index.html`, procurando por `FIREBASE_CONFIG` (perto do topo do bloco `<script>`) e preenchendo cada campo entre aspas.
8. Salve, suba o `index.html` atualizado no GitHub (substitui o antigo) e pronto — o badge "🌐" aparece no topo do dashboard confirmando a conexão.

### Regra de segurança (depois dos 30 dias de teste)

Em **Firestore Database → Regras**, troque pelo seguinte (permite leitura livre — necessário para a equipe ver — e escrita livre, já que é um dashboard interno sem dados sensíveis de clientes/senhas):

```
rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /rbr_dashboard/{doc} {
      allow read, write: if true;
    }
  }
}
```

⚠️ Isso deixa o documento gravável por qualquer pessoa que tenha o link do dashboard (não por qualquer pessoa na internet em geral, mas tecnicamente qualquer um que inspecione o código consegue a chave). Para um dashboard interno de uma equipe pequena isso costuma ser aceitável; se quiser mais segurança (exigir login antes de publicar), é possível adicionar Firebase Authentication depois — me avise que ajudo a configurar.

### Como usar depois de configurado

- Quem sobe os Excel clica em **"📤 Publicar para a equipe"** depois de calcular o dashboard.
- Qualquer pessoa que abrir o link já vê os dados publicados automaticamente — e se alguém publicar de novo enquanto a página está aberta, ela atualiza sozinha, sem precisar dar F5.
- Sem clicar em "Publicar", os dados ficam só no seu navegador (como antes).

---

## Publicando/atualizando no GitHub Pages

1. Repositório público no GitHub, com o `index.html` na raiz.
2. Settings → Pages → Branch: `main` / pasta `/ (root)` → Save.
3. O link fica em `https://SEU-USUARIO.github.io/NOME-DO-REPO/`.
4. Para atualizar: suba um novo `index.html` substituindo o antigo (Add file → Upload files → mesmo nome → Commit).
