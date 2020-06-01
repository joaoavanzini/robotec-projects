#AgroRover

Com o desenvolvimento da tecnologia no campo, startup’s e empresas de robótica (como a própria Robotec) começam a pensar ao futuro. Desenvolvem princípios e programações para um futuro robô no qual ajudam o plantio, colheita e até mesmo a adubações das plantas. Uma ideia do Mário Avancini, fez com que o próprio criador da Robotec crie e automatize um robô, onde este AgroRover precisa molhar e deixar plantas em perfeito estado para a sobrevivência em si.

João Victor Barbosa (creator of  Robotec): – “Foi ai que concordei, pois precisava de algo novo. Algo revolucionário.” Comecei a criar esboços para a programação e em alguns meses ( de 4 a 6 meses ) já consegui um grande feito.

Uma versão “beta” já está disponível para a compra do código. O código vem com um “kit” inicial, onde temos oque precisamos para a “cabeça” do projeto

![Kit Inicial](https://raw.githubusercontent.com/vicpb/robotec-projects/AgroRover01.png)

Ao executar o arquivo principal, temos um menu.

![Menu](https://raw.githubusercontent.com/vicpb/robotec-projects/agrorover/AgroRover02.png)

A primeira opção é como usar / uma ajuda além do README.

A segunda opção diz a respeito do desenvolvimento do caminho do Rover. Ele andará sozinho, e suas coordenadas de objetos é dada pelo seu HC-SR04 (sensor ultrassônico), desviando e escolhendo o melhor caminho.

![Detecção do melhor caminho](https://raw.githubusercontent.com/vicpb/robotec-projects/agrorover/AgroRover03.png)

Na terceira opção podemos “desenhar” um caminho, onde ele irá seguir. Sua precisão será baseada ao torque do motor, rodas, velocidade e peso. Para este “desenho”, você deverá modificar o código, dizendo se ele irá para frente, para trás, esquerda, ou direita.

![“Desenho” do caminho](https://raw.githubusercontent.com/vicpb/robotec-projects/agrorover/AgroRover04.png)

Para a ultima opção, resolvi criar uma área onde podemos ver aquilo que o Rover vê. Daqui algumas atualizações, teremos a opção de fazer stream pelo navegador; sendo assim, visualizando em real-time.

Quando selecionamos esta opção, é feito uma foto, desta foto é salva em uma galeria (em “Pictures” – pasta do kit inicial); esta mesma foto é salva no apache2, nos possibilitando a opção de ver direto no navegador.

![Pictures](https://raw.githubusercontent.com/vicpb/robotec-projects/agrorover/AgroRover05.png)

Para a visualização das fotos, basta acessar o ip correspondente ao AgroRover em sua rede de internet, e acessar a pasta “Pictures”, mostrando então todas as fotos retiradas até o momento.

![Foto visualizada através do navegador](https://raw.githubusercontent.com/vicpb/robotec-projects/agrorover/AgroRover06.png)

![AgroRover](https://raw.githubusercontent.com/vicpb/robotec-projects/agrorover/Rover.png)

Assim que possível, farei um vídeo sobre. Estamos em versão “beta”, então várias coisas, alem do código poderá ser mudadas: visual do Rover, altura, peso, etc. Deixarei vocês o máximo possível atualizados.