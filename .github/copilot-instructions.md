# Instruções para AI Coding Agents - Projeto Cassino

## Visão Geral do Projeto
Landing page promocional single-file para oferta de cashback de cassino online. Foco em conversão através de design atrativo com tema greco-mitológico (Poseidon, Zeus, Dionísio) e fluxo otimizado para mobile.

## Estrutura e Arquitetura
- **Single-file HTML**: Todo CSS inline em `<style>` e JavaScript inline em `<script>`
- **Sem dependências externas**: Projeto standalone, sem frameworks ou bibliotecas
- **Assets externos**: Imagens em `/images/` (aposta-poseidon.png, aposta-poseidon-2.png, aposta-zeus.png, aposta-dionisio.png)

## Convenções de Design e Estilo

### Paleta de Cores (CSS Custom Properties)
```css
--gold: #f5c56b           /* Cor primária dourada */
--gold-dark: #c89b3c      /* Dourado escuro */
--bg: #0b0f1a             /* Background escuro */
--green: #1aff64          /* CTAs de ação */
```

### Padrões de Design
- **Gradientes**: Usados extensivamente para profundidade (backgrounds, texto, botões)
- **Glassmorphism**: `.card` usa `backdrop-filter: blur(6px)` com fundo semitransparente
- **Animações**: Background rotativo com `@keyframes bgRotate` (18s loop entre imagens)
- **Acessibilidade**: `@media (prefers-reduced-motion: reduce)` desabilita animações

### Componentes UI Principais
- `.badge`: Tag de destaque com gradiente dourado
- `.card`: Container principal com glassmorphism e bordas douradas
- `.cta`: Botões de call-to-action com hover effects e sombras intensas
- `.sticky-cta`: CTA fixo no mobile (visível apenas <640px)

## Fluxo de Conversão
1. **Botão principal verde** → Abre cadastro em nova aba + redireciona para WhatsApp
2. **Botão dourado secundário** → Envia direto para WhatsApp (usuários já cadastrados)
3. **CTA fixo mobile** → Replica botão principal para acesso rápido ao rolar

### Configuração de URLs (JavaScript)
```javascript
CADASTRO_URL = "https://brsuperbet.com/registro_9490"
WHATS_URL = "https://wa.me/5571986135263?text=..."
```

## Regras de Desenvolvimento

### Ao Modificar CTAs
- Mantenha 2 botões: verde (cadastro) + dourado (WhatsApp já cadastrado)
- CTA fixo mobile deve sempre espelhar o botão principal
- Preserve `onclick` handlers para fluxo de abertura em nova aba + redirecionamento

### Ao Ajustar Responsividade
- Breakpoint principal: `480px` (ajustes de fonte/padding)
- Sticky CTA aparece em `640px` e abaixo
- Legal footer fixo deve ficar sempre visível (60px altura aprox.)

### Ao Trabalhar com Animações
- Background rotativo usa imagens da pasta `/images/`
- Tempo de rotação: 18s (ajustável em `@keyframes bgRotate`)
- Sempre testar com `prefers-reduced-motion` para acessibilidade

### Compliance e Legal
- Rodapé branco fixo com avisos obrigatórios: +18, jogo responsável, Portaria SPA/MF
- Não remover ou ocultar avisos legais
- Manter linguagem sobre "cashback" e "promocional" (não é aposta direta)

## Otimizações de Conversão

### Mobile-First
- CTA fixo aparece automaticamente em telas pequenas
- Font-sizes escalam proporcionalmente
- Touch targets adequados (min 44px padding nos botões)

### UX de Duplo Funil
- **Usuários novos**: Botão verde → cadastro + WhatsApp
- **Usuários retornando**: Botão dourado → WhatsApp direto
- Delay de 900ms entre abertura de cadastro e redirecionamento para WhatsApp

## Testes e Validação
- Testar ambos os botões em mobile e desktop
- Verificar abertura em nova aba do cadastro
- Confirmar redirecionamento para WhatsApp após delay
- Validar responsividade em 320px, 480px, 640px, 1024px
- Testar com motion-reduced para acessibilidade

## Exemplos de Modificações Comuns

### Alterar URLs de conversão:
Editar constantes JavaScript no `<script>` final

### Mudar esquema de cores:
Ajustar custom properties em `:root` no `<style>`

### Adicionar nova imagem ao background rotativo:
Inserir nova etapa em `@keyframes bgRotate` (calcular % baseado em número total de imagens)

### Modificar texto da oferta:
Editar `<h1>`, `.highlight` e `.steps` mantendo estrutura de emojis nos passos
