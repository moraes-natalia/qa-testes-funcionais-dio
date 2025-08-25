# Casos de Teste BDD - Sistema de Cupons de Desconto

## Funcionalidade: Sistema de Cupons de Desconto SwagLabs

### Caso de Teste BDD 1: Aplicação Bem-Sucedida de Cupom Válido

**ID do Teste:** BDD-CUPOM-001  
**Objetivo:** Validar o comportamento completo da aplicação de cupom válido  
**Prioridade:** Alta  
**Tipo:** Comportamental  

#### Cenário: Cliente aplica cupom de desconto válido no checkout

```gherkin
Funcionalidade: Aplicação de cupom de desconto
    Como um cliente da loja online
    Quero aplicar um cupom de desconto no checkout
    Para que eu possa economizar dinheiro na minha compra

Contexto:
    Dado que estou na página de checkout do SwagLabs
    E possuo produtos no carrinho no valor de R$ 100,00
    E o sistema está funcionando normalmente

Cenário: Aplicar cupom válido com desconto percentual
    Dado que estou na seção de pagamento
    E o campo "Cupom de Desconto" está visível
    E o cupom "DESCONTO10" está ativo no sistema
    E oferece 10% de desconto sem valor mínimo
    
    Quando eu digito "DESCONTO10" no campo de cupom
    E clico no botão "Aplicar"
    
    Então o sistema deve processar a validação em menos de 2 segundos
    E a mensagem "Cupom aplicado com sucesso!" deve ser exibida
    E o resumo do pedido deve mostrar:
        | Campo                | Valor      |
        | Subtotal            | R$ 100,00  |
        | Desconto (DESCONTO10)| -R$ 10,00  |
        | Total Final         | R$ 90,00   |
    E o botão "Remover cupom" deve ficar visível
    E o campo de cupom deve ficar desabilitado
    E a interface deve permanecer responsiva
```

**Critérios de Aceitação:**
- O cupom deve ser validado em tempo real
- A mensagem de sucesso deve aparecer imediatamente após validação
- Os valores devem ser recalculados automaticamente
- A funcionalidade de remoção deve estar disponível
- O estado da página deve ser preservado

---

### Caso de Teste BDD 2: Tratamento de Múltiplos Cenários de Erro

**ID do Teste:** BDD-CUPOM-002  
**Objetivo:** Validar o comportamento do sistema em diferentes cenários de erro  
**Prioridade:** Alta  
**Tipo:** Comportamental Negativo  

#### Cenários: Cliente tenta aplicar cupons com diferentes tipos de problemas

```gherkin
Funcionalidade: Validação de cupons inválidos
    Como um cliente da loja online
    Quero receber feedback claro quando um cupom não pode ser aplicado
    Para que eu entenda o motivo e possa tentar novamente com informações corretas

Contexto:
    Dado que estou na página de checkout do SwagLabs
    E possuo produtos no carrinho
    E o sistema está funcionando normalmente
    E o campo "Cupom de Desconto" está disponível

Esquema do Cenário: Aplicar cupons inválidos com diferentes problemas
    Dado que meu carrinho possui o valor de <valor_carrinho>
    Quando eu digito "<codigo_cupom>" no campo de cupom
    E clico no botão "Aplicar"
    Então o sistema deve processar em menos de 2 segundos
    E a mensagem "<mensagem_erro>" deve ser exibida
    E o valor total deve permanecer <valor_final>
    E o campo de cupom deve permanecer disponível para nova tentativa
    E nenhum desconto deve ser aplicado ao resumo
    E o botão "Remover cupom" não deve estar visível

Exemplos:
    | codigo_cupom        | valor_carrinho | mensagem_erro                                  | valor_final |
    | CUPOM_INEXISTENTE   | R$ 100,00     | "Cupom inválido ou expirado"                 | R$ 100,00  |
    | CUPOM_EXPIRADO      | R$ 100,00     | "Cupom inválido ou expirado"                 | R$ 100,00  |
    | DESCONTO20          | R$ 80,00      | "Valor mínimo não atingido para este cupom"  | R$ 80,00   |
    | CUPOM_USADO         | R$ 150,00     | "Cupom já foi utilizado"                     | R$ 150,00  |
    | CATEGORIA_ESPECIFICA| R$ 200,00     | "Este cupom não se aplica aos produtos selecionados" | R$ 200,00 |

Cenário: Tentativa de aplicar múltiplos cupons simultaneamente
    Dado que já apliquei o cupom "DESCONTO10" com sucesso
    E o desconto de R$ 10,00 está aplicado
    E o botão "Remover cupom" está visível
    
    Quando eu tento digitar um novo código "DESCONTO20" no campo de cupom
    Então o campo deve estar desabilitado
    E uma mensagem informativa deve aparecer: "Remova o cupom atual para aplicar outro"
    E os valores já aplicados devem ser mantidos
    
    Quando eu clico em "Remover cupom"
    Então o desconto deve ser removido
    E o campo de cupom deve ficar disponível novamente
    E o total deve retornar ao valor original
    E posso aplicar um novo cupom

Cenário: Recuperação após erro de conexão durante validação
    Dado que estou tentando aplicar o cupom "DESCONTO10"
    Quando eu clico em "Aplicar"
    E ocorre um erro de conexão durante a validação
    
    Então uma mensagem deve aparecer: "Erro de conexão. Tente novamente."
    E o campo deve permanecer preenchido com "DESCONTO10"
    E o botão "Aplicar" deve continuar disponível
    E posso tentar novamente sem perder os dados inseridos
    
    Quando a conexão é restabelecida
    E eu clico novamente em "Aplicar"
    Então o cupom deve ser validado normalmente
```

**Critérios de Aceitação:**
- Todas as mensagens de erro devem ser específicas e claras
- O estado do formulário deve ser preservado após erros
- O sistema deve permitir novas tentativas sem reload da página
- Apenas um cupom pode ser aplicado por vez
- A funcionalidade de remoção deve funcionar corretamente
- Erros de conectividade devem ser tratados adequadamente

**Configuração do Ambiente:**
- **Navegadores:** Chrome, Firefox, Edge (versões atuais)
- **Ambientes:** Desenvolvimento, QA, Produção
- **Dados de Teste:** Conforme especificado nos exemplos do esquema de cenário

**Automação:**
Estes cenários BDD podem ser automatizados utilizando ferramentas como:
- Cucumber + Selenium WebDriver
- Playwright + Cucumber
- Cypress com cucumber-preprocessor