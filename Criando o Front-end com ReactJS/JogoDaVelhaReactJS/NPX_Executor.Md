# NODEJS

## Conhecendo o NPX - Executor de Pacotes do NPM
##### Thiago Marinho 

🚀   Vamos falar sobre o NPX, descobrir quem criou, quem está mantendo, o que podemos fazer com essa ferramenta, qual a vantagem de utilizar e algumas dicas. 👊

👩‍💻 Quem criou e quem está por trás dessa ferramenta?
O NPX foi desenvolvido pela Kat Marcán, atualmente é mantido pelo NPM, que foi comprado recentemente pelo Github. O NPX é um binário que está presente no NPM desde a versão 5.2.

🤷‍♂️ O que é?

NPX é um package runner do NPM. Ele executa as bibliotecas que podem ser baixadas do site npmjs. Essas bibliotecas ficam em um banco de dados chamado NPM Registry, que também podem ser baixadas via CLI com npm ou yarn e com npx como veremos a seguir.

NPM é um gerenciador de pacotes que já estamos acostumados a usar junto com o Node.js. Com NPM instalamos e desinstalamos as bibliotecas de um projeto ou da máquina. Com Yarn é a mesma coisa na prática.

Se o NPM é um gerenciador (manager) de pacotes, o NPX é um executor, por isso o X no final da sigla.

drwx = Directory/Read/Write/eXecute.

⏮️ Antes do NPX

Antes precisávamos instalar os pacotes do npm na máquina de maneira global.


npm install cowsay -g 

O binário do pacote instalado fica salvo no path e disponível no terminal para executar de qualquer local.

Porém, isso gerava problemas na seguinte situação: se mandasse o projeto para outro dev, ele não teria acesso as bibliotecas de maneira local, o mesmo deveria instalar a biblioteca global na máquina.


Instalando o cowsay globalmente: npm install cowsay -g

Projetos Locais

Surgiu a necessidade do package.json que tem as devDependencies e dependencies. Que contém todo o descritivo das bibliotecas necessárias no projeto.

Com isso podemos instalar as bibliotecas de maneira local por projeto, e então cada projeto passa a ter uma node_modules de acordo com a versão da biblioteca.


Instalando o cowsay no projeto local.

Criando um projeto com node e instalando a lib cowsay:

mkdir myNodeProject && cd myNodeProject && npm init -y && npm install cowsay

Executando a lib cowsay diretamente na node_modules:

node node_modules/cowsay/clis.js

Ou colocaria um script no package.json:

{
  "name": "blog-npx",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "fala": "cowsay"
  },
  "dependencies": {
    "cowsay": "^1.4.0"
  }
}
Resultado quando executar npm run fala algo legal:

❯ npm run fala algo legal

> blog-npx@1.0.0 fala /Users/tgmarinho/Developer/blog-rocketseat/blog-npx
> cowsay "algo" "legal"

 ____________
< algo legal >
 ------------
        \\   ^__^
         \\  (oo)\\_______
            (__)\\       )\\/\\
                ||----w |
                ||     ||

Developer/blog-rocketseat/blog-npx

🚀 Com NPX

O NPX busca a biblioteca na Registry do NPM, instala em uma pasta temporária, executa o comando e depois remove a biblioteca da máquina, ela não fica na node_modules global.

NPX não só busca no site do npmjs, como busca de dentro da node_modules do projeto também ou até mesmo na node_modules global antes de ir na Internet buscar a lib e executar.

Verifico se já tenho a lib instalada e executo com npx

Nesse outro exemplo eu desinstalo a lib cowsay e utilizo o npx para baixar e executar:

npx cowsay

Exemplo de como iniciar um projeto react native com typescript usando o npx.

npx react-native init MyApp --template react-native-template-typescript

O comando acima executa o react-native com o init MyAppRN --template react-native-template-typescript, para isso ele verifica se o react-native está presente na node_modules global, se não estiver ele baixa e executa de uma vez.

Uma vez o projeto criado e com a biblioteca do react-native na node_modules, mesmo que você executar novamente o npx react-native run-ios por exemplo, ele não vai na Internet buscar o react-native, mas sim vai utilizar o que está na node_modules.

😎 Vantagem

Ter o react-native cli ou create-react-app na máquina ocupa espaço e essas bibliotecas são atualizadas muito rápido, então não compensa ficar mantendo elas na máquina. O comando create-react-app, por exemplo, é feito uma vez e depois nunca mais, a menos que você comece outro projeto.

❯ du -sh react-native create-react-app 

306M	react-native
 28M	create-react-app

Olha ai o tanto de espaço que economiza na máquina: 334 Mb.

Inclusive a lib do React reforça isso.

📜 Documentação das bibliotecas
Hoje muitas documentações instruem instalar a sua biblioteca de forma global com parâmetro -g  mas estão desatualizadas, se for um script que cria um projeto basta executar com npx. Se você entendeu o que é o npx, já consegue identificar quando usar lib local ou usar apenas o npx.

Rodando node em outras versões
Temos o nvm Node Version Manager que faz o gerenciamento de versões do node na máquina.

Mas com o npx podemos também fazer o gerenciamento de versão também.

Exemplo:

❯ npx node@6 -v                               
v6.17.1
~/Developer took 12s 
❯ node -v                                                                             
v13.9.0
Perceba que o comando foi executado na versão 6.x do node, mas o node instalado na minha máquina está na versão 13.x

Sintaxe:

npx node@version <command>
🦸‍♀️ Avançado
Podemos ainda executar comandos que estão no Gist.

npx https://gist.github.com/tgmarinho/cbf45688de3c7a721785ccb4efbb10ca
O comando acima vai ler o arquivo package.json, instalar as bibliotecas de forma temporária, executar o script que está no "bin" do package.json.

O arquivo index.js está importando a lib cowsay e está imprimindo um log no console com o cowsaw. Veja o resultado:

❯ npx https://gist.github.com/tgmarinho/cbf45688de3c7a721785ccb4efbb10ca       
npx: installed 11 in 7.452s
 _____________________
< Hello Rocketseat!!! >
 ---------------------
        \\   ^__^
         \\  (OO)\\_______
            (__)\\       )\\/\\
             U  ||----w |
                ||     ||
Eu sou um script que está no gist e sendo executado com npx
~/Developer took 7s
Conclusão
A dica é: sempre que for criar um projeto react ou react native utilize o npx:

Criar um projeto com React:

npx create-react-app MyWebApp
Criar um projeto com React Native:

npx react-native init MyApp
Criar um projeto com React Native com Typescript:

npx react-native init MyApp --template react-native-template-typescript
➕ Plus:
Mostrando onde o binário foi instalado com Which:

which create-react-app
/Users/tgmarinho/.nvm/versions/node/v13.9.0/bin/create-react-app
which react-native
react-native not found
Exibindo o tamanho da pasta dom DU:

du -sh /Users/tgmarinho/.nvm/versions/node/v13.9.0/lib/node_modules/
454M
🔗 Links
Segue alguns links de referência sobre npx.

🔗  npx | awesome-npx | intro-npx-by-creator |dif-npm-e-npx | walde.co

READ MORE POSTS BY THIS AUTHOR
Thiago Marinho
Dev Apaixonado por Tecnologia & Educação! Evolua rápido como a tecnologia, aprendizado é contínuo e sempre haverá um próximo nível. Boost Yourself! 🚀

THE LINK HAS BEEN COPIED!
https://blog.rocketseat.com.br/conhecendo-o-npx-executor-de-pacote-do-npm/
PRÓXIMO POST
O que é README e porque é tão importante
POST ANTERIOR
5 dicas para uma carreira sólida como programador(a)

Blog da Rocketseat
HOME
 
BACK END
 
FRONT END
 
MOBILE
© 2021 Blog da Rocketseat. Feito com <3. Published with Ghost.
Palavras-chave...
DIGITE NO MÍNIMO 3 CARACTERES
Posso te sugerir um assunto?
REACT NATIVE REACT JAVASCRIPT REACTJS NODEJS EXPRESSJS BACKEND FRONT END REDUX ADONISJS ROCKETSEAT REACTNAVIGATION MAPBOX EXPO GITHUB NEXTJS DOCKER TYPESCRIPT TOP GRAPHQL
Posso te sugerir um autor?
DIEGO FERNANDES THIAGO MARINHO HIGO RIBEIRO CLAUDIO ORLANDI JOÃO PAULO DE MAGALHÃES TIAGO LUCHTENBERG CARLOS LEVIR
Blog da Rocketseat. Junte-se a milhares de devs e acelere na direção dos seus objetivos. Transforme sua carreira em uma jornada de evolução contínua através das melhores tecnologias..