# Configurando ambiente

1. **yarn init -y** para criar o arquivo package.json
2. **yarn add react** para adicionarmos o modulo do react
3. **yarn add react-dom** baixamos a dependencia do DOM em React para permitir a comunicação com os elementos em tela
4. Criando a organização do nosso projeto:

- Crie uma pasta **src** onde irá ficar todo codigo criado por nós.
- Crie uma pasta **public** onde vai ficar arquivo ou assets que são os arquivos publicos, como icones
  robots.txt e qualquer arquivo que precise ser acessada de meio externo

**public**

1. Crie um arquivo chamado **index.html**

# Instalando o Babel

1. O quê é Babel?

- Basicamente é um "conversor" de codigo para uma maneira em que todos os browsers consigam entender nosso codigo devido que o javascript se atualiza muito e as vezes.

2. **yarn add @babel/core @babel/cli @babel/preset-env -D** para inicializarmos o babel o -D é para desenvolvimento

3. Em seguida crie um arquivo chamado **babel.config.js** e exporte os presets:

~~~javascript
   module.exports = {
      presets: [
      '@babel/preset-env'
      ]
   }
~~~

4. Podemos converter codigos diretamente pelo babel desde que já tenhamos instalado o Babel
   **yarn babel src/index.js --out-file dist/bundle.js**

5. Quando acessarmos a basta dist veremos o codigo de nossa aplicação convertido para que outros
   browsers consigam entender

6. Porém até agora não iremos conseguir fazer com que o babel entenda html no javacript
   para fazer isso precisamos adicionar **yarn add @babel/preset-react -D**

7. Agora teremos que ir em nosos **babel.config.js** e adicionar o **@babel/preset-react**

8. É legal alteramos nosso arquivo index.js para index.jsx pois jsx é a nomenclatura quando usamos html no javascript

**src**

1. Crie um arquivo chamado **index.js**

# Instalando o Webpack

1. O quê é o Webpack?

- Ele vai estipular uma serie de configurações em que chamamos de loaders que vão ensinar para nossa aplicação como ela deve tratar cada tipo de arquivo transformando todos em .js .css .jpg .png

2. **yarn add webpack webpack-cli -D** instalando como dependencia de desenvolvimento

3. Em seguida crie um arquivo chamado **webpack.config.js** e passe o **entry** ele fala qual é o arquivo inicial/principal da aplicação

4. Depois de passarmos o entry precisamos passar o **output** que seria o arquivo que iremos gerar com o webpack, também podemos passar o **resolve: {extensions: ['.js', '.jsx']}** que serve para dizer que ele pode ler tanto arquivo js quanto arquivo jsx

5. Temos que passar o **module** é onde irá ficar as configurações de como a nossa aplicação irá se comportar

6. Quando passarmos dentro de module as regras iremos usar o **use** e nela iremos passar o babel-loader
   que temos que instalar com **yarn add babel-loader -D**

7. Agora basta fazer um teste... Crie um arquivo **src/App.jsx** e dentro dele vamos criar uma mini estrutura de react

8. Para remover o erro "The 'mode' option ..." basta ir no webpack.config.js e adicionar **mode: 'development'**

# Estrutura do ReactJS

1. Vá até o index.html e adicione logo após o body uma div: <div id="root"></div>

- Essa div é onde será armazenada todo conteudo de nossa aplicação

2. No **index.jsx** iremos importar o **react-dom** e usar a função **ReactDOM.render()**

3. Podemos também "parar" de ter que importar o React toda vez que criarmos um jsx

- Podemos ir em **babel.config.js** e adicionar:

~~~javascript
  ['@babel/preset-react', {
      runtime: 'automatic'
  }]
~~~

- Agora não iremos mais precisar ficar importando o React toda vez que for escrever html

# Servindo HTML Estatico

1. Iremos até o **public/index.html**, em seguida, remova a tag script
2. Vá até o cmd e adicione **yarn add html-webpack-plugin -D**
3. Depois vamos até o **webpack.config.js** e crie uma const: **const HtmlWebpackPlugin = require('html-webpack-plugin')**
4. Depois inclua em seu webpack config:

- 
~~~javascript
plugins: [
   new HtmlWebpackPlugin({
   template: path.resolve(__dirname, 'public', 'index.html')
   }),
],
~~~

# Webpack DevServer

1. **yarn add webpack-dev-server -D**

2. Iremos usar o webpack-dev-server para que ele fique observando os nosso arquivos e a cada vez que houver uma atualização ele irá gerar o novo bundle

3. Para isso vá em **webpack.config.js** e adicione um objeto **DevServer** passando a propriedade **contentBase: path.resolve(\_\_dirname, 'public')**

4. E para executarmos nosso codigo a partir de agora basta digitar webpack serve

# Source Maps

1. São uma forma de conseguir checar o codigo original de nossa aplicação mesmo quando ela está embaralhado no bundle.js

2. Para isso vamos no **webpack.config.js** e embaixo de mode adicione **devtool: 'eval-source-map'**

# Ambiente Dev & Produção

1. Crie uma constante com o nome **isDevelopment** que receba o valor  
   **process.env.NODE_ENV !== 'production'** e crie uma verificação em **mode** e **devtool**
   mode: isDevelopment ? 'development' : 'production',
   devtool: isDevelopment ? 'eval-source-map' : 'source-map',

2. Porém temos que criar essa variavel do .NODE_ENV no linux podemos criar da seguinte forma:
   no console digite: 

   ~~~javascript
   _NODE_ENV=production webpack yarn webpack
   ~~~

- No windows para fazer funcionar devemos fazer da seguinte forma:
  **yarn add cross-env -D** ela serve para definirmos variaveis env independente do sistema operacional
- Depois de instar vá até o packege.json e crie um "scripts" que receba:

~~~javascript
"scripts": {
"dev": "webpack serve",
"build": "cross-env NODE_ENV=production webpack"
}
~~~

# Importando arquivos CSS

- Crie uma pasta chamada styles dentro de src e um arquivo global.css e importe no App.jsx

- O que fizemos acima nós retorna um erro não? Pois ele não conseguiu entender o nossso css pois ele só entende javascript, então iremos criar uma nova regra para arquivo css no **webpack.config.js**

- Antes disso devemos instalar **yarn add style-loader css-loader -D**

- Logo em seguida basta adicionar em **rules** a nova regra:

~~~javascript
  {
  test: /\.css$/,
  exclude: /node_modules/,
  use: ['style-loader', 'css-loader'],
  }
~~~

# Configurando o Sass
- yarn add node-sass sass-loader -D 

- Adicionamos ele nas regras do css do webpack config  e mudamos o **,css** para **.scss**



<h4>Feito no Ignite da @Rocketseat </h4>