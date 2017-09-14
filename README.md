Software de Monitoramento de Temperatura
=============

O que o software faz?
-----------
Esse software tem um propósito bem geral, que é armazenar dados de temperaturas colhidas por dois sensores COLOCAR NOME DO SENSOR, controlados por um Arduino Mega. Esse dados são armazenados na memória do computador e depois é salvo em uma planilha no formato "xlsx".

Motivo da criação do software?
-----------
Esse software foi criado a princípio para estudar o comportamento das caixas térmicas que são usadas para o transporte de Órgãos humanos no estado do Espírito Santo, afim de verificar através dos dados colhidos pelo software como a caixa se comporta em diferentes situações (Exposta ao Sol, dentro do carro e etc), e com essas analises, tentar mostrar quais são os cuidados que se deve ter com a caixa durante o transporte, já que, segundo a Anvisa a temperatura do Órgão deve estar entre -2ºC a -8ºC, e qualquer temperatura a baixo e a cima disso pode inviabilizar a utilização do Órgão para ser transplantado.

Através de uma entrevista com o stakeholder para melhor entendimento do problema, foi percebido que eles devem fazer um teste de qualidade da caixa termica por eles utilizada no transporte de Órgãos para ser apresentado a Anvisa. Esse relatório consiste em um funcionário simular o ambiente dentro da caixa térmica - Colocar o Gelox para resfriar a caixa, colocar o suporte para o Órgão e etc - e ficar anotando em um papel de uma em uma hora a temperatura interna e externa mostrada pelo termômetro usado por deles, essa aferição era feita por eles durante 24 horas. Depois do funcionário ter anotado as aferições ele passava para o Excel os dados obtidos e montava um gráfico para gerar um relatório para aprensentar a Anvisa. Visto isso, foi percebido que o funcionamento do software pode automatizar esse processo, evitando trabalho manual e reduzindo um pouco o trabalho dos funcionários.
