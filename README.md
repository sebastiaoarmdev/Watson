# Watson:

Sistema desktop para gestão de registros de sessões de terapia. Desenvolvido em Delphi, utiliza SQLite para armazenamento local dos dados. Projetado para otimizar o fluxo de trabalho de terapeutas e profissionais de saúde mental, oferecendo uma solução robusta e intuitiva para o gerenciamento de sessões, notas de pacientes e histórico de atendimentos.

---

## Requisitos:

### Requisitos Funcionais:

_Definem o que o Watson **precisa fazer**:_

* **Cadastro de Pacientes**: O sistema deve permitir o cadastro de pacientes com os seguintes campos: nome, data de nascimento, número de documento, telefone e e-mail.
* **Gestão de Prontuários de Sessão**: Deve ser possível criar, editar e armazenar prontuários para cada sessão. Cada prontuário deve conter a data, a hora de início e de término da sessão, além de um campo para anotações detalhadas.
* **Busca de Informações**: O sistema precisa oferecer funcionalidades de busca que permitam ao usuário:
    * Buscar prontuários por nome de paciente.
    * Buscar prontuários por data.
    * Realizar uma busca por palavra-chave no texto das anotações das sessões.

---

### Requisitos Não Funcionais:

_Definem o **quão bem** o Watson faz:_

* **Segurança e Confidencialidade**:
    * O sistema deve implementar níveis de acesso, restringindo o conteúdo clínico dos prontuários apenas ao psicólogo.
    * Deve-se considerar o uso de criptografia para proteger os dados de pacientes, tanto em trânsito quanto no armazenamento no arquivo SQLite, garantindo que mesmo que o arquivo seja acessado, ele não possa ser lido.
* **Integridade e Confiabilidade dos Dados**:
    * O sistema deve ter um sistema de backup automático.
    * Deve-se prever a sincronização automática dos dados após cada nova entrada, para minimizar o risco de perda de dados em caso de falha de hardware.
* **Desempenho**: O software deve ter um desempenho rápido nas operações de busca e manipulação de dados, mesmo com um histórico extenso de prontuários.

---

### Requisitos de Domínio do Negócio

_Garantem a conformidade do software com as normas profissionais:_

* **Conformidade Legal**: O sistema deve estar em total conformidade com a **Resolução CFP nº 01/2009**, que regulamenta o uso e a guarda de prontuários eletrônicos.
* **Guarda dos Prontuários**: O sistema deve garantir que os prontuários sejam mantidos e possam ser acessados por um período mínimo de **cinco anos**.
* **Controle de Acesso**: O acesso a informações confidenciais deve ser rigidamente controlado e limitado, respeitando a ética profissional.

---

## Análise e Modelagem:

Refino dos requisitos para que sejam claros, completos e consistentes (a gente transforma em casos de uso!).

### Atores do Sistema:

* **Psicólogo**: O único ator humano. É o usuário principal e administrador do próprio sistema, com acesso total a todas as funcionalidades e dados.
* **Sistema (ou Agente de Backup)**: O ator técnico, responsável por tarefas automáticas, como o backup.

---

### Casos de Uso do Psicólogo:

#### **1. Configurar Senha de Primeiro Acesso**

* **Objetivo**: Permitir que o psicólogo defina uma senha para proteger o acesso ao sistema na primeira vez que o aplicativo for executado.
* **Ator**: Psicólogo.
* **Fluxo Principal**:
    1.  O psicólogo abre o aplicativo pela primeira vez.
    2.  O sistema identifica que não há uma senha cadastrada e exibe uma tela de configuração.
    3.  O psicólogo digita e confirma a nova senha.
    4.  O sistema salva a senha e permite o acesso.

#### **2. Alterar Senha de Acesso**

* **Objetivo**: Permitir que o psicólogo altere a senha de acesso ao sistema a qualquer momento.
* **Ator**: Psicólogo.
* **Fluxo Principal**:
    1.  O psicólogo acessa a função de alteração de senha (dentro do menu, por exemplo).
    2.  O sistema exibe o formulário de alteração.
    3.  O psicólogo digita a senha atual e a nova senha, confirmando-a.
    4.  O sistema valida a senha atual e, se correta, atualiza a nova senha e informa o sucesso da operação.
* **Fluxo Alternativo**: Se a senha atual for digitada incorretamente, o sistema exibe uma mensagem de erro.

#### **3. Cadastrar Novo Paciente**

* **Objetivo**: Registrar as informações de um novo paciente no sistema.
* **Ator**: Psicólogo.
* **Fluxo Principal**:
    1.  **O psicólogo faz o login no sistema com sua senha.**
    2.  Acessa a função de cadastro de pacientes.
    3.  O sistema exibe um formulário.
    4.  O psicólogo preenche os campos obrigatórios: `Nome`, `Data de Nascimento`, `Documento`, `Telefone` e `E-mail`.
    5.  O psicólogo confirma o cadastro.
    6.  O sistema salva as informações, cria um registro de paciente e exibe uma mensagem de sucesso.
* **Fluxo Alternativo**: Se um campo obrigatório não for preenchido, o sistema deve exibir uma mensagem de erro.

#### **4. Registrar Sessão**

* **Objetivo**: Criar um novo prontuário para uma sessão de atendimento.
* **Ator**: Psicólogo.
* **Fluxo Principal**:
    1.  **O psicólogo está logado no sistema.**
    2.  Ele seleciona um paciente existente.
    3.  Inicia a criação de um novo prontuário.
    4.  O sistema preenche automaticamente a `Data` e a `Hora de Início`.
    5.  O psicólogo digita a `Hora de Término` e as `Notas da Sessão`.
    6.  Ele salva o prontuário.
    7.  O sistema armazena o prontuário associado ao paciente e exibe uma confirmação.

#### **5. Consultar Prontuários**

* **Objetivo**: Localizar e visualizar prontuários de pacientes.
* **Ator**: Psicólogo.
* **Fluxo Principal**:
    1.  **O psicólogo está logado no sistema.**
    2.  Ele insere os critérios de busca: nome do paciente, data ou palavras-chave das notas.
    3.  O sistema exibe uma lista de prontuários que correspondem aos critérios.
    4.  O psicólogo seleciona um prontuário para visualização completa.
* **Fluxo Alternativo**: Se nenhum resultado for encontrado, o sistema deve exibir uma mensagem informando.

#### **6. Editar Prontuário**

* **Objetivo**: Modificar o conteúdo de um prontuário de sessão.
* **Ator**: Psicólogo.
* **Fluxo Principal**:
    1.  **O psicólogo está logado no sistema.**
    2.  Ele consulta os prontuários e seleciona um para edição.
    3.  O sistema exibe o prontuário em modo de edição.
    4.  O psicólogo altera as `Notas da Sessão`.
    5.  Ele salva as alterações.
    6.  O sistema atualiza o registro do prontuário, com uma validação para garantir que o prontuário não seja modificado após um período determinado.

---

### Casos de Uso do Sistema:

_Esses casos de uso são automáticos._

* **Realizar Backup Automático**: Garante a segurança dos dados.
* **Garantir Conformidade Legal (Guarda de Prontuários)**: Assegura que os prontuários sejam mantidos pelo período mínimo de 5 anos exigido pela legislação.

