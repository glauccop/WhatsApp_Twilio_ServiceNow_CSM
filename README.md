# WhatsApp_Twilio_ServiceNow_CSM
Bot de Integração - WhatsApp - Twilio - ServiceNow - CSM Case

1) Importar o UpdateSet em sua instância ServiceNow
-- 1.1 - Importar o UpdateSet - Whatsapp_Twilio_Spoke_v2.xml 
---- O UpdateSet irá adicionar
---- Spoke WhatsApp_Twilio_v2 que será responsável por realizar o push back ServiceNow - Twilio - WhatsApp

-- 1.2 - Importar o UpdateSet - WhatsApp_Twilio_ServiceNow_CSM.xml 
---- O UpdateSet irá adicionar
---- Vai adicionar o channel WhatsApp no campo "contact_type"
---- Vai adicionar uma Business Rules chamada "Whatsapp_Assign_John_Jason" todo caso criado no canal whatsapp cai para o Jonh Jason (Agente CSM)
---- Vai adicionar o flow designer de push back ServiceNow Twilio "WhatsApp_Update" informando o usuário para as situações de "Awaiting Info", Resolved, Closed.


2) Passo - Criar uma conta no twilio - https://twilio.com 
-- Ao criar a conta o twilio te dá U$ 15 dólares de crédito.
-- Entre na Console Dashboard e anote o ACCOUNT_SID e o AUTH_TOKEN - iremos usar ele na integração reversa ServiceNow - Twilio - WhatsApp

3) Twilio - Abrir o aplicativo RUNTIME => Functions e criar um novo serviço chamado (Ex. servicenow)
-- Dentro da console do Functions, procure a engrenagem chamada "Dependencies"
-- Adicione as seguintes dependências:
MODULE: axios VERSION: 0.20.0
MODULE: os    VERSION: 0.1.1

-- Clique no botão "Add +" para adicionar uma nova função e adicione as seguintes funções.
/busca_feed_case
/update_case
/lista_case
/consulta_case
/valida_usuario_csm
/cria_case

-- Copie o conteúdo dos arquivos postados no git de mesmo nome e sobreescreva todo o conteúdo das funções.
-- Selecione o botão Deploy All e valide que não tenha nenhum erro de deploy.
-- Caso tenha - falar comigo glaucco.morais@servicenow.com

4) Twilio - Abrir o aplicativo RUNTIME => Studio
-- Crie um novo Flow chamado (Ex. twbot )
-- Importe o JSON Chamado ABACAXI
-- Abra o flow, reveja cada passo e para cada função, conecte-a a função correspondente.
---- Como fazer !.
---- clique no Widget Exemplo (</>valida_usuario_csm)
---- Na aba Config clique no campo "SERVICE"
---- Selecione o ENVIRONMENT = ui 
---- Selecione a função "/valida_usuario_csm""

---- REPITA ESSE PROCESSO PARA TODAS AS FUNÇÕES DO FLUXO QUE COMEÇEM COM "</>Função"

---- Clique em Publish

---- No Widget Inicial Chamado "Trigger" Clique em sua engrenagem e nas propriedades do Widget será apresentado o WEBHOOK URL - Copie ele !, pois iremos usalo para integrar o SandBox do WhatsApp com esse flow(bot)
