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
