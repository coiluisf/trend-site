# 🚀 Guia de Deploy Hostinger - Trend Hair

## Passo 1: Preparar os Arquivos

### 1.1 Estrutura de Diretórios
```
public_html/
├── index.html
├── support.js
├── image-slot.js
├── favicon.ico
├── robots.txt
├── sitemap.xml
├── .htaccess (opcional, para redirects)
├── assets/
│   ├── trend-hair-logo.png
│   ├── og-image.jpg
│   └── photos/
│       └── (todas as fotos de serviços)
└── 404.html
```

### 1.2 Arquivos a Renomear
```bash
# Renomear o DC HTML para index.html
mv Trend_Hair.dc.html index.html
```

---

## Passo 2: Configurações na Hostinger

### 2.1 Painel de Controle (cPanel)
1. Acesse **cPanel** → **Gerenciador de Arquivos**
2. Navegue para **public_html/**
3. Faça upload dos arquivos (ou via FTP)

### 2.2 SSL/HTTPS
1. Vá em **SSL/TLS**
2. Ative **"Autorizar HTTP"** → Use HTTPS apenas
3. Crie certificado Let's Encrypt (grátis):
   - cPanel → SSL/TLS → Auto-Configure
   - Selecione seu domínio
   - Deixar 90 dias de auto-renovação ✓

### 2.3 Compressão & Cache
1. **cPanel** → **Compressão Gzip**
   - Ative Gzip para `.js`, `.css`, `.html`, `.svg`

2. **Cabeçalhos de Cache (.htaccess)**
```apache
<IfModule mod_headers.c>
    # Cache 1 ano para imagens
    <FilesMatch "\.(jpg|jpeg|png|gif|ico|webp)$">
        Header set Cache-Control "max-age=31536000, public"
    </FilesMatch>
    
    # Cache 1 mês para assets
    <FilesMatch "\.(js|css)$">
        Header set Cache-Control "max-age=2592000, public"
    </FilesMatch>
    
    # Sem cache para HTML
    <FilesMatch "\.(html|htm)$">
        Header set Cache-Control "max-age=0, public, must-revalidate"
    </FilesMatch>
</IfModule>

# Redirecionar HTTP para HTTPS
<IfModule mod_rewrite.c>
    RewriteEngine On
    RewriteCond %{HTTPS} off
    RewriteRule ^(.*)$ https://%{HTTP_HOST}%{REQUEST_URI} [L,R=301]
</IfModule>
```

### 2.4 Redirects Permanentes (se tiver subdomínios)
cPanel → Parked Domains & Redirects

---

## Passo 3: Validação Antes de Publicar

### 3.1 Checklist Local
```bash
# Testar localmente com Python
python -m http.server 8000

# Ou com Node.js
npx http-server
```

Acessar: `http://localhost:8000`

### 3.2 Validações
- [ ] **HTML Validation**: https://validator.w3.org/
- [ ] **Lighthouse**: Chrome DevTools → Lighthouse
  - Performance: > 90
  - Accessibility: > 90
  - Best Practices: > 90
  - SEO: > 90

- [ ] **Mobile**: Testar em smartphone real (não emulador)
- [ ] **Links**: Todos os botões e âncoras funcionando
- [ ] **WhatsApp**: Testar clique em CTA (abrir WhatsApp)

### 3.3 Performance Check
- https://gtmetrix.com/
- https://pagespeed.web.dev/

---

## Passo 4: SEO & Indexação

### 4.1 Submeter ao Google
1. Acesse Google Search Console: https://search.google.com/search-console
2. Adicione seu domínio
3. Submeta o sitemap.xml

### 4.2 Google Analytics
1. Crie conta em: https://analytics.google.com/
2. Adicione seu domínio
3. Copie o tracking ID
4. Adicione no HTML:

```html
<!-- Google Analytics -->
<script async src="https://www.googletagmanager.com/gtag/js?id=G-XXXXXXXXXX"></script>
<script>
  window.dataLayer = window.dataLayer || [];
  function gtag(){dataLayer.push(arguments);}
  gtag('js', new Date());
  gtag('config', 'G-XXXXXXXXXX');
</script>
```

### 4.3 Meta Tags Verificadas
- ✅ Descrição (160 caracteres)
- ✅ Og:image (1200x630px)
- ✅ Canonical: `<link rel="canonical" href="https://seu-dominio.com">`

---

## Passo 5: Problemas Comuns & Soluções

### ⚠️ "Imagens não carregam"
```html
<!-- ERRADO -->
<img src="assets/foto.jpg">

<!-- CORRETO (com / no início) -->
<img src="/assets/foto.jpg">
```

### ⚠️ "Scripts não funcionam"
```html
<!-- Verificar que support.js e image-slot.js estão em public_html/ -->
<script src="./support.js"></script>
<script src="./image-slot.js"></script>
```

### ⚠️ "Favicon não aparece"
```bash
# Fazer upload de favicon.ico em public_html/
# E adicionar no HTML:
<link rel="icon" type="image/x-icon" href="/favicon.ico">
```

### ⚠️ "Página muito lenta"
1. Comprimir imagens: https://tinypng.com/
2. Verificar Gzip ativado
3. Remover inline CSS excessivo
4. Lazy load de imagens

---

## Passo 6: Monitoramento

### 6.1 Uptime Monitoring
Use serviço gratuito: https://uptimerobot.com/

### 6.2 Search Console
- Monitore erros de crawl
- Verifique impressões (quantas vezes aparece em buscas)
- Acompanhe CTR (Click-Through Rate)

### 6.3 Google Analytics
- Sessões por dia
- Sessões por dispositivo
- Cliques em CTA (configurar eventos)

---

## Passo 7: Tracking de Eventos (Opcional)

Adicionar no HTML para rastrear cliques:

```html
<!-- Em cada CTA de WhatsApp -->
<a href="{{ whatsappLink }}" onclick="gtag('event', 'whatsapp_click', {'location': 'hero'})">
  Agendar pelo WhatsApp
</a>
```

---

## Passo 8: Email & Suporte

### Configurar Email da Marca
cPanel → Email Accounts
```
contato@seu-dominio.com
info@seu-dominio.com
```

### Auto-resposta
cPanel → Email → Auto Responders

---

## Checklist Final de Deploy

```
PRÉ-DEPLOY:
- [ ] Renomear Trend_Hair.dc.html → index.html
- [ ] Adicionar todas as imagens em /assets/photos/
- [ ] Criar favicon.ico
- [ ] Adicionar meta tags SEO
- [ ] Testar localmente (python -m http.server)
- [ ] Validar HTML (W3C)
- [ ] Lighthouse score > 90 em todas categorias
- [ ] Testar links e CTA em mobile real

UPLOAD:
- [ ] Fazer upload via FTP ou File Manager
- [ ] Verificar permissões (644 para arquivos, 755 para pastas)
- [ ] Testar acesso pelo domínio

PÓS-DEPLOY:
- [ ] Ativar SSL/HTTPS
- [ ] Ativar Gzip compression
- [ ] Configurar cache headers
- [ ] Submeter sitemap ao Google Search Console
- [ ] Submeter ao Google Analytics
- [ ] Testar WhatsApp em smartphone real
- [ ] Monitorar com UptimeRobot

APRESENTAÇÃO:
- [ ] Demo em desktop
- [ ] Demo em mobile
- [ ] Testar todas as interações
- [ ] Mostrar velocidade de carregamento
- [ ] Confirmar numero WhatsApp ativo
```

---

## Dúvidas Frequentes

**P: Como faço backup?**
A: cPanel → Backup → Download backup completo (semanalmente)

**P: Como renovar SSL?**
A: Automático (Let's Encrypt renova a cada 90 dias)

**P: Posso modificar via cPanel depois?**
A: Sim, File Manager. Mas melhor fazer localmente e fazer upload.

**P: Domain apontando errado?**
A: Verificar DNS records em seu registrador (GoDaddy, etc)
Nameservers da Hostinger devem estar configurados.

---

**Tempo total estimado:** 3-4 horas
**Próximos passos após 1 semana:** Checar Search Console por indexação
