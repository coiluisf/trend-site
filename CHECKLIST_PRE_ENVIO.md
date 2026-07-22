# 📋 Checklist de Pré-Envio - Trend Hair Landing Page

## 🔴 CRÍTICO (Bloqueadores)

### 1. **Estrutura de Arquivos**
- [ ] Criar pasta `/assets/photos/` com as imagens:
  - `hero.jpg` (imagem hero - 1920x1080 recomendado)
  - `servico-corte-feminino.jpg` (220px altura)
  - `servico-coloracao.jpg`
  - `servico-mechas.jpg`
  - `servico-escova.jpg`
  - `servico-tratamentos.jpg`
  - `servico-manicure.jpg`
  - `servico-pedicure.jpg`
  - `servico-sobrancelhas.jpg`
  - `servico-maquiagem.jpg`
  - `servico-penteados.jpg`
  - `estrutura-recepcao.jpg` (260px altura)
  - `estrutura-espaco-interno.jpg`
  - `estrutura-cafeteria.jpg` (falta - usar placeholder)
  - `estrutura-jardim.jpg`
  - `estrutura-lavagem.jpg`
  - `estrutura-manicure.jpg` (falta - usar placeholder)
  - `ba-antes-1.jpg` (440px altura)
  - `ba-depois-1.jpg`
  - `ba-antes-2.jpg`
  - `ba-depois-2.jpg`
  - `ba-antes-3.jpg`
  - `ba-depois-3.jpg`

- [ ] Adicionar `assets/trend-hair-logo.png` (logo em PNG com background transparente)

- [ ] Colocar os arquivos JS no root:
  - `support.js` (dc-runtime)
  - `image-slot.js` (componente de imagem)

### 2. **Meta Tags SEO (Adicionar no `<head>`)**
```html
<meta name="description" content="Salão de beleza premium em Porto Alegre. Corte, coloração, tratamentos capilares, manicure e mais. Profissionais especializadas, ambiente elegante, atendimento personalizado.">
<meta name="keywords" content="salão de beleza, Porto Alegre, corte feminino, coloração, mechas, escova, manicure">
<meta name="author" content="Trend Hair">
<meta name="theme-color" content="#111111">

<!-- Open Graph para redes sociais -->
<meta property="og:title" content="Trend Hair · Salão de Beleza Premium em Porto Alegre">
<meta property="og:description" content="Experiência completa em beleza, autoestima e bem-estar. Clientes satisfeitas com 4.8★ e +530 avaliações.">
<meta property="og:image" content="https://seu-dominio.com/assets/og-image.jpg">
<meta property="og:type" content="website">
<meta property="og:url" content="https://seu-dominio.com">

<!-- Twitter Card -->
<meta name="twitter:card" content="summary_large_image">
<meta name="twitter:title" content="Trend Hair · Salão de Beleza Premium">
<meta name="twitter:description" content="Profissionais especializadas, produtos premium e ambiente sofisticado.">
```

### 3. **Favicon**
- [ ] Criar `favicon.ico` (16x16, 32x32, 64x64)
- [ ] Criar `apple-touch-icon.png` (180x180)
- [ ] Adicionar no `<head>`:
```html
<link rel="icon" type="image/x-icon" href="favicon.ico">
<link rel="apple-touch-icon" href="apple-touch-icon.png">
```

### 4. **Image Slot State**
- [ ] Verificar se o arquivo `.imageslots.state.json` está no mesmo diretório do HTML
- [ ] Conteúdo atual tem referência a `structure-lavagem` - verificar se é necessário

---

## 🟡 IMPORTANTE (Qualidade)

### 5. **Otimização de Imagens**
- [ ] Converter todas as imagens para WebP com fallback JPG
  - Fotos principais: 80% qualidade
  - Compressão máxima com `imagemin` ou similar
  
- [ ] Lazy loading: Adicionar `loading="lazy"` em `<img>` fora do viewport

- [ ] Sizes responsivos:
```html
<!-- Para hero -->
<img ... srcset="
  hero-mobile.jpg 480w,
  hero-tablet.jpg 768w,
  hero-desktop.jpg 1920w"
  sizes="(max-width: 768px) 100vw, 100vw">
```

### 6. **Performance - Lighthouse**
- [ ] Minificar CSS inline (atualmente muito grande)
- [ ] Verificar Core Web Vitals:
  - LCP (Largest Contentful Paint): < 2.5s
  - FID (First Input Delay): < 100ms
  - CLS (Cumulative Layout Shift): < 0.1

- [ ] Remover fontes não usadas (atualmente: Playfair Display + Inter)
  - Usar `font-display: swap` para otimizar

### 7. **Validação HTML**
- [ ] Rodar validador W3C HTML
- [ ] Verificar:
  - ✅ IDs únicos (ref="{{ headerSentinelRef }}" não é ID HTML - verificar)
  - ✅ Alt texts em todas as imagens (OK)
  - [ ] Tags semânticas (adicionar `<main>` e `<aside>` onde apropriado)

### 8. **Acessibilidade (WCAG 2.1)**
- [ ] Contraste de cores:
  - ✅ #C7A46A (ouro) em #111111 (preto) - PASS
  - ✅ #111111 em #ffffff (branco) - PASS
  - [ ] Verificar #4a4a4a (cinza) em #ffffff - pode estar margem

- [ ] Aria labels:
  - ✅ Botões têm aria-label ✓
  - [ ] Adicionar aria-label em dots de testimonial
  - [ ] Considerar aria-live em contador de ratings

- [ ] Keyboard navigation:
  - [ ] Testar TAB em todos os botões
  - [ ] Menu mobile deve ter focus trap

### 9. **Responsividade Mobile**
- [ ] Testar em:
  - iPhone SE (375px)
  - iPhone 12 (390px)
  - Pixel 5 (393px)
  - Tablet (768px)
  - iPad (1024px)

- [ ] Verificar media queries existentes (vejo até 900px e 560px)

### 10. **Funcionalidades JavaScript**
- [ ] Testar:
  - ✅ Menu hamburger (toggleMenu)
  - ✅ Scroll header (IntersectionObserver)
  - ✅ Testimonials auto-rotate (6s)
  - ✅ FAQ accordion
  - ✅ Before/After carousel
  - [ ] Counter animation (4.8 rating)
  
- [ ] Verificar se todos os refs estão funcionando

### 11. **Links e Formulários**
- [ ] WhatsApp link é dinâmico:
  ```
  https://wa.me/5551991528060?text=Olá%2C%20gostaria%20de%20agendar%20um%20horário%20no%20Trend%20Hair.
  ```
  - [ ] **CRÍTICO**: Verificar se o número (55) 99152-8060 é ATIVO
  - [ ] Testar link em desktop e mobile

- [ ] Âncoras internas funcionando:
  - [ ] #inicio
  - [ ] #servicos
  - [ ] #avaliacoes
  - [ ] #contato

### 12. **Redes Sociais**
- [ ] Verificar links:
  - Instagram: https://www.instagram.com/estetica_trendhair/
  - Facebook: https://www.facebook.com/trend.hair.rs/
  - WhatsApp: (55) 99152-8060

---

## 🟢 BOAS PRÁTICAS

### 13. **404 & Redirect Pages**
- [ ] Criar página 404.html simples
- [ ] Configurar redirects na Hostinger (settings/rewrite rules)

### 14. **robots.txt**
```
User-agent: *
Allow: /
Disallow: /admin/
Sitemap: https://seu-dominio.com/sitemap.xml
```

### 15. **sitemap.xml**
Criar sitemap com as seções principais

### 16. **SSL/HTTPS**
- [ ] Ativar certificado SSL na Hostinger (grátis com Let's Encrypt)
- [ ] Redirecionar HTTP → HTTPS

### 17. **Velocidade**
- [ ] Ativar Gzip compression na Hostinger
- [ ] Cache headers:
  - Imagens: 1 ano
  - CSS/JS: 1 mês
  - HTML: Sem cache

### 18. **Google Analytics**
- [ ] Adicionar Google Analytics 4 (GA4)
- [ ] Tag Manager (GTM) para track eventos de CTA

### 19. **Google Search Console**
- [ ] Submeter sitemap
- [ ] Verificar cobertura
- [ ] Monitorar erros de crawl

### 20. **Email de Contato**
- [ ] ⚠️ **NÃO há formulário de email** - apenas WhatsApp
- [ ] Considerar adicionar formulário?
  ```html
  <form method="POST" action="https://formspree.io/f/[SEU_ID]">
    <input type="email" name="email" required>
    <textarea name="message" required></textarea>
    <button type="submit">Enviar</button>
  </form>
  ```

---

## 📝 ESTRUTURA FINAL RECOMENDADA

```
seu-dominio.com/
├── index.html (Trend_Hair.dc.html renomeado)
├── support.js
├── image-slot.js
├── favicon.ico
├── apple-touch-icon.png
├── robots.txt
├── sitemap.xml
├── .imageslots.state.json
├── assets/
│   ├── trend-hair-logo.png
│   ├── og-image.jpg (1200x630 para Open Graph)
│   └── photos/
│       ├── hero.jpg
│       ├── servico-*.jpg (11 fotos)
│       ├── estrutura-*.jpg (6 fotos)
│       └── ba-*.jpg (6 fotos antes/depois)
├── css/
│   └── (se minificar estilos inline)
└── 404.html
```

---

## ⚡ ANTES DE PUBLICAR

1. [ ] Renomear `Trend_Hair.dc.html` → `index.html`
2. [ ] Testar localmente com `python -m http.server` ou Live Server
3. [ ] Executar Lighthouse audit (Chrome DevTools)
4. [ ] Testar em mobile real (não apenas DevTools)
5. [ ] Testar todos os botões CTA (WhatsApp)
6. [ ] Verificar velocidade com GTmetrix
7. [ ] Validar HTML com W3C
8. [ ] Testar com adblocker ativo (alguns bloqueiam WhatsApp)

---

## 📞 PARA O CLIENTE

### Checklist de apresentação:
- [ ] Mostrar layout desktop, tablet e mobile
- [ ] Demonstrar interações:
  - Menu mobile
  - Scroll do header
  - Carousel de antes/depois
  - FAQ accordion
  - Hover states
- [ ] Explicar como agendar (WhatsApp com pré-preenchido)
- [ ] Mostrar avaliações e rating
- [ ] Testar link de WhatsApp com o cliente (importante!)

---

**Tempo estimado de conclusão:** 2-4 horas para preparar tudo

**Prioridade de correção:**
1. Adicionar todas as imagens (estrutura de assets)
2. Meta tags SEO + og: tags
3. Favicon
4. Testar funcionalidades
5. Otimizar imagens
6. Performance audit
