# Ping Pong
Nesse repositório irei apresentar como foi feito um simples jogo de ping pong
em javascript para a conclusão de um módulo da disciplina de informática e
robótica do 3 ano do ensino médio. 

## Definição de variavéis importantes

```javascript
let xBolinha = 300;
let yBolinha = 200;
let diametro = 15;
let raio = diametro / 2 ;
```

Nesse bloco declaramos a posição inical da bolinha com as variaveis xBolinha e
yBolinha(posição horizontal e vertical no plano) assim como seu diametro e por
consequencia seu raio, ambas variaveis importantes para a construção do tamanho
desejado da bolinha.

```javascript
//velocidade da bolinha
let velocidadeXBolinha = 5; // velocidade com que a bolinha anda horizontalmente
let velocidadeYBolinha = 5; // velocidade com que a bolinha anda verticalmente
```

Aqui declaramos a velocidade com que a bolinha se movera tanto horizontalmente,
tanto verticalmente.

```javascript
let xRaquete = 5;
let yRaquete = 150;
let raqueteComprimento = 10;
let raqueteAltura = 90;
let colidiu = false;
```
Um jogo de ping pong não se resume apenas a bolinha, logo, aqui declaramos
variaveis para a construção da raquete do jogo, assim como uma variavel que
sera utilizada para quando a bolinha encostar na raquete.

```javascript
//Placar do jogo
let meusPontos = 0;
let pontosDoOponente = 0;
```

Aqui é declarado os pontos de cada participante, que sera mudado com o desenrolar do jogo.

```javascript
//variaveis do oponente 
let xRaqueteOponente = 585
let yRaqueteOponente = 150
let velocidadeYOponente;
```

Aqui declaramos as variaveis que darão a posição inicial da raquete do adversário.

## a 

Aqui criamos os espaço que sera criado o jogo.
```javascript
function setup() {
	createCanvas(600, 400);
}
```

```javascript
function draw() {
	background(0);
	mostraBolinha();
	movimentaBolinha();
	verificaColisaoBorda();
	movimentaMinhaRaquete();
	verificaColisaoRaquete(xRaquete, yRaquete);
	mostraRaquete(xRaquete, yRaquete);
	mostraRaquete(xRaqueteOponente, yRaqueteOponente);
	movimenteRaqueteOponente();
	verificaColisaoRaquete(xRaqueteOponente, yRaqueteOponente)
	incluiPlacar(); 
	marcaPonto();
}
```

A função draw é a função principal deste programa, ela que colocara todas as
funções que desenvolveremos na tela. Nela tudo que precisa estar na tela
precisa esta declarada.

```javascript
function mostraBolinha(){
	circle(xBolinha, yBolinha, diametro);
}
```

Essa função criara a bolinha do jogo, utilizando dentro dela a função ~circle~
que recebe por padrão a posicão da bolinha e seu diametro.

```javascript
function movimentaBolinha(){
	xBolinha += velocidadeXBolinha;
	yBolinha += velocidadeYBolinha;
}
```

Essa função sera responsavel pela movimenção da bolinha. Por meio do incremento
dos valores xBolinha e yBolinha que a fara se mover pela tela com a velocidade
antes declarada.

```javascript
function verificaColisaoBorda(){
	if (xBolinha + raio> width || xBolinha - raio< 0){
		velocidadeXBolinha *= -1;
	}
	if (yBolinha + raio> height || yBolinha - raio < 0){
		velocidadeYBolinha *= -1;
	}
}
```

Essa função verifica se houve colisão da bolinha com qualquer das bordas do
plano, e então, a fazendo ir para o lado oposto multiplicando o valor da
velocidade da bolinha por -1, assim a fazendo ir para o lado oposto.

```javascript
function mostraRaquete(x,y){
	rect (x, y, raqueteComprimento, raqueteAltura)
}
```

Aqui é função que fara a raquete aparecer na tela do jogador, ela recebe os
valores x,y(que serão definidos ao uso da função) e as variaveis ja definidas
anteriormente da altura e comprimento das raquetes, e as utiliza para a criação
de um retangulo com a função rect.

```javascript
function movimentaRaqueteOponente() {
	if (keyIsDown(87)) {
		yRaqueteOponente -= 10;
	}
	if (keyIsDown(83)) {
		yRaqueteOponente += 10;

	}
}
```

Esta é responsavel pela movimentação da raquete do adversário por meio de uma
condicional que checara os botões presionados pelo jogador e movera a raquete
como o esperado.

Vale lembrar que os valores das teclas pressionadas é dada pela keycode que
cada tecla recebe, neste caso o número 87 para a tecla W e o número 83 para a
tecla S.

```javascript
function movimentaMinhaRaquete() {
	if (keyIsDown(UP_ARROW)) {
		yRaquete -= 10;
	}
	if (keyIsDown(DOWN_ARROW)) {
		yRaquete += 10;
	}
}
```

Agora a vez do outro jogador.

```javascript
function verificaColisaoRaquete(x, y) {
	colidiu = collideRectCircle(x, y, raqueteComprimento, raqueteAltura, xBolinha, yBolinha, raio);
	if (colidiu) {
		velocidadeXBolinha *= -1;
	}
}
```
Aqui é verificada a colisão da bolinha com a raquete, assim a fazendo se mover
para o lado oposto quando a colisão acontecer.

```javascript
function  movimenteRaqueteOponente(){
	velocidadeYOponente = yBolinha - yRaqueteOponente - raqueteComprimento /2 -30;
	yRaqueteOponente += velocidadeYOponente
}
```
Aqui é a criação de uma função que, caso o jogador não mova a raquete do
oponente, fara com que a raquete do adversário se mova em direção a bolinha.

```javascript
function incluiPlacar(){
	stroke(255);
	textAlign(CENTER);
	textSize(16);
	fill(color(86, 89, 89));
	rect(150, 10, 40, 20);
	fill(255);
	text(meusPontos, 170, 26);
	fill(color(86, 89, 89));
	rect(450, 10, 40, 20);
	fill(255);
	text(pontosDoOponente, 470, 26);
}
```
Aqui uma simples função que utiliza uma serio de funções de texto para exibir o
placar da partida.

```javascript
function marcaPonto() {
	if (xBolinha > 591) {
		meusPontos += 1;
	}
	if (xBolinha < 9) {
		pontosDoOponente += 1;
	}
}
```
E por fim, a contabilização dos ponsto de acordo com a posição x da bolinha.
