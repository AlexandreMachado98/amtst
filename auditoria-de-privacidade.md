# Relatório de Auditoria Forense de Privacidade e Segurança — GoField Pro

**Data da Auditoria:** 12 de Setembro de 2026  
**Versão Auditada:** `3.0.0-native` (Build Code `1`, Namespace `com.gofield.pro`)  
**Titular dos Direitos / Desenvolvedor:** AM TST SAÚDE E SEGURANÇA DO TRABALHO  
**CNPJ Responsável:** `65.130.609/0001-20`  
**Site Oficial:** [https://amtst.vercel.app](https://amtst.vercel.app)  
**E-mail de Contato Técnico / DPO:** `apoioamtst@gmail.com`  
**Público-Alvo:** Equipe de Engenharia, Encarregado de Proteção de Dados (DPO) e Revisores Jurídicos  
**Marco Legal de Referência:** LGPD (Lei nº 13.709/2018, esp. Arts. 5º, 7º, 18, 46 e 50), Diretrizes da ANPD e Políticas de Dados do Desenvolvedor da Google Play.

---

## 1. Sumário Executivo e Enquadramento Regulatório

O **GoField Pro** opera como uma ferramenta técnica móvel voltada para engenharia agronômica, inventário florestal, topografia, geoprocessamento e gestão de ocorrências em áreas rurais e remotas.

### 1.1. Tratamento de Dados sob a LGPD (Art. 5º, X)
Diferentemente de declarações genéricas de "não coleta de dados", a presente auditoria constata que **o GoField Pro realiza operações de tratamento de dados pessoais** (como coleta, processamento, cálculo, armazenamento local, modificação e exportação de coordenadas geográficas de alta precisão, registros fotográficos e dados de identificação técnica do operador).
* **Identificabilidade (Art. 5º, I):** Mesmo sem login obrigatório, dados de geolocalização contínua (trilhas GPS), fotos de evidências de campo e dados de perfil local (nome, cargo, empresa, e-mail) constituem dados de pessoas naturais identificadas ou identificáveis.
* **Inaplicabilidade da tese de "anonimato por ausência de login":** O fato de o aplicativo possibilitar o uso no modo local sem cadastro prévio **não torna os dados anônimos** e **não afasta a incidência da LGPD**. As obrigações de segurança, transparência e respeito aos direitos dos titulares incidem sobre o software e seu controlador.

---

## 2. Mapa de Evidências Técnicas do Código-Fonte

### 2.1. Arquitetura de Armazenamento e Limites de Custódia

1. **Inexistência de Servidor Central Próprio do Desenvolvedor:**
   - O desenvolvedor **não mantém servidores proprietários** para recepção, armazenamento centralizado, espelhamento de banco de dados ou telemetria dos projetos criados no aplicativo.
   - O desenvolvedor **não tem acesso remoto** aos waypoints, fotos, polígonos, relatórios ou dados do perfil salvos no aparelho do usuário.
2. **Armazenamento Privado Local (Sandbox):**
   - Todos os dados operacionais residem no diretório `/data/user/0/com.gofield.pro/`, isolado por permissões de usuário Linux no Android.
3. **Mecanismos de Backup do Sistema Operacional Android:**
   - O manifesto declara `android:allowBackup="true"`.
   - Conforme mapeado em `backup_rules.xml` e `data_extraction_rules.xml`, o banco de dados Room e as preferências locais estão habilitados para o serviço nativo de **Backup na Nuvem do Android (Google Backup)** vinculado à conta Google configurada pelo próprio usuário no smartphone.
   - Esse backup é de responsabilidade e custódia da Google e do próprio titular do aparelho, não transitando por servidores do desenvolvedor do GoField Pro.

---

### 2.2. Permissões de Sistema e Justificativas Técnicas

| Permissão | Nível | Finalidade Técnica Auditada | Evidência no Código |
| :--- | :--- | :--- | :--- |
| `ACCESS_FINE_LOCATION` | Sensível | Coleta de coordenadas GNSS de alta precisão para cálculo de área, perímetro e pontos. | `LocationTrackingService.kt:360-398` |
| `ACCESS_COARSE_LOCATION` | Sensível | Obtenção de posição aproximada enquanto o receptor GNSS estabiliza o fix de satélite. | `LocationTrackingService.kt:360-398` |
| `ACCESS_BACKGROUND_LOCATION` | Sensível | Continuidade da gravação de trilhas em campo com tela bloqueada ou app em segundo plano. | `LocationTrackingService.kt:122-127` |
| `FOREGROUND_SERVICE_LOCATION` | Especial | Manutenção do serviço com notificação persistente na barra de status durante gravação ativa. | `LocationTrackingService.kt:346-357` |
| `POST_NOTIFICATIONS` | Runtime | Notificação contínua de status da missão (quilometragem, tempo decorrido e qualidade do sinal). | `LocationTrackingService.kt:400-439` |
| `CAMERA` | Sensível | Registro de fotos de evidência em pontos de vistoria e imagem de perfil do operador. | `provider_paths.xml` |
| `WAKE_LOCK` | Normal | Prevenção contra corte de energia da CPU pelo sistema operacional durante rastreamento de campo. | `LocationTrackingService.kt:205-230` |
| `INTERNET` / `ACCESS_NETWORK_STATE` | Normal | Requisições HTTP para download de mosaicos de mapa (tiles) e sincronização opcional. | `OfflineTileDownloader.kt:210-241` |

---

### 2.3. Tráfego de Rede e Destinatários Externos

1. **Servidores de Tiles Abertos (OpenStreetMap / OpenTopoMap):**
   - **O que é enviado:** Requisição HTTP GET para download de imagens de quadrículas (`https://tile.openstreetmap.org/{z}/{x}/{y}.png`), contendo o cabeçalho `User-Agent: GoFieldPro/3.0.0` e o endereço IP do dispositivo.
   - **O que NÃO é enviado:** Nenhum identificador pessoal, e-mail, coordenadas de waypoints privados ou traçados vetoriais do usuário.
2. **Google Maps SDK (Google LLC):**
   - **O que é enviado:** Requisições de imagens de satélite e dados de telemetria técnica de renderização regidos pelos termos e infraestrutura do Google Play Services.
3. **Autenticação e Nuvem Firebase (Opcional):**
   - **Comportamento:** Apenas ativado se o usuário realizar login voluntário e acionar a sincronização em nuvem. No uso padrão sem login, nenhuma informação é transmitida ao Firebase.
4. **Google Drive / Aplicativos Externos via Intents:**
   - **Comportamento:** Integração restrita ao recebimento e envio de arquivos através do framework de compartilhamento do Android (`KmlImportDispatchActivity.kt`). Não há sincronização invisível em background.

---

## 3. Delimitação Técnica de Responsabilidades e Riscos

### 3.1. Riscos de Perda de Dados e Guarda
Como o desenvolvedor não armazena cópia dos dados dos projetos em servidor próprio:
- **Desinstalação do Aplicativo:** O Android apaga todo o diretório privado (`filesDir` e bancos Room). Se o usuário não tiver gerado exportações (KML, KMZ, PDF, CSV) ou se o backup do Android estiver inativo, **os dados serão permanentemente perdidos**.
- **Limpeza de Armazenamento / Formatação / Perda do Aparelho:** O desenvolvedor não possui capacidade técnica de restaurar dados que jamais recebeu ou custodiou.
- **Dever de Diligência do Usuário:** O usuário é responsável por gerenciar o controle físico do aparelho, a rotina de exportação dos seus levantamentos e as permissões de acesso ao dispositivo.

### 3.2. Responsabilidade do Desenvolvedor (Art. 46 da LGPD)
O desenvolvedor responde pela segurança da aplicação, pela correta implementação das regras de sandbox, pela transparência das operações de tratamento, pela ausência de código malicioso ou vazamentos ocultos e pela conformidade com as diretrizes da Google Play.

---

## 4. Tabela de Segurança de Dados da Google Play (Data Safety Reference)

| Categoria da Google Play | Dado Coletado | Finalidade Primária | Compartilhado com Terceiros? | Criptografia em Trânsito | Solicitação de Exclusão |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Localização** | Localização precisa e em 2º plano | Demarcação cartográfica e gravação de trilhas | Não compartilhado com terceiros | Sim (se sincronizado via TLS) | Exclusão local instantânea |
| **Informações Pessoais** | Nome, E-mail, Telefone, Empresa (opcional) | Identificação em relatórios técnicos locais | Não compartilhado com terceiros | Sim (se sincronizado) | Exclusão local instantânea |
| **Fotos e Vídeos** | Fotos da Câmera / Galeria | Evidências fotográficas de campo e avatar | Não compartilhado com terceiros | Sim (se sincronizado) | Exclusão local instantânea |
| **Arquivos e Documentos** | Arquivos KML/KMZ, GeoPDF, Relatórios | Gestão e visualização de projetos de campo | Não compartilhado | N/A (processamento local) | Exclusão local instantânea |

---

## 5. Dados Cadastrais e de Contato

* **Titular dos Direitos:** AM TST SAÚDE E SEGURANÇA DO TRABALHO
* **CNPJ:** `65.130.609/0001-20`
* **Site Oficial:** [https://amtst.vercel.app](https://amtst.vercel.app)
* **Canal Oficial de Atendimento / DPO:** `apoioamtst@gmail.com`
* **Atendimento:** Exclusivamente eletrônico via e-mail oficial
