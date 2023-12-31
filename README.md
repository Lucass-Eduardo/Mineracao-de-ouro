# Descrição

[Zyfra](https://www.zyfra.com/industries/industrial-artificial-intelligence-lab/) é uma empresa de tecnologia com foco em soluções para a indústria pesada, o objetivo desse projeto é treinar modelos  capazes de prever a quantidade de ouro puro extraído do minério de ouro e escolher o melhor modelo.

A extração do ouro é uma tarefa complexa e para entender melhor o projeto é necessário entender o ***[processo tecnológico](https://github.com/Lucass-Eduardo/Mineracao-de-ouro/blob/main/Processo_Tecnologico.md)*** da extração do ouro e avaliação do modelo. 

## Estrutura do Projeto

1. **Preparar os dados**
    - Os dados estão em 3 arquivos:
        - *`/datasets/gold_recovery_train.csv` : [Dados de treinamento.](https://tripleten.com/trainer/data-scientist/lesson/b2e60a2e-bac1-4a55-b822-0f4725e244c8/)*
        - *`/datasets/gold_recovery_test.csv`: [Dados de teste.](https://practicum-content.s3.us-west-1.amazonaws.com/datasets/gold_recovery_test.csv?etag=1e251eb453e155475fca8d03d8b66ae2)*
        - *`/datasets/gold_recovery_full.csv` : [Dados completos.](https://practicum-content.s3.us-west-1.amazonaws.com/datasets/gold_recovery_full.csv?etag=b2fba00139bca2b8c4c9af43667e0656)*
    - Verifiquei nos dados  se a retirada (na coluna `rougher.output.recovery`) foi calculada corretamente:
        - Refis todo o calculo da retirada.
        - Usei o MSA(Erro quadrático absoluto) como métrica para comparar os resultados.
    - Analisei o conjunto de teste para identificar as características não disponíveis, dessa forma eu descobri quais características meu modelo teria que usar para fazer a previsão.
    - Por ultimo eu fiz o pré-processamento dos dados.
2. **Analise os dados**
    - Observei como as concentrações (*Au, Ag, Pb*) mudam dependendo do estágio de purificação.
    - Comparei a as distribuições de partículas de minério no conjunto de treinamento e no conjunto de teste. Pois se elas variassem muito, a avaliação do modelo estaria incorreta.
    - Observei as concentrações totais de todas as substâncias em diferentes estágios: minério bruto, concentrado bruto e concentrado final.
3. **Construção modelo**
    - Primeiro escrevi a função para calcular a métrica *sMAPE*.
    - Treinei diferentes modelos:
        - Testei vários hiperparâmentros para melhorar a previsão dos modelos.
        - Comparei os resultados e selecionei os melhores modelos para fazer o teste final.
    - Testei os melhores modelos e para avalia-los utilizei o  calculo *sMAPE FINAL*.
