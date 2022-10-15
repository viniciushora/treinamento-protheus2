# Transações
- Controle de concorrência;
- Garante que as transações sejam seguras;
- Integridade stuff;
- Transações em concorrência devem ter o msm processamento que realizadas em serial.

## Begin Transaction / End Transaction
- Transações são unidades lógicas;
- Inicia um bloco de transação;
- Em caso de falha: operações do bloco serão integralmente desfeitas.
```
BEGIN TRANSACTION 
RecLock("SB2”) 
... 
MsUnLock()
END TRANSACTION
```

### BeginTran
- Inicia transação que pode ser terminada em meio a uma condicional com o EndTran()

```
AADD(xAutoCab,{“A1_FILIAL”,xFilial(“SA1”) , Nil})
AADD(xAutoCab,{“A1_COD” , “000001” , Nil})
AADD(xAutoCab,{“A1_LOJA” , “01” , Nil})
AADD(xAutoCab,{“A1_NOME” , “TESTE-000001” , Nil}) 

BeginTran() 

lMsErroAuto := .F. 
MsExecAuto({|x,y| MATA030(x,y)}, xAutoCab, 3) 

IF lMsErroAuto 
    DisarmTransaction() 
ELSE 
    EndTran() 
ENDIF
MsUnlockAll()
```