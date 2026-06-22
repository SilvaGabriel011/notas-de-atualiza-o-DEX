# Notas de Atualização · Kotai DEX

Site estático (deploy no Vercel) com o histórico de releases. Cada release tem
uma galeria com várias versões de design da mesma página de notas.

## Estrutura

- `index.html` — página inicial: lista/histórico de releases.
- `galeria.html` — galeria do release de 12/06 (versões na raiz: `v1-*.html` … `v6-*.html`).
- `AAAA-MM-DD/` — uma pasta por release novo, contendo:
  - `index.html` — galeria daquele release.
  - `v1-original.html` … `v6-hero-glow.html` — as versões de design.

## Como adicionar um novo relatório de atualização

1. **Crie a pasta do release** com a data: `AAAA-MM-DD/` (ex.: `2026-07-10/`).
2. **Copie** para dentro dela a galeria e as 6 versões de um release existente
   (ex.: a pasta `2026-06-22/`) e troque o conteúdo das notas e a data.
3. **Registre o release** no topo do array `releases`, dentro do `<script>` de
   `index.html`:

   ```js
   {
     date: '2026-07-10',                         // AAAA-MM-DD (ordena sozinho)
     version: 'Release · 10 de julho de 2026',
     tag: 'Atual',                               // tire o 'Atual' do release anterior
     desc: 'Resumo curto do release.',
     counts: { novo: 0, melhoria: 0, correcao: 0 },
     link: '2026-07-10/index.html',              // pasta/index.html
   },
   ```

## Cuidado importante com links (o bug que já corrigimos)

O `vercel.json` usa `cleanUrls: true`, então a galeria é servida em
`/AAAA-MM-DD` **sem barra final**. Por isso, **não use links relativos**
(`v1-original.html`) dentro da galeria de uma pasta: eles resolveriam para a
raiz e abririam o conteúdo de outro release.

A galeria já resolve isso sozinha: ela descobre a própria pasta a partir da URL
(`const base = location.pathname.replace(/\/(index\.html)?$/, '')`) e monta os
links como `${base}/${arquivo}`. Mantendo esse trecho ao copiar a galeria, um
release novo funciona sem ajustar caminho nenhum.
