Exit code: 0
Wall time: 0.3 seconds
Output:
# SolicitaÃ§Ã£o de Financeiro SPOA - FNHIS Sub 50

AplicaÃ§Ã£o estÃ¡tica para uso no navegador. Recebe separadamente a planilha de solicitaÃ§Ã£o de caixa do DHR e a extraÃ§Ã£o de saldos de empenho do SIAFI, produzindo a planilha padronizada para a SPOA.

## Uso

1. Acesse a pÃ¡gina publicada e anexe a planilha de solicitaÃ§Ã£o de caixa do DHR.
2. Anexe a extraÃ§Ã£o de Saldos de Empenho do SIAFI.
3. Clique em **Gerar Planilha SolicitaÃ§Ã£o de Financeiro SPOA**.
4. Baixe o arquivo gerado. A aba `LOG` traz os contratos que nÃ£o puderam ser distribuÃ­dos integralmente e a razÃ£o da inconsistÃªncia.

## Regras de reconhecimento

- A aplicaÃ§Ã£o busca os cabeÃ§alhos nas primeiras 30 linhas de cada aba, permitindo arquivos com linhas de tÃ­tulo antes da tabela.
- VariaÃ§Ãµes como `Proposta TGOV`, `Prop. TGOV` e nÃºmeros no formato `33404/2024` sÃ£o normalizadas.
- SÃ£o aceitas, entre outras, as variaÃ§Ãµes `NÂº Instrumento` para ConvÃªnio, `Nome Proponente` para Tomador e `Valor da Parcela autorizado RP3` para o valor solicitado.
- Quando nÃ£o encontra cabeÃ§alho ou sinÃ´nimo, a aplicaÃ§Ã£o verifica o perfil dos valores: ConvÃªnio Ã© um nÃºmero de seis dÃ­gitos iniciado por 9; UF Ã© uma sigla vÃ¡lida; proposta termina em ano; e Nota de Empenho contÃ©m o padrÃ£o `AAAA NExxxxx`.
- Campos nÃ£o utilizados no resultado podem deixar de ser reconhecidos sem impedir o processamento. Para campos indispensÃ¡veis, a aplicaÃ§Ã£o sÃ³ infere um candidato quando o perfil for Ãºnico; se houver ambiguidade, informa o campo que precisa ser identificado.
- A identificaÃ§Ã£o da Nota de Empenho aceita cÃ³digos longos do SIAFI e extrai o trecho no formato `AAAA NExxxxx`.
- Para ligar uma solicitaÃ§Ã£o a uma nota, a aplicaÃ§Ã£o prioriza o `CONVENIO_SIAFI` do DHR contra o `NÃºmero do ConvÃªnio` do SIAFI. Na ausÃªncia desse campo, tenta proposta/processo e, por fim, favorecido contra Tomador ou MunicÃ­pio.
- Para NEs de anos anteriores, o saldo disponÃ­vel Ã© exclusivamente `Restos a Pagar a Pagar`. Para NEs do ano atual, o saldo disponÃ­vel Ã© exclusivamente `Despesas Empenhadas a Liquidar`. SÃ£o considerados empenhos de 2025 e 2026.
- A aplicaÃ§Ã£o prioriza o exercÃ­cio mais antigo. Quando um saldo complementar precisar ser atendido por empenhos de exercÃ­cio posterior, prioriza a menor NE suficiente para reduzir saldos residuais.

## SaÃ­da

A planilha gerada possui a aba `ajustada CORH`, com o cabeÃ§alho definido pela CORH, e a aba `SALDOS DE EMPENHO`, que conserva a extraÃ§Ã£o do SIAFI. A aba `LOG` Ã© criada somente quando houver inconsistÃªncias. AÃ§Ã£o, abreviatura e UGs sÃ£o preenchidas como `00TI`, `FNHIS SUB 50`, `560015` e `560018`.


