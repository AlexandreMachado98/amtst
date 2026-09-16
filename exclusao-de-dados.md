# Orientações de Exclusão de Dados, Conta e Desconexão de Serviços — GoField Pro

**Última Atualização:** 12 de Setembro de 2026  
**Versão do Aplicativo:** `3.0.0-native` (Namespace `com.gofield.pro`)  
**Titularidade:** AM TST SAÚDE E SEGURANÇA DO TRABALHO (CNPJ: `65.130.609/0001-20`)  
**Site Oficial:** [https://amtst.vercel.app](https://amtst.vercel.app)  

Este documento apresenta as instruções técnicas e os procedimentos operacionais para que o Usuário possa gerenciar, excluir dados, revogar permissões e desconectar serviços no **GoField Pro**, em cumprimento ao **Art. 18, VI da Lei Geral de Proteção de Dados (LGPD - Lei nº 13.709/2018)** e às **Políticas de Exclusão de Contas e Dados da Google Play Store**.

---

## 1. Princípio da Autonomia de Exclusão Local

Como o GoField Pro opera sob arquitetura **Offline-First**, a grande maioria das informações residem exclusivamente no armazenamento privado do seu smartphone. Por essa razão:
- **Você tem controle direto:** Não há necessidade de intermediários, aprovações de suporte ou espera em filas para excluir pontos, fotos, trilhas ou projetos.
- **A exclusão é imediata e irreversível:** Uma vez confirmada a exclusão no aplicativo, o registro é destruído do banco de dados SQLite/Room local.

---

## 2. Passo a Passo para Exclusão de Dados por Categoria

### 2.1. Exclusão de Waypoints, Coordenadas e Evidências Fotográficas
1. No menu principal do aplicativo, acesse **Waypoints** ou selecione o marcador no mapa.
2. Toque no ícone de **Lixeira (Excluir)**.
3. Confirme a exclusão no diálogo modal.
4. **Efeito:** O registro é removido da tabela `waypoints` / `evidences` e os arquivos de foto associados são apagados do armazenamento interno.

### 2.2. Exclusão de Trilhas de GPS e Caminhamentos
1. Na tela do mapa ativo, abra o painel **Trilhas**.
2. Selecione **Limpar Trilha Ativa** ou selecione a trilha salva e clique em **Excluir**.
3. **Efeito:** Os vértices de coordenadas acumulados daquela gravação são eliminados das preferências do mapa (`gofield_pdf_map_data`).

### 2.3. Exclusão de Plantas PDF e Calibrações GeoPDF
1. Acesse o menu **Plantas PDF**.
2. Toque nas opções da planta desejada e selecione **Excluir Planta**.
3. **Efeito:** O arquivo PDF original, as matrizes afins/UTM de georreferenciamento e as imagens rasterizadas geradas em alta resolução são apagados permanentemente do diretório `/files/maps/`.

### 2.4. Exclusão de Regiões de Mapas Baixados para Uso Offline
1. Acesse **Mapas Offline** no menu lateral.
2. Localize a região baixada e toque em **Excluir Região**.
3. **Efeito:** Todos os arquivos de mosaico de satélite/relevo (`.png`) daquela área são excluídos da memória interna, liberando imediatamente o espaço em disco do smartphone.

### 2.5. Exclusão de Dados Cadastrais e Avatar do Perfil
1. Acesse a tela de **Perfil**.
2. Para remover a foto: toque sobre a imagem e selecione **Remover Avatar**.
3. Para limpar os dados pessoais: apague os campos de texto (Nome, Empresa, Telefone, E-mail) e clique em **Salvar Perfil**.
4. **Efeito:** As preferências locais (`gofield_user_profile`) são sobrescritas com valores vazios e o arquivo de imagem do avatar é deletado do disco.

---

## 3. Desconexão de Contas e Exclusão em Nuvem (Firebase / Google)

Caso você tenha realizado login voluntário para sincronização:

### 3.1. Desconexão Imediata no Aplicativo
1. Vá até o menu **Perfil** ou **Sincronização**.
2. Clique no botão **Desconectar Conta / Sair**.
3. **Efeito:** A sessão é encerrada, o aplicativo retorna ao modo Usuário Local e os identificadores remotos são excluídos das preferências do app. Seus dados locais são mantidos intactos.

### 3.2. Solicitação de Exclusão de Registros em Servidores de Nuvem
Caso queira a eliminação de dados que tenham sido previamente sincronizados para a nuvem Firebase:
1. Envie uma mensagem para o Encarregado de Dados:
   - **E-mail Oficial:** `apoioamtst@gmail.com`
   - **Assunto:** `Exclusão de Dados de Nuvem — GoField Pro`
   - **Identificação:** Informe o e-mail cadastrado na autenticação.
2. **Prazo de Atendimento:** A confirmação da eliminação definitiva nos bancos remotos e cópias de segurança será comunicada em até **15 (quinze) dias**, em observância ao Art. 19 da LGPD.

---

## 4. Exclusão Total Instantânea via Sistema Operacional Android

Caso queira eliminar absolutamente todos os dados, projetos, configurações e caches do aplicativo de uma única vez:

### Opção A: Limpar Armazenamento
1. Acesse as **Configurações** do Android > **Aplicativos** > **GoField Pro**.
2. Toque em **Armazenamento e Cache**.
3. Toque em **Limpar Dados** (ou *Limpar Armazenamento*) e confirme.
4. **Efeito:** Todo o banco de dados, preferências e arquivos locais são zerados para o estado de fábrica.

### Opção B: Desinstalação do Aplicativo
1. Mantenha pressionado o ícone do **GoField Pro** na tela inicial e toque em **Desinstalar**.
2. **Efeito:** O sistema operacional Android apaga integralmente a pasta privada do aplicativo (`/data/user/0/com.gofield.pro/`).

---

## 5. Como Excluir ou Gerenciar Backups do Android OS (Google Drive)

O backup automático do sistema operacional Android é gerenciado diretamente pela sua conta Google:
1. Acesse as **Configurações do Android** > **Google** > **Backup**.
2. Selecione **Gerenciar Backup** > **Dados dos Apps**.
3. Localize o **GoField Pro** e escolha **Excluir Backup do Google Drive**.

---

## 6. Como Revogar Permissões de Sistema

Você pode revogar permissões concedidas a qualquer momento:
1. Acesse **Configurações > Aplicativos > GoField Pro > Permissões**.
2. Altere as permissões de **Localização**, **Câmera** ou **Notificações** para **"Não permitir"**.

---

## 7. Canal de Suporte e Privacidade

Em caso de dúvidas ou solicitações sobre exclusão de dados:

* **Titular:** AM TST SAÚDE E SEGURANÇA DO TRABALHO
* **CNPJ:** `65.130.609/0001-20`
* **Site Oficial:** [https://amtst.vercel.app](https://amtst.vercel.app)
* **E-mail de Contato / DPO:** `apoioamtst@gmail.com`
* **Atendimento:** Exclusivamente eletrônico via e-mail oficial
