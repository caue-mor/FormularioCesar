# Formulário Energia Solar - César

Formulário de captação de leads para energia solar com integração Meta CAPI (Conversions API) e webhook.

## Características

- **Design responsivo** com gradiente azul → amarelo
- **Fluxo multi-etapas** progressivo
- **Validação condicional** (financiamento solicita CPF, data de nascimento e renda)
- **Integração Meta CAPI** para rastreamento de conversões
- **Webhook robusto** com 4 fallbacks (fetch → sendBeacon → form POST → pixel GET)
- **Seguro** com validações de idade (18+) e sanitização de dados

## Como fazer deploy no Vercel

### Opção 1: Via CLI (Recomendado)

1. Instale o Vercel CLI globalmente:
```bash
npm install -g vercel
```

2. Faça login no Vercel:
```bash
vercel login
```

3. Na pasta do projeto, execute:
```bash
vercel
```

4. Siga as instruções:
   - Set up and deploy? **Yes**
   - Which scope? (escolha sua conta)
   - Link to existing project? **No**
   - Project name? (pressione Enter ou escolha um nome)
   - In which directory is your code located? **./** (pressione Enter)

5. Para fazer deploy em produção:
```bash
vercel --prod
```

### Opção 2: Via Interface Web

1. Acesse [vercel.com](https://vercel.com)
2. Faça login com GitHub, GitLab ou Bitbucket
3. Clique em **"Add New Project"**
4. Importe o repositório ou faça upload dos arquivos
5. Configure:
   - **Framework Preset**: Other
   - **Build Command**: (deixe vazio)
   - **Output Directory**: (deixe vazio)
6. Clique em **"Deploy"**

### Opção 3: Deploy direto via GitHub

1. Crie um repositório no GitHub
2. Faça push dos arquivos:
```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/SEU-USUARIO/SEU-REPO.git
git push -u origin main
```

3. No Vercel:
   - Conecte sua conta GitHub
   - Selecione o repositório
   - Deploy automático

## Estrutura de arquivos

```
FormularioCesar/
├── index.html          # Página principal do formulário
├── vercel.json         # Configuração do Vercel
├── package.json        # Metadados do projeto
├── .gitignore          # Arquivos ignorados pelo Git
└── README.md           # Este arquivo
```

## Configurações importantes

### Webhook URL
O formulário envia dados para:
```
https://primary-production-4e12.up.railway.app/webhook/df1ce19a-e032-4dd7-aa9f-081d3820a33f
```

### Meta CAPI
- **Endpoint**: Graph API v24.0
- **Pixel ID**: 2727680507430142
- **Access Token**: Configurado no código (linha 439)
- **Evento**: Lead (CRM)

### Parâmetros UTM suportados
- `fbclid` - Facebook Click ID (automático)
- `lead_id` - ID do Lead Ads (automático)
- `test_event_code` - Para testes no Events Manager

## Teste local

Para testar localmente antes do deploy:

```bash
npx serve .
```

Acesse: http://localhost:3000

## Segurança

- ✅ Headers de segurança configurados (X-Content-Type-Options, X-Frame-Options, X-XSS-Protection)
- ✅ Sanitização de CPF (remove caracteres não numéricos)
- ✅ Validação de idade (18+)
- ✅ Hash SHA-256 de email e telefone para Meta CAPI
- ✅ Normalização de telefone (adiciona +55 automaticamente)

## Fallbacks de envio

O formulário tenta enviar os dados em ordem:

1. **Fetch API** (CORS habilitado)
2. **navigator.sendBeacon** (sem CORS)
3. **Form POST** via iframe oculto
4. **Pixel GET** via querystring

## Suporte

Para dúvidas ou problemas:
- Revise os logs do console do navegador
- Verifique o Events Manager do Facebook para eventos de teste
- Confirme se o webhook está respondendo corretamente

## Licença

MIT
