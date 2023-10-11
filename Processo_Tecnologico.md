# Processo Tecnológico

O minério extraído passa por processamento primário para obter a mistura de minério que é a matéria-prima usada para flotação (que é um método de concentração do minério). Após a flotação, o material passa por uma purificação em duas etapas.

![https://practicum-content.s3.us-west-1.amazonaws.com/new-markets/DS_sprint_10/PT/10.3.2PT.png?etag=8496d983a4374c26bfbed704bfc14305](https://practicum-content.s3.us-west-1.amazonaws.com/new-markets/DS_sprint_10/PT/10.3.2PT.png?etag=8496d983a4374c26bfbed704bfc14305)

Vamos detalhar o processo:

**1. Flotação**

A mistura de minério de ouro é alimentada nos bancos de flotação para obter concentrado de Au bruto e outros restos de minérios brutos (resíduos de produtos com baixa concentração de metais valiosos).

A estabilidade deste processo é afetada pelo estado físico-químico volátil e não ótimo da polpa de flotação (uma mistura de partículas sólidas e líquidas).

**2. Purificação**

O concentrado bruto passa por duas etapas de purificação. Após a purificação, temos o concentrado final e novos restos de minério.

## Descrição de dados

**Processo tecnológico**

- *Rougher feed* — matéria-prima
- *Rougher additions* (ou *aditivos reagentes*) — reagentes de flotação: *Xantato, Sulfeto, Depressor*
    - *Xanthate* — promotor ou ativador da flotação
    - *Sulphate* — sulfeto de sódio para este processo específico
    - *Depressant* — silicato de sódio
- *Rougher process* — flotação
- *Rougher tails* — resíduos do produto
- *Float banks* — unidade de flotação
- *Cleaner process* — purificação
- *Rougher Au* — concentrado de ouro bruto
- *Final Au* — concentrado de ouro final

**Parâmetros das etapas**

- *air amount — volume of air* — volume de ar
- *fluid levels*
- *feed size* — tamanho de partícula alimentada
- *feed rate*

## Nomeação de características

Veja como você nomeia as características:

`[stage].[parameter_type].[parameter_name]`

Exemplo: `rougher.input.feed_ag`

Valores possíveis para `[stage]`:

- *rougher —* (Minério bruto) flotação
- *primary_cleaner* — purificação primária
- *secondary_cleaner* — purificação secundária
- *final* — características finais

Valores possíveis para `[parameter_type]`:

- *input* — parâmetros de matéria-prima
- *output* — parâmetros do produto
- *state* — parâmetros que caracterizam o estado atual do processamento
- *calculation* — características de cálculo

![https://practicum-content.s3.us-west-1.amazonaws.com/new-markets/DS_sprint_10/PT/10.3.2.2PT.png?etag=5c85836f278d616bbe69ee2f069a12b4](https://practicum-content.s3.us-west-1.amazonaws.com/new-markets/DS_sprint_10/PT/10.3.2.2PT.png?etag=5c85836f278d616bbe69ee2f069a12b4)

## Cálculo de retirada

Você precisa simular o processo de retirada do ouro puro do minério de ouro.

Use a seguinte fórmula para simular o processo de retirada:

![https://code.s3.yandex.net/new-markets/new_markets_data_images/DS,%20Sprint%2010/PT/10.3.2.3PT.png](https://code.s3.yandex.net/new-markets/new_markets_data_images/DS,%20Sprint%2010/PT/10.3.2.3PT.png)

$$ retirada = \fraq{C.(F-T))}{F.(C-T)}.100% $$

onde:

- *C* — proporção de ouro no concentrado logo após a flotação (para encontrar a quantidade retirada do concentrado bruto)/após a purificação (para encontrar a quantidade retirada final do concentrado)
- *F* — a proporção de ouro alimentado no sistema antes da flotação (para encontrar a quantidade retirada do concentrado bruto)/ quantidade no concentrado logo após a flotação (para encontrar a quantidade retirada final do concentrado)
- *T* — a proporção de ouro nos restos de minério bruto logo após a flotação (para encontrar a quantidade retirada do concentrado bruto)/ quantidade após a purificação (para encontrar a quantidade retirada final do concentrado)

Para prever o coeficiente, você precisará encontrar a proporção de ouro no concentrado e nos restos de minério. Observe que tanto os concentrados finais quanto os brutos importam.

## Métrica de avaliação

Para resolver o problema, precisaremos de uma nova métrica. É chamado de **sMAPE**, ou erro percentual absoluto médio simétrico.

É semelhante ao EAM, mas é expresso em valores relativos em vez de absolutos. Por quê é simétrico? Ele leva em conta a escala do objetivo e da previsão.

Veja como *sMAPE* é calculado:

![https://code.s3.yandex.net/new-markets/new_markets_data_images/DS,%20Sprint%2010/PT/10.3.2.4PT.png](https://code.s3.yandex.net/new-markets/new_markets_data_images/DS,%20Sprint%2010/PT/10.3.2.4PT.png)

Denotação:

![https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_y1_1576238832_1589899414.jpg](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_y1_1576238832_1589899414.jpg)

- Valor do objetivo para a observação com o índice *i* no conjunto utilizado para medir a qualidade.

![https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_yi_1_1576238835_1589899461.jpg](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_yi_1_1576238835_1589899461.jpg)

- Valor da predição para a observação com o índice *i*, por exemplo, na amostra de teste.

![https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_N_1_1576238819_1589899496.jpg](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_N_1_1576238819_1589899496.jpg)

- Número de observações na amostra.

![https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_I_1576238817_1589899530.jpg](https://practicum-content.s3.us-west-1.amazonaws.com/resources/moved_I_1576238817_1589899530.jpg)

- Somatório de todas as observações da amostra (***i*** assume valores de 1 a *N*).

Precisamos predizer dois valores:

1. Quantidade retirada do concentrado bruto `rougher.output.recovery`
2. Quantidade retirada final do concentrado `final.output.recovery`

A métrica final inclui os dois valores:

![https://code.s3.yandex.net/new-markets/new_markets_data_images/DS,%20Sprint%2010/PT/10.3.2.5PT.png](https://code.s3.yandex.net/new-markets/new_markets_data_images/DS,%20Sprint%2010/PT/10.3.2.5PT.png)