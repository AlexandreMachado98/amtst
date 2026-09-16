# Política de Privacidade — GoField Pro

**Última Atualização:** 12 de Setembro de 2026  
**Versão do Aplicativo:** `3.0.0-native` (Namespace `com.gofield.pro`)  
**Entidade Responsável:** AM TST SAÚDE E SEGURANÇA DO TRABALHO (CNPJ: `65.130.609/0001-20`)  
**Site Oficial:** [https://amtst.vercel.app](https://amtst.vercel.app)  

Esta Política de Privacidade tem o objetivo de esclarecer com total transparência e rigor técnico como o aplicativo **GoField Pro** (doravante "Aplicativo"), de titularidade de **AM TST SAÚDE E SEGURANÇA DO TRABALHO**, inscrita no CNPJ sob o nº **65.130.609/0001-20** (doravante "Controlador"), realiza o tratamento de dados pessoais e operacionais, em conformidade com a **Lei Geral de Proteção de Dados Pessoais (LGPD - Lei nº 13.709/2018)** e as **Políticas de Dados do Desenvolvedor da Google Play**.

---

## 1. Diretriz sobre Armazenamento, Custódia e Aplicação da LGPD

### 1.1. Tratamento Local e Aplicação da LGPD
* O GoField Pro permite a utilização completa de suas ferramentas sem exigir a criação obrigatória de conta ou login.
* **O login opcional NÃO torna os dados anônimos e NÃO afasta a aplicação da LGPD:** O tratamento de informações de pessoas identificadas ou identificáveis (tais como coordenadas geográficas precisas, registros fotográficos de propriedades, trilhas de deslocamento e dados cadastrais de perfil) constitui tratamento de dados pessoais sujeito às normas de segurança, finalidade, adequação e transparência da LGPD (Arts. 5º e 46).

### 1.2. Ausência de Servidores Próprios de Hospedagem
* O Controlador **NÃO mantém servidores próprios** para recepção, custódia, telemetria contínua ou armazenamento centralizado dos projetos, bancos de dados e medições gerados no Aplicativo.
* O Controlador **NÃO tem acesso remoto**, não visualiza e não possui cópia dos arquivos, waypoints, plantas PDF ou polígonos salvos na memória do seu aparelho.

---

## 2. Diferenciação das Camadas de Armazenamento e Compartilhamento

Para que você compreenda com exatidão onde suas informações residem e quem as gerencia, distinguimos quatro esferas:

### 2.1. Arquivos e Bancos de Dados Locais (No Aparelho)
* **Onde ficam:** No contêiner de armazenamento privado do Aplicativo (`/data/user/0/com.gofield.pro/`), protegido pela sandbox de segurança do sistema operacional Android.
* **O que contêm:** Banco de dados SQLite/Room (pontos georreferenciados, evidências, cubagens de madeira, ocorrências, histórico de percursos), preferências do usuário (nome, cargo, empresa, formato de coordenadas), imagens em alta resolução de plantas PDF calibradas e blocos de mapas baixados para uso offline.
* **Administração:** O Usuário administra diretamente o acesso físico ao seu smartphone, os arquivos que decide importar e o histórico salvo.

### 2.2. Backups Automáticos do Sistema Operacional Android (Nuvem Google do Usuário)
* **Como funciona:** O Aplicativo está configurado de acordo com os padrões técnicos do Android (`android:allowBackup="true"`, conforme regras de extração de dados). Isso permite que o serviço nativo de **Backup na Nuvem do Android (Google Backup / Google Drive)** copie periodicamente o banco de dados e preferências para a conta Google pessoal vinculada ao aparelho pelo próprio Usuário.
* **Responsabilidade:** Esse backup é transmitido diretamente entre o dispositivo do Usuário e a infraestrutura de nuvem da Google LLC. O Controlador do GoField Pro não intermedia, não hospeda e não tem acesso às chaves ou aos arquivos desse backup do sistema operacional.

### 2.3. Exportações e Compartilhamentos Externos (Disparados pelo Usuário)
* **Como funciona:** O Usuário pode, a seu exclusivo critério, exportar relatórios técnicos (PDF/CSV) ou camadas vetoriais (KML/KMZ) e compartilhá-los via e-mail, WhatsApp, Google Drive ou outros aplicativos instalados.
* **Responsabilidade:** O Usuário é o único responsável pela seleção dos destinatários e pelos canais externos escolhidos para transmissão de seus relatórios e arquivos.

### 2.4. Sincronização em Nuvem Firebase (Opcional)
* **Como funciona:** Caso o Usuário decida voluntariamente conectar uma conta online e utilizar a tela de sincronização, os dados de waypoints e evidências selecionados serão sincronizados via Google Firebase utilizando conexões criptografadas (HTTPS/TLS).

---

## 3. Dados Pessoais e Operacionais Tratados

| Categoria de Dado | Descrição Técnica | Finalidade Específica | Base Legal (LGPD) |
| :--- | :--- | :--- | :--- |
| **Geolocalização de Alta Precisão** | Coordenadas GNSS (lat, lng, alt, velocidade, acurácia). | Demarcação de vértices, cálculo de áreas e perímetros, navegação e plotagem sobre plantas PDF. | Art. 7º, V (Execução de Contrato) |
| **Geolocalização em 2º Plano** | Coleta contínua de satélite com tela desligada durante gravação ativa. | Gravação contínua do percurso percorrido em campo pelo operador sem interrupções. | Art. 7º, I (Consentimento) e Art. 7º, V |
| **Fotografias e Câmera** | Fotos capturadas no aplicativo ou anexadas da galeria. | Registro de evidências visuais de vistorias técnicas, ocorrências florestais e avatar. | Art. 7º, V (Execução de Contrato) |
| **Identificação do Operador** | Nome, empresa, cargo, e-mail, telefone (opcionais). | Preenchimento automático do cabeçalho de responsabilidade nos laudos técnicos de campo. | Art. 7º, V (Execução de Contrato) |
| **Arquivos Geoespaciais** | Arquivos KML, KMZ e plantas GeoPDF importados. | Leitura cartográfica e sobreposição vetorial na área de trabalho. | Art. 7º, V (Execução de Contrato) |

---

## 4. Comunicações com Serviços de Terceiros e Provedores de Mapas

O Aplicativo estabelece conexões de rede exclusivamente para as seguintes finalidades operacionais:

1. **OpenStreetMap Foundation e OpenTopoMap:**
   - **Operação:** O Aplicativo envia requisições HTTP GET puras para baixar imagens de quadrículas cartográficas públicas (tiles) para visualização em tela e armazenamento de mapas offline (raio de até 150 km).
   - **Dados transmitidos:** Endereço IP do dispositivo (inerente à comunicação na internet), coordenadas de zoom/quadrícula e cabeçalho `User-Agent: GoFieldPro/3.0.0`.
   - **Não envio:** Nenhum dado pessoal do usuário (nome, e-mail, pontos marcados ou projetos) é transmitido aos servidores de tiles do OpenStreetMap ou OpenTopoMap.
2. **Google Maps SDK (Google LLC):**
   - **Operação:** Carregamento de camadas de satélite e terrenos. A comunicação técnica ocorre diretamente entre o SDK e os servidores da Google, regida pela [Política de Privacidade do Google](https://policies.google.com/privacy).
3. **Ausência de Rastreamento Publicitário:**
   - O Aplicativo **não utiliza** SDKs de corretores de dados (*data brokers*), redes de anúncios (AdMob, Facebook Audience Network) ou rastreadores comportamentais de terceiros.

---

## 5. Riscos Reais de Perda de Dados e Limites de Recuperação

> [!IMPORTANT]
> **AVISO CRÍTICO SOBRE A GUARDA DE DADOS LOCAIS:**
> Como o Controlador **não armazena seus dados em servidores próprios**, a segurança física e digital das informações locais depende do Usuário.

* **Desinstalação do Aplicativo:** A desinstalação do GoField Pro no Android faz com que o sistema operacional apague permanentemente o diretório privado do aplicativo.
* **Limpeza de Armazenamento / "Limpar Dados":** A limpeza manual do armazenamento do app nas configurações do Android apaga de forma definitiva o banco de dados e as plantas locais.
* **Perda, Roubo, Dano Físico ou Formatação do Aparelho:** Caso o aparelho seja danificado ou formatado sem que o Usuário tenha realizado exportações prévias ou mantido o Backup do Android ativo, os dados locais serão irrecuperáveis.
* **Impossibilidade de Recuperação pelo Fornecedor:** O Controlador **NÃO tem como recuperar arquivos, medições ou waypoints perdidos**, pois jamais teve a custódia ou posse dessas informações. Recomendamos fortemente a exportação periódica de seus projetos importantes (KML/KMZ/PDF/CSV).

---

## 6. Segurança da Informação (LGPD — Art. 46)

O Controlador adota medidas técnicas e administrativas compatíveis com a arquitetura local para proteger os dados tratados:
- Isolamento por *Application Sandbox* no sistema operacional Android.
- Compartilhamento restrito e seguro de arquivos via `androidx.core.content.FileProvider`.
- Transmissão criptografada (HTTPS com TLS moderno) em todas as requisições de rede (download de tiles e sincronização voluntária).

---

## 7. Direitos dos Titulares de Dados (LGPD — Art. 18)

O Usuário pode exercer plenamente seus direitos de titular de dados:
- **Acesso e Confirmação:** Consulta direta de todos os seus dados a qualquer momento no Aplicativo.
- **Retificação:** Edição imediata de qualquer coordenada, nota técnica ou informação de perfil.
- **Eliminação:** Exclusão autônoma e instantânea de qualquer ponto, trilha, planta PDF ou pacote offline diretamente nas opções da interface.
- **Portabilidade:** Exportação de dados em formatos abertos e estruturados (KML, KMZ, PDF e CSV).
- **Revogação de Permissões:** O Usuário pode revogar a qualquer momento o acesso à Localização, Câmera ou Notificações nas configurações de aplicativos do Android.

---

## 8. Canal de Contato e Encarregado de Proteção de Dados (DPO)

Para dúvidas sobre esta Política, solicitações ou comunicações referentes à LGPD:

* **Controlador:** AM TST SAÚDE E SEGURANÇA DO TRABALHO
* **CNPJ:** `65.130.609/0001-20`
* **Site Oficial:** [https://amtst.vercel.app](https://amtst.vercel.app)
* **E-mail de Contato / DPO / Suporte:** `apoioamtst@gmail.com`
* **Atendimento:** Exclusivamente eletrônico via e-mail oficial
