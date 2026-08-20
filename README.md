Exit code: 0
Wall time: 0.3 seconds
Output:
# Solicitação de Financeiro SPOA - FNHIS Sub 50

Aplicação estática para uso no navegador. Recebe separadamente a planilha de solicitação de caixa do DHR e a extração de saldos de empenho do SIAFI, produzindo a planilha padronizada para a SPOA.

## Uso

1. Acesse a página publicada e anexe a planilha de solicitação de caixa do DHR.
2. Anexe a extração de Saldos de Empenho do SIAFI.
3. Clique em **Gerar Planilha Solicitação de Financeiro SPOA**.
4. Baixe o arquivo gerado. A aba `LOG` traz os contratos que não puderam ser distribuídos integralmente e a razão da inconsistência.

## Regras de reconhecimento

- A aplicação busca os cabeçalhos nas primeiras 30 linhas de cada aba, permitindo arquivos com linhas de título antes da tabela.
- Variações como `Proposta TGOV`, `Prop. TGOV` e números no formato `33404/2024` são normalizadas.
- São aceitas, entre outras, as variações `Nº Instrumento` para Convênio, `Nome Proponente` para Tomador e `Valor da Parcela autorizado RP3` para o valor solicitado.
- Quando não encontra cabeçalho ou sinônimo, a aplicação verifica o perfil dos valores: Convênio é um número de seis dígitos iniciado por 9; UF é uma sigla válida; proposta termina em ano; e Nota de Empenho contém o padrão `AAAA NExxxxx`.
- Campos não utilizados no resultado podem deixar de ser reconhecidos sem impedir o processamento. Para campos indispensáveis, a aplicação só infere um candidato quando o perfil for único; se houver ambiguidade, informa o campo que precisa ser identificado.
- A identificação da Nota de Empenho aceita códigos longos do SIAFI e extrai o trecho no formato `AAAA NExxxxx`.
- Para ligar uma solicitação a uma nota, a aplicação prioriza o `CONVENIO_SIAFI` do DHR contra o `Número do Convênio` do SIAFI. Na ausência desse campo, tenta proposta/processo e, por fim, favorecido contra Tomador ou Município.
- Para NEs de anos anteriores, o saldo disponível é exclusivamente `Restos a Pagar a Pagar`. Para NEs do ano atual, o saldo disponível é exclusivamente `Despesas Empenhadas a Liquidar`. São considerados empenhos de 2025 e 2026.
- A aplicação prioriza o exercício mais antigo. Quando um saldo complementar precisar ser atendido por empenhos de exercício posterior, prioriza a menor NE suficiente para reduzir saldos residuais.

## Saída

A planilha gerada possui a aba `ajustada CORH`, com o cabeçalho definido pela CORH, e a aba `SALDOS DE EMPENHO`, que conserva a extração do SIAFI. A aba `LOG` é criada somente quando houver inconsistências. Ação, abreviatura e UGs são preenchidas como `00TI`, `FNHIS SUB 50`, `560015` e `560018`.


