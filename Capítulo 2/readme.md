# Programação de Atualização
- Modelos de programas de atualização de cadastros e digitação de movimentos:

| Modelo                 | Utilidade                                                                                                                                                                                                                                                                             |
|------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Modelo 1 ou AxCadastro | Para cadastramentos em tela cheia                                                                                                                                                                                                                                                     |
| Modelo 2               | Cadastramentos envolvendo apenas uma tabela, mas com um cabeçalho e, opcionalmente, um rodapé e um corpo com quantidade ilimitada de linhas. Ideal para casos em que há dados que se repetem por vários itens e que, por isso, são colocados no cabeçalho. Exemplo: Pedido de Compra. |
| Modelo 3               | Cadastramentos envolvendo duas tabelas, um com dados de cabeçalho e outro digitado em linhas com os itens. Exemplo: Pedido de Vendas, Orçamento etc                                                                                                                                   |

## Modelo1() ou AxCadastro()
- Funcionalidade de cadastro simples;
- Poucas opções de customização;
- Composto de:
  - Browser padrão para visualização das informações da base de dados, de acordo com as configurações do SX3 – Dicionário de Dados (campo browser);
  - Funções de pesquisa, visualização, inclusão, alteração e exclusão padrões para visualização de registros simples, sem a opção de cabeçalho e itens.
- Sintaxe:
  - AxCadastro(cAlias, cTitulo, cVldExc, cVldAlt)

**Parâmetros**
| Variável | Descrição                                                                                        |
|----------|--------------------------------------------------------------------------------------------------|
| cAlias   | Alias padrão do sistema para utilização, o qual deve estar definido no dicionário de dados – SX3 |
| cTitulo  | Título da Janela                                                                                 |
| cVldExc  | Validação para Exclusão                                                                          |
| cVldAlt  | Validação para Alteração                                                                         |

**Função Cadastro**
```
#include "TOTVS.ch"
User Function XCadSA2()
  Local cAlias := "SA2"
  Local cTitulo := "Cadastro de Fornecedores"
  Local cVldExc := ".T."
  Local cVldAlt := ".T."

  dbSelectArea(cAlias)
  dbSetOrder(1)

  AxCadastro(cAlias,cTitulo,cVldExc,cVldAlt)

Return Nil
```

**Função de validação da alteração**
```
User Function VldAlt(cAlias,nReg,nOpc)

  Local lRet := .T.
  Local aArea := GetArea()
  Local nOpcao:= 0

  nOpcao := AxAltera(cAlias,nReg,nOpc)
  
  If nOpcao == 1
    MsgInfo(“Alteração concluída com sucesso!”)
  Endif

  RestArea(aArea)

Return lRet
```

**Função de validação da exclusão**
```
User Function VldExc(cAlias,nReg,nOpc)
  Local lRet := .T.
  Local aArea := GetArea()
  Local nOpcao := 0

  nOpcao := AxExclui(cAlias,nReg,nOpc)

  If nOpcao == 1
    MsgInfo(“Exclusão concluída com sucesso!”)
  Endif
  
  RestArea(aArea)
Return lRet
```

