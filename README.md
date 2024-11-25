
# Documentação Técnica do Aplicativo
## Visão Geral
Este aplicativo será composto por duas telas distintas, cada uma dividida em componentes que se comunicam para fornecer uma experiência coesa ao usuário. A comunicação entre componentes será feita através de inputs, outputs e eventos, garantindo que a parametrização seja clara e fácil de implementar. A seguir, cada tela e seus respectivos componentes serão detalhados.

## Tela 1: Dashboard de Relatórios
### Componentes:
1. Componente: report-date-filter
Descrição: Um componente que permite ao usuário selecionar um intervalo de datas para filtrar relatórios. Exibe um calendário para escolha das datas.

### Inputs:
[startDate] - Tipo: Date - Data inicial do intervalo a ser mostrado no calendário.<br>
[endDate] - Tipo: Date - Data final do intervalo a ser mostrado no calendário.

### Outputs:
(onDateRangeSelect) - Tipo: EventEmitter<{startDate: Date, endDate: Date}> - Emite o intervalo de datas selecionado.

Exemplo de Uso:
````
<report-date-filter 
  [startDate]="selectedStartDate"
  [endDate]="selectedEndDate" 
  (onDateRangeSelect)="updateReportList($event)">
</report-date-filter>
````
#### Explicação do Exemplo:
O componente recebe selectedStartDate e selectedEndDate como intervalo inicial a ser mostrado.
Quando o usuário seleciona um intervalo de datas, o evento onDateRangeSelect é disparado, atualizando a lista de relatórios.

2. Componente: report-list
Descrição: Lista de relatórios filtrada pelo intervalo de datas selecionado.

Inputs:<br>
[reportData] - Tipo: Array<Report> - Lista de relatórios a serem exibidos.<br>
[loading] - Tipo: boolean - Define se a lista está carregando.

Outputs:
(onReportSelect) - Tipo: EventEmitter<Report> - Evento disparado ao selecionar um relatório.

Exemplo de Uso:
````
<report-list 
  [reportData]="filteredReports" 
  [loading]="isLoading" 
  (onReportSelect)="viewReportDetails($event)">
</report-list>
````
#### Explicação do Exemplo:
Recebe uma lista filteredReports para exibir.
Se isLoading for verdadeiro, a lista mostra um indicador de carregamento.
Quando um relatório é selecionado, o evento onReportSelect dispara para exibir os detalhes.

#### Comunicação Entre Componentes da Tela 1
O componente report-date-filter emite um intervalo de datas que é usado para filtrar a lista de relatórios no componente report-list.<br>
A comunicação acontece através do evento (onDateRangeSelect), que atualiza a propriedade filteredReports com base no intervalo recebido.


## Tela 2: Gerenciamento de Usuários
### Componentes:
1. Componente: user-form
Descrição: Formulário para criação ou edição de usuários. Permite que o administrador insira ou modifique dados de um usuário.

#### Inputs:
[userData] - Tipo: User - Dados do usuário que está sendo editado.

#### Outputs:
(onSave) - Tipo: EventEmitter<User> - Evento disparado quando o usuário clica em "Salvar".

Exemplo de Uso:
````
<user-form 
  [userData]="selectedUser" 
  (onSave)="saveUser($event)">
</user-form>
````

#### Explicação do Exemplo:
O componente recebe selectedUser como dados para edição.<br>
Quando o formulário é salvo, o evento onSave é disparado com os dados atualizados do usuário.

2. Componente: user-list
Descrição: Lista de usuários cadastrados no sistema, com opções para editar ou deletar.

##### Inputs:
[users] - Tipo: Array<User> - Lista de usuários a serem exibidos.<br>
[highlightedUser] - Tipo: User - Usuário atualmente selecionado, para destacar na lista.

####Outputs:
(onUserSelect) - Tipo: EventEmitter<User> - Evento disparado ao selecionar um usuário.<br>
(onUserDelete) - Tipo: EventEmitter<number> - Evento disparado ao deletar um usuário pelo seu ID.

Exemplo de Uso:
````
<user-list 
  [users]="userList" 
  [highlightedUser]="selectedUser" 
  (onUserSelect)="editUser($event)" 
  (onUserDelete)="removeUser($event)">
</user-list>
````

#### Explicação do Exemplo:
O componente recebe userList e destaca selectedUser na interface.<br>
Quando um usuário é selecionado para edição ou deleção, os eventos (onUserSelect) e (onUserDelete) são disparados respectivamente.<br>

#### Comunicação Entre Componentes da Tela 2
O componente user-list emite o evento (onUserSelect) quando um usuário é selecionado, enviando seus dados para o componente user-form para edição.
O componente user-form pode então emitir (onSave) para atualizar a lista de usuários com os dados editados.


Essa documentação detalha a especificação dos componentes e suas funcionalidades, permitindo que outros desenvolvedores implementem ou utilizem esses componentes.
