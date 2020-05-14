# AUTOMATIZAÇÃO DE MENSAGENS NO WHATSAPP COM OPENPYXL E SELENIUM

Esse repositório contêm todos os arquivos necessários para executar um programa que, dada uma lista de contatos telefônicos e nomes
associados, envia uma mensagem personalizada para cada contato pelo Whatsapp Web. Nota-se que embora já exista uma miríade de ferramentas poderosas de automação no Whatsapp - destacando-se o Whatsapp Bussines e o Twilio - todas esbarram em algum tipo de dificuldade, o que ensejou a criação desse programa. Dentre outros problemas, o Whatsapp Bussiness, por exemplo, demanda que todos os contatos telefônicos sejam registrados num chip antes do envio das mensagens e o Twilio, além de não ser gratuito, possui uma série de dificuldades burocráticas para que seu uso seja autorizado. Entendendo que o programa desenvolvido demanda certas especificações no seu uso, abaixo e no vídeo anexado nesse repositório residem explicações de como utilizá-lo. 

# I) Explicando os arquivos do repositório
   Existem cinco arquivos no repositório:
  
   1) driver.py, arquivo python que possui todos as funções necessárias para todar o programa. 
   
     - para facilitar a leitura para o usuário, foi optado por manter todo o código num mesmo arquivo;
     - o código foi extensivamente comentando e é fortemente recomendado que o usuário, mesmo não entendendo de 
     programação, tente ler o que foi escrito e ter uma noção mínima de como o programa funciona;
       
   2) ContatosPame.xlsx, arquivo excel onde estão contidos todos os contatos telefônicos e nomes associados que receberão as mensagens.
   
     - é importante notar que não se pode mudar nem o nome nem a extensão desse arquivo: o programa driver.py 
     o identifica como "ContatosPame.xlsx" e qualquer mudança implicará em erro;
     
     - dentro dessa planilha, deve necessariamente existir uma aba com o nome "telefones". Mais uma vez, 
     ressalta-se que qualquer mudança nesse nome implicará em erro. Podem haver outras abas com nomes distintos 
     sem problemas;
     
     - na aba "telefones" devem existir duas colunas: a coluna A, com "Telefones" na primeira linha, e a 
     coluna B, com "Nomes". Na coluna A devem estar contidos os contatos telefônicos - QUE DEVEM ESTAR 
     NO FORMATO 5521 + NÚMERO (EXEMPLO: 5521982086222) - qualquer mudança na formatação fará com que o 
     contato telefônico não seja reconhecido pelo Whatsapp (por exemplo, +5521982086222 o 215521982086222 não
     serão considerados números válidos). Na coluna B devem estar os nomes associados a cada contato telefônico,
     que podem ou não ser utilizados para enviar uma mensagem personalizada para cada contato. Nota-se que
     nesse caso os nomes "Telefones" e "Nomes" colocados no cabeçalho das colunas A e B, respectivamente, 
     podem ser alterados sem implicar em erro no programa;
     
   3) chromedriver.exe, que é um requisito do programa driver.py para que o programa navegue pelo google chrome. 
   
    - é possível que a versão do chromedriver.exe desse repositório não seja compatível com a versão do 
    google chrome do usuário. Nesse caso, o programa implicará em erro logo no seu início e haverá uma mensagem 
    avisando o erro e requisitando que o usuário instale um chromedriver compatível. Para descobrir qual versão 
    do google chrome está instalada, basta acessar chrome://version e verificar o número na primeira linha. 
    Para instalar o chromedriver adequado à sua versão, você pode ir em https://chromedriver.chromium.org/downloads
    e encontrar a versão correta. Lembre-se de, na pasta onde estão os arquivos driver.py e ContatosPame.xlsx,
    substituir o chromedriver.exe antigo pelo recêm instalado.
    
   4) Explicação.mp4, que é um vídeo explicativo de como usar o programa, desde a instalação, configuração do 
   ambiente e solução de problemas à demonstração do seu uso na prática;
   
   5) README.md, que simplesmente contêm o texto aqui escrito.
    
    
# II) Configuração do ambiente
    Para que o programa funcione, deve ser instalado:

    1) Python 3.8, cujo IDLE (interpretador) permite a leitura do código de driver.py
      - link para download: https://www.python.org/downloads/release/python-380/
      - a princípio qualquer versão do Python 3 deve servir;
      
    2) openpyxl e selenium, duas bibliotecas do Python que permitem a leitura de dados na planilha e automação do 
    envio de mensagens, respectivamente;
      - link para documentação do openpyxl: https://openpyxl.readthedocs.io/en/stable/
      - link para documentação do selenium: https://selenium-python.readthedocs.io/
      
      Para instalar essa bibliotecas e permitir que o Python no seu computador use o código dessa bibliotecas,
      é sugerido que você utilize o PIP, um gerenciador de pacotes de Python (mais informações em 
      https://www.w3schools.com/python/python_pip.asp). 
      
      - a princípio basta ir no seu terminal de comando (pesquisar por prompt de comando) e, executando esse 
      programa como administrador (clique com o botão direito e selecione "Executar como Administrador"),
      digite os seguintes comandos:
        - pip install openpyxl 
        - pip install selenium
        
      Se algum erro ocorrer, provavelmente você não tem o PIP configurado na sua variável de ambiente. Para
      resolver esse problema, você deve:
      
      2.1) procurar a pasta na qual o Python foi instalado no seu computador.
      Ali - ou em alguma pasta perto - haverá uma outra pasta chamada "Scripts". Copie o caminho dessa pasta
      (clique na pasta - sem abrir - e no canto superior esquerdo da sua tela haverá um pequeno botão com o 
      texto "Copiar Caminho". Clique ali);
      
      2.2) com o caminho copiado, clique no botão windows e procure no seu computador por "Editar variáveis de
      ambiente do sistema". Abra isso e então clique em "Variáveis de ambiente". Clique então para editar a
      variável "PATH" e adicione uma nova variável com o caminho copiado no passo 2.1) (no meu caso, por 
      exemplo, é "C:\Users\Leonardo\AppData\Local\Programs\Python\Python38-32\Scripts"). Se não houver
      um botão "Novo" para criar uma nova variável em PATH, você deverá colocá-la no final da linha
      com um ponto e vírgula no final;
      
      2.3) reinicie seu promt de comando, execute-o como administrador e tente novamente os comandos
        - pip install openpyxl 
        - pip install selenium
        
# III) Configuração do programa
    Com o python e as bibliotecas openpyxl e selenium instaladas, abra o arquivo driver.py que contêm todo
    código do programa (abra o IDLE do Python, no menu superior clique em "File", então "open" e encontre 
    o arquivo driver.py). 
    Mais uma vez: recomenda-se que, mesmo se o usuário não possuir uma grande noção de programação, o 
    arquivo seja lido, pois ele foi extensivamente comentado de maneira a facilitar seu entendimento e
    uso. 
    
    1) Na função "loopPhoneListAndSendMessage", que deve estar em azul, procure pela variável "message", 
    que foi inicialmente configurada com "Ola, Leonardo". Essa é a mensagem que será enviada para cada
    contato telefônico. 
    Como comentado no programa, se você quiser enviar uma mensagem que contenha quebras de linha, você 
    deverá encodificar a mensagem em https://www.url-encode-decode.com/. Com a mensagem encodificada,
    copie-a e cole-a no lugar de Ola, Leonardo ou a mensagem que estiver colocada na variável message.
    Lembre-se que sua mensagem deve estar dentro de aspas, "OLA, LEONARDO", "EXEMPLO DE MENSAGEM", etc. 
    Para entender porque, acesse https://www.w3schools.com/python/python_strings.asp. 
    
    2) ESSENCIAL: para que o programa funcione, o selenium deve reconhecer a caixa de texto que possui
    a mensagem a ser enviada no whatsapp e pressionar enter. Para reconhecer essa caixa de texto,
    devemos especificar o que está escrito nela - no caso a nossa mensagem. ENTÃO SEMPRE QUE VOCÊ
    MODIFICAR A MENSAGEM, a variável "xpath", que está algumas linhas abaixo da variável "message"
    e que especifica onde está a caixa de texto - deve ser modificada com algum trecho da mensagem
    a ser enviada.
    xpath contêm quatro string concatenas com o sinal de "+" 
    (exemplo: xpath = "//*[contains(text(), " + "'"+ "Ola" + "')]"). Altere a terceira string, que
    nesse exemplo possui "Ola", colocando algum trecho da mensagem que você está enviando. Exemplo:
    se sua mensagem é message ="Meu nome é João, tenho 23 anos, 64 quilos e sou legal", seu xpath 
    deve ser algo similar a xpath = "//*[contains(text(), " + "'"+ "tenho 23 anos" + "')]"). 
    Se sua mensagem estiver encodifcada, não use caracteres encodificados no xpath, mas um trecho
    da sua mensagem escrita mesmo. 
    
    3) Se você deseja utilizar o nome associado ao contato telefônico na sua mensagem, você deve 
    concatenar a variável namesList[i] à sua string em message. namesList[i], no escopo em questão,
    representa o nome associado ao contato telefônico que enviaremos a mensagem.
    
    Exemplo: message = "Ola, Leonardo". Queremos substituir "Leonardo" pelo nome associado ao contato
    telefônico. Faremos então message = "Ola, " + namesList[i]. 
    Se sua mensagem estiver encodificada, seguimos o mesmo princípio. 
    Exemplo: message = "Ola%2C+Leonardo", transformada fica: message = "Ola%2C+" + namesList[i]
    
    
    4) Apenas relembrando: os contatos telefônicos e nomes que são utilizados no programa estão
    contidos na aba "telefones" da planilha "ContatosPame.xlsx", que deve estar na mesma pasta
    do arquivo driver.py e do arquivo chromedriver.exe. Na coluna A da aba "telefones" você pode
    configurar os contatos telefônicos e na coluna B os nomes. 

# IV) Rodando o programa
    Supondo que o Python 3 e as bibliotecas openpyxl e selenium foram instalados, que a planilha 
    "ContatosPamexlsx" foi configurada com os corretos contatos telefônicos (deve ser no modelo
    5521982086343, por exemplo, sem "+", espaços ou coisas do tipo) e nomes associados e que a
    mensagem e o xpath foram ajeitados, basta pressionar F5 e executar o programa. Com isso:

    1) A página principal do Whatsapp Web aparecerá e o usuário terá 15 segundos para scannear 
    o QR code e acessar sua conta do Whatsapp;
    
    2) O programa automaticamente começara a rodar, seguindo a ordem dos contatos passados na 
    coluna A da aba "telefones" da planilha "ContatosPame.xlsx" e enviando a mensagem especificada
    para cada contato telefônico. Se por algum motivo a mensagem não estiver sendo enviada, 
    reconfigure a variável xpath (III.2) com outro trecho da sua mensagem. Se a mensagem enviada
    não for a desejada ou algum erro estiver ocorrendo, basta fechar o programa e ele será parado
    imediatamente;
      
      
      
   
