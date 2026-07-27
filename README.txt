AM TST — Site institucional
============================

ESTRUTURA DE ARQUIVOS (não altere os nomes/pastas):

  index.html          -> página principal do site
  assets/logo.png      -> logo usada no cabeçalho, hero, "quem somos" e rodapé

Os dois precisam ficar juntos, na mesma estrutura de pastas, onde
quer que você hospede o site.


COMO HOSPEDAR (opções mais simples, gratuitas)
------------------------------------------------

1) NETLIFY (o mais rápido, sem precisar mexer em código)
   - Acesse https://app.netlify.com/drop
   - Arraste a pasta "site-amtst" inteira (com index.html e assets/) para a
     área indicada.
   - Pronto: em segundos o Netlify gera um link público (ex:
     amtst.netlify.app). Depois é possível trocar para um domínio próprio
     (ex: amtst.com.br) nas configurações do site.

2) VERCEL
   - Acesse https://vercel.com > New Project > Deploy sem repositório
     (opção "Deploy without Git" / arraste a pasta).
   - Mesma lógica do Netlify.

3) GITHUB PAGES (gratuito, bom se já usa GitHub)
   - Crie um repositório novo (ex: amtst-site).
   - Suba os arquivos "index.html" e a pasta "assets" para a raiz do
     repositório.
   - Vá em Settings > Pages > Source: selecione a branch "main" e a pasta
     "/root".
   - O site fica disponível em https://SEUUSUARIO.github.io/amtst-site

4) HOSPEDAGEM TRADICIONAL (HostGator, Hostinger, Locaweb etc. — se for
   usar um domínio próprio tipo amtst.com.br)
   - Entre no painel de hospedagem (cPanel ou similar) > Gerenciador de
     Arquivos > pasta "public_html".
   - Envie o arquivo "index.html" e a pasta "assets" (com o logo.png
     dentro) para dentro de "public_html", mantendo a mesma estrutura.
   - Acesse o domínio no navegador para conferir.


DOMÍNIO PRÓPRIO
------------------------------------------------
Se quiser usar algo como "www.amtst.com.br":
 - Registre o domínio em um registrador (Registro.br, GoDaddy, Hostinger).
 - Aponte o domínio para o serviço de hospedagem escolhido (Netlify/
   Vercel/hospedagem tradicional) seguindo as instruções de DNS que cada
   um fornece na hora do deploy.


PERSONALIZAÇÕES FUTURAS
------------------------------------------------
 - Telefone, WhatsApp, e-mail e endereço já estão configurados com os
   dados reais (Três Lagoas/MS).
 - Os botões de WhatsApp já abrem uma conversa direta com o número
   (67) 99105-6313.
 - O formulário de orçamento ainda não envia e-mail de verdade — ele só
   mostra uma mensagem de confirmação na tela. Para receber os pedidos
   por e-mail é preciso ligar o formulário a um serviço como Formspree,
   Netlify Forms (gratuito e simples se hospedar no Netlify) ou um
   backend próprio. Posso configurar isso quando quiser.
