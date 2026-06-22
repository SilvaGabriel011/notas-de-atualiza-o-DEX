# Notas de Atualização · Kotai DEX

Site estático (deploy no Vercel) com o histórico de releases. O layout adotado é
o **V6 (Hero)**.

## Estrutura

- `index.html` — página inicial: lista/histórico de releases. Cada item abre
  direto a página de notas daquele release (na mesma aba).
- `v6-hero-glow.html` — notas do release de 12/06 (layout V6).
- `AAAA-MM-DD/v6-hero-glow.html` — notas de cada release novo (uma pasta por release).
- `v1-*.html` … `v5-*.html` — versões de design antigas, mantidas no repositório
  apenas para referência (não estão linkadas em lugar nenhum).

## Como adicionar um novo relatório de atualização

1. **Crie a pasta do release** com a data: `AAAA-MM-DD/` (ex.: `2026-07-10/`).
2. **Copie** para dentro dela o `v6-hero-glow.html` de um release existente e
   troque o conteúdo das notas, a data e os contadores.
3. **Registre o release** no topo do array `releases`, dentro do `<script>` de
   `index.html`:

   ```js
   {
     date: '2026-07-10',                          // AAAA-MM-DD (ordena sozinho)
     version: 'Release · 10 de julho de 2026',
     tag: 'Atual',                                // tire o 'Atual' do release anterior
     desc: 'Resumo curto do release.',
     counts: { novo: 0, melhoria: 0, correcao: 0 },
     link: '2026-07-10/v6-hero-glow.html',        // pasta/arquivo do V6
   },
   ```

## Observação sobre links

O `vercel.json` usa `cleanUrls: true`. Dentro das páginas, prefira links
**absolutos** (começando com `/`) — como o botão "voltar" do V6, que aponta para
`/`. Links relativos podem resolver para a raiz quando a URL não tem barra final.
