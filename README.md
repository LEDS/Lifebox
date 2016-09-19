Software de Monitoramento de Temperatura
=============

O que o software faz?
-----------
Esse software tem um propósito bem geral, que é armazenar dados de temperaturas colhidas por dois sensores COLOCAR NOME DO SENSOR, controlados por um Arduino Mega. Esse dados são armazenados na memória do computador e depois é salvo em uma planilha no formato "xlsx".

Motivo da criação do software?
-----------
Esse software foi criado a princípio para estudar o comportamento das caixas térmicas que são usadas para o transporte de Órgãos humanos no estado do Espírito Santo, afim de verificar através dos dados colhidos pelo software como a caixa se comporta em diferentes situações (Exposta ao Sol, dentro do carro e etc), e com essas analises, tentar mostrar quais são os cuidados que se deve ter com a caixa durante o transporte, já que, segundo a Anvisa a temperatura do Órgão deve estar entre -2ºC a -8ºC, e qualquer temperatura a baixo e a cima disso pode inviabilizar a utilização do Órgão para ser transplantado.

Através de uma entrevista com o stakeholder para melhor entendimento do problema, foi percebido que eles devem fazer um teste de qualidade da caixa termica por eles utilizada no transporte de Órgãos para ser apresentado a Anvisa. Esse relatório consiste em um funcionário simular o ambiente dentro da caixa térmica - Colocar o Gelox para resfriar a caixa, colocar o suporte para o Órgão e etc - e ficar anotando em um papel de uma em uma hora a temperatura interna e externa mostrada pelo termômetro usado por deles, essa aferição era feita por eles durante 24 horas. Depois do funcionário ter anotado as aferições ele passava para o Excel os dados obtidos e montava um gráfico para gerar um relatório para aprensentar a Anvisa. Visto isso, foi percebido que o funcionamento do software pode automatizar esse processo, evitando trabalho manual e reduzindo um pouco o trabalho dos funcionários.

Installation
-----------

1. Download the python-rtmbot code

        git clone https://github.com/slackhq/python-rtmbot.git
        cd python-rtmbot

2. Install dependencies ([virtualenv](http://virtualenv.readthedocs.org/en/latest/) is recommended.)

        pip install -r requirements.txt

3. Configure rtmbot (https://api.slack.com/bot-users)

        cp docs/example-config/rtmbot.conf .
        vi rtmbot.conf
          SLACK_TOKEN: "xoxb-11111111111-222222222222222"

*Note*: At this point rtmbot is ready to run, however no plugins are configured.

Add Plugins
-------

Plugins can be installed as .py files in the ```plugins/``` directory OR as a .py file in any first level subdirectory. If your plugin uses multiple source files and libraries, it is recommended that you create a directory. You can install as many plugins as you like, and each will handle every event received by the bot indepentently.

To install the example 'repeat' plugin

    mkdir plugins/repeat
    cp docs/example-plugins/repeat.py plugins/repeat/

The repeat plugin will now be loaded by the bot on startup.

    ./rtmbot.py

Create Plugins
--------

####Incoming data
Plugins are callback based and respond to any event sent via the rtm websocket. To act on an event, create a function definition called process_(api_method) that accepts a single arg. For example, to handle incoming messages:

    def process_message(data):
        print data

This will print the incoming message json (dict) to the screen where the bot is running.

Plugins having a method defined as ```catch_all(data)``` will receive ALL events from the websocket. This is useful for learning the names of events and debugging.

Note: If you're using Python 2.x, the incoming data should be a unicode string, be careful you don't coerce it into a normal str object as it will cause errors on output. You can add `from __future__ import unicode_literals` to your plugin file to avoid this.

####Outgoing data
Plugins can send messages back to any channel, including direct messages. This is done by appending a two item array to the outputs global array. The first item in the array is the channel ID and the second is the message text. Example that writes "hello world" when the plugin is started:

    outputs = []
    outputs.append(["C12345667", "hello world"])

*Note*: you should always create the outputs array at the start of your program, i.e. ```outputs = []```

####Timed jobs
Plugins can also run methods on a schedule. This allows a plugin to poll for updates or perform housekeeping during its lifetime. This is done by appending a two item array to the crontable array. The first item is the interval in seconds and the second item is the method to run. For example, this will print "hello world" every 10 seconds.

    outputs = []
    crontable = []
    crontable.append([10, "say_hello"])
    def say_hello():
        outputs.append(["C12345667", "hello world"])

####Plugin misc
The data within a plugin persists for the life of the rtmbot process. If you need persistent data, you should use something like sqlite or the python pickle libraries.

####Direct API Calls
You can directly call the Slack web API in your plugins by including the following import:

    from client import slack_client

You can also rename the client on import so it can be easily referenced like shown below:

    from client import slack_client as sc

Direct API calls can be called in your plugins in the following form:
    
    sc.api_call("API.method", "parameters")

####Todo:
Some rtm data should be handled upstream, such as channel and user creation. These should create the proper objects on-the-fly.
