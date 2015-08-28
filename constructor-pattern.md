## Constructor Pattern

Em linguagens clássicas orientada a objetos, o `constructor` é um método especial usado para inicializar um objeto 
recém criado, uma vez que a memória já foi alocada para ele. Como em JavaScript quase tudo é um objeto, estamos interessados
em objetos construtores.

Objetos construtores são usados para criar tipos especificos de objetos, preparando o objeto para uso e aceitar argumentos
que um construtor pode usar para definir os valores da propriedade e métodos quando o objeto é criado pela primeira vez


### Criando o Objeto

Segue uma das três maneiras comuns de se criar objeto em JavaScript: 

```javascript
// Opções de criar objetos vazios

var novoObjeto = {};

// ou
var novoObjeto = Object.create(Object.prototype);
// ou
var novoObjeto = new Object();
```

No último exemplo o "Object" constructor cria um objeto para um valor especificou ou quando não é passado
nenhum valor ele cria um objeto vazio e retorna o mesmo.

Continuando, existem várias maneiras de atribuir a um objeto valores do tipo chave/valor, vamos ver algumas delas:

```javascript
// Usando ponto (.)
 
// Setando propriedade
novoObjeto.chave= "Olá";
 
// Obtendo propriedade
var value = novoObjeto.chave;
 
 
// Usando colchetes([])
 
// Setando propriedade
novoObjeto["chave"] = "Olá";
 
// Obtendo propriedade
var value = novoObjeto["chave"];
 
```

### Construtores básicos

Como vimos, JavaScript não suporta o conceito de classes mas ele simula com funções construtoras que trabalham com objetos
O prefixo usado para chamar uma função contrutora é o `new` que cria o objeto com seus membros que foram definidos.

Nos construtores, a palavra `this` faz referência ao novo objeto que está sendo criado, vejamos:


```javascript
// A RacionaisMCs "class"
function RacionaisMCs( music ) {
 
  this.music = music;
  this.year = "2014";
  // Adicionando comportamento a classe
  this.getInfo = function () {
    return this.music + " " + this.year;
  };
 
};
// Criando objetos
var primeiraMusica = new RacionaisMCs("Vida Loka");
var segundaMusica = new RacionaisMCs("Jesus Chorou");

console.log(primeiraMusica.getInfo()); 
console.log(segundaMusica.getInfo());
```
Este exemplo acima tem não é a melhor maneira de criar objetos, pois sofre alguns problemas como fazer herança de 
forma dificil e performance pois o método `getInfo` é recriado e adicionado na memória toda vez que criamos um objeto do tipo `RacionaisMC`

Como resolver isso? Com `prototype`!

### Construtores com Prototype

Para quem não sabe o JavaScript é uma linguagem prototype-based. O que isso quer dizer? Quer dizer que ela é baseada em protótipos : `Cada objeto tem um link interno para um outro objeto chamado prototype. Esse objeto prototype também tem um atributo prototype, e assim por diante até que null seja encontrado como prototype (como em uma implementação de fila em C, por exemplo). null, por definição, não tem prototype, e age como um link final em um encadeamento de protótipos (prototype chain).`

Quando instanciamos um objeto, este já tem uma referência`(__proto__)` para o prototype da função que o construiu  . Ou seja, [só haverá um método na memória](http://javascript.crockford.com/private.html): o definido no prototype da função construtora! Assim ganhamos em memória e performance.

Sendo assim daqui pra frente vamos adotar o uso do prototype em nossas funções. Continuando nossa Classe ficaria assim:

```javascript
// A RacionaisMCs "class"
function RacionaisMCs( music ) {
   this.music = music;
   this.year = "2014";
 };
 // Adicionando comportamento a classe
 RacionaisMCs.prototype.getInfo = function () {
   return this.music + " " + this.year;
 };

```
Agora temos uma única instância de `getInfo` que pode ser compartilhado entre todos objetos de `RacionaisMCS`


[ << Voltar](README.md)