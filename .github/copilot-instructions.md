# Instruções para AI Coding Agents - Projeto Cassino

## Visão Geral
Landing page single-file HTML para oferta de cashback de cassino. Single-file: todo CSS e JS inline. Objetivo: conversão via 2 botões (cadastro verde + WhatsApp ouro) com foco mobile-first e animações de background rotativo.

## Arquitetura & Estrutura
- **Arquivo único**: [index.html](index.html) (~400 linhas) - CSS `<style>` + JS `<script>` inline
- **Sem dependências**: Projeto standalone, zero frameworks
- **Imagens**: `/images/` contém backgrounds rotativos (aposta poseidon, zeus, dionisio) + legal footer tag (tag18-branca.png)

## Paleta de Cores (CSS :root)
```css
--gold: #f7d07b           /* Primária: textos/botões ouro */
--green: #16ff6e          /* CTA principal: botão cadastro */
--glass: rgba(16,20,45,.62)  /* Fundo card com blur */
--bg0: #060812, --bg1: #0b1130  /* Background base escuro */
```

## Padrões de Design Críticos
- **Card glassmorphism**: `.card` com `backdrop-filter: blur(10px)` + border semitransparente
- **Animações**: `.hero` usa `@keyframes bgRotate` (18s, 3 imagens em 33%/66%/100%)
- **Gradientes**: Extensivos em textos (`.grad`), botões e sombras de glow
- **Acessibilidade**: `@media (prefers-reduced-motion: reduce)` desativa animações

## Fluxo de Conversão (2 Botões)
1. **Botão verde** (`.btn.primary`): `handleCadastroClick()` → abre URL cadastro em nova aba via `window.open()`
2. **Botão ouro** (`.btn.secondary`): `handleWhatsClick()` → redirect direto para WhatsApp via `window.location.href`

### URLs (constantes no `<script>`)
```javascript
CADASTRO_URL = "https://brsuperbet.com/registro_9490"
WHATS_URL = "https://wa.me/5516988193058?text=..."
```

## Pontos Críticos de Edição

### Modificar botões/conversão
- Editar URLs em constantes `<script>` (final do arquivo)
- NÃO remover `onclick="handleCadastroClick"` ou `handleWhatsClick` - usados para fluxos abertos em nova aba
- Classes `.btn.primary` (verde) e `.btn.secondary` (ouro) - não invertir cores

### Responsividade
- **Breakpoint mobile**: `@media (max-width: 420px)` - ajusta h1 (30px), card padding, background estático
- **Background mobile**: `images/estatua-mobile.png.png` (nota: extensão duplicada no arquivo atual)
- Botões sempre `100%` width no mobile

### Animações background
- 3 imagens rotam em `@keyframes bgRotate` (0% → 33% → 66% → 100%)
- **Para adicionar 4ª imagem**: ajustar percentuais para 25%/50%/75%/100% e inserir novo `background-image` em @keyframes

### Compliance
- `.legal` (fixed bottom, branco) - obrigatório, contém `tag18-branca.png`
- Manter disclaimer em `.fine` sobre validação e WhatsApp
- Nunca remover avisos legais

## Estrutura HTML (ordem importante)
1. `.hero` - seção principal com overlay + vignette + sparkles + `.wrap` → `.card`
2. `.card` → `.pill` (badge) + `h1` + `.sub` + `.chips` + `.headline` + `.steps` (lista 4 passos) + `.btns` (2 botões) + `.fine`
3. `.legal` - fixed bottom bar com imagem tag

## Desenvolvimento Comum
- **Alterar oferta/texto**: editar `<h1>`, `.sub`, `.steps` mantendo estrutura
- **Mudar cores**: ajustar vars em `:root`
- **Testar acessibilidade**: verificar `prefers-reduced-motion` desativa animações
- **Testar conversão**: ambos botões em mobile (≤420px) e desktop
