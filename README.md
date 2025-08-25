##O Dia a Dia de um QA: A Prática de Testes Manuais Funcionais

Este projeto faz parte dos desafios práticos do Bootcamp WEX – End to End Engineering, uma iniciativa conjunta entre a WEX, empresa global de tecnologia fi nanceira, e a plataforma de ensino DIO (Digital Innovation One).Apresenta a implementação da funcionalidade de cupons de desconto para a plataforma SwagLabs Shopping, desenvolvido como parte de um desafio de projeto. A documentação incluída abrange todo o ciclo de desenvolvimento, desde o planejamento até a implementação e testes, seguindo metodologias ágeis e boas práticas de engenharia de software.

## Documentação do Projeto

Este repositório inclui a seguinte documentação:

- Plano de Fluxo de Trabalho: Desenvolvimento e ciclo de vida do bug conforme metodologia ágil
- User Stories: Mínimo de 2 User Stories pensadas e criadas em formato PDF
- Documentos de Teste:
  - Mind-map de pelo menos 1 User Story
  - 2 casos de teste utilizando técnica step-by-step
  - 2 casos de teste utilizando BDD (Behavior Driven Development)

## User Story Principal

Como um cliente da loja online  
Quero inserir um cupom de desconto na página de pagamento  
Para que eu possa obter desconto no valor total da minha compra e economizar dinheiro

### Valor de Negócio

A funcionalidade de cupom de desconto proporciona economia financeira para os clientes, melhoria na experiência de compra, aumento na conversão de vendas, fidelização de clientes e oferece uma ferramenta eficaz para campanhas promocionais.

## Funcionalidades Implementadas

### Interface do Usuário
- Campo de entrada "Cupom de Desconto" na página de checkout
- Botão "Aplicar" para validação do cupom
- Botão "Remover cupom" quando cupom estiver ativo
- Interface responsiva para dispositivos móveis
- Feedback visual durante processamento

### Validações e Regras de Negócio
- Validação em tempo real do cupom
- Verificação de validade temporal
- Controle de valor mínimo do pedido
- Verificação de elegibilidade dos produtos
- Prevenção de aplicação de múltiplos cupons
- Controle de limite de uso por cliente

### Experiência do Usuário
- Tempo de resposta inferior a 2 segundos
- Atualização de valores sem reload da página
- Mensagens de erro claras e específicas
- Manutenção do estado do formulário após erros

## Arquitetura Técnica

### Frontend
- Campo de entrada integrado à página de checkout existente
- Validação client-side para melhor experiência
- Interface responsiva e acessível

### Backend
- Endpoint /api/coupons/validate para validação de cupons
- API RESTful para gerenciamento de cupons
- Integração com sistema de pedidos

### Banco de Dados
- Tabela/coleção coupons com histórico de uso
- Vínculo com pedidos e controle de aplicação
- Armazenamento de dados de auditoria

## Estrutura de Dados

Cada aplicação de cupom contém:
- Código do cupom inserido
- Valor do desconto aplicado
- Tipo de desconto (percentual ou valor fixo)
- Data/hora da aplicação
- Status da validação ("válido", "inválido", "expirado")
- Valor original e final do pedido

## Critérios de Aceite

### Funcionalidades Principais
- Campo de cupom visível na página de pagamento
- Validação em tempo real de cupons
- Aplicação automática de desconto
- Exibição de resumo atualizado do pedido
- Mensagens de feedback apropriadas

### Validações de Erro
- "Cupom inválido ou expirado"
- "Cupom já foi utilizado"
- "Valor mínimo não atingido para este cupom"
- "Este cupom não se aplica aos produtos selecionados"

### Performance e Usabilidade
- Tempo de resposta menor que 2 segundos
- Interface responsiva
- Feedback visual durante processamento
- Manutenção de estado após erros

## Plataformas Suportadas

- Web: Navegadores modernos
- Mobile Web: Interface responsiva
- Ambientes: Desenvolvimento, QA e Produção

## Público-Alvo

- Usuários logados (clientes registrados)
- Visitantes (compradores anônimos)
- Qualquer pessoa realizando uma compra na plataforma

## Como Usar

1. Acesse a página de checkout/pagamento
2. Localize o campo "Cupom de Desconto"
3. Digite o código promocional
4. Clique em "Aplicar"
5. Verifique o desconto aplicado no resumo do pedido

## Métricas de Sucesso

- Aumento na taxa de conversão
- Melhoria na satisfação do cliente
- Incremento no valor médio dos pedidos
- Redução na taxa de abandono do carrinho

## Testes

Este projeto inclui uma suíte completa de testes:

### Testes Manuais
- Casos de teste step-by-step para fluxos principais
- Casos de teste BDD para comportamentos específicos
- Mind-map de cenários de teste

### Cenários de Teste Cobertos
- Aplicação de cupom válido
- Tentativa de uso de cupom inválido
- Remoção de cupom aplicado
- Validação de regras de negócio
- Testes de responsividade

## Status do Projeto

- Status: Em Desenvolvimento
- Prioridade: Média
- Projeto: SwagLabsShopping
- Responsável: A ser atribuído
- Data de Criação: Agosto/2025

---

**Bootcamp WEX - End to End Engineering - [DIO](https://web.dio.me/)**  
Desenvolvido por [Natalia Moraes](https://www.linkedin.com/in/moraesnatalia/)
