# Mao-na-massa-aula-7-Javascript

Começando deste ponto ?
Começando deste ponto? Você pode fazer o download completo do projeto do capítulo anterior e continuar seus estudos a partir deste capítulo.

Mãos na Massa: Removendo os pacientes

Neste capítulos aprendemos mais sobre eventos e vimos que através da delegação de eventos conseguimos reduzir o número de eventListeners na página e ainda assim executar as funções que desejamos. Vamos implementar a remoção de pacientes colocando um escutador na tabela:

1- Nosso primeiro passo é criar um novo arquivo /js, já que se trata de uma nova funcionalidade vamos chamá-lo de remove-paciente.js:

    introducao-javascript
       └── js
           ├── calcula-imc.js
           ├── form.js
           └── remove-paciente.js
       
2- Não vamos esquecer de importar o nosso novo arquivo .js ao fim da tag <body>:

    //index.html
    </section>

    <script src="js/calcula-imc.js" ></script>
    <script src="js/form.js" ></script>
    <script src="js/remove-paciente.js" ></script>

    </body>

3- Agora vamos selecionar o corpo da tabela para adicionarmos um eventListener de duplo clique. Dentro do remove-paciente.js faça:

      // remove-paciente.js
      var tabela = document.querySelector("#tabela-pacientes");
      tabela.addEventListener("dblclick", function() {

      });

4- Agora devemos remover a linha que foi clicada, porém como o eventListener está na tabela, devemos perguntar primeiro qual das <td> que foi clicada, em seguida buscar pelo seu pai <tr> e removê-lo:

    // remove-paciente.js
    var tabela = document.querySelector("#tabela-pacientes");
    tabela.addEventListener("dblclick", function(event) {
        event.target.parentNode.remove();
    });

Não esqueça de adicionar o parâmetro event na função anônima do evento!

Agora ao dar um duplo clique no elemento, o evento sobe até a tabela, e dentro da função conseguimos perguntar qual td foi clicado (event.target) e partir disto subir para o seu pai (parentNode) que é a <tr> do paciente e removê-lá.

Dica
Não sei se você notou, mas se der um duplo clique no cabeçalho da nossa tabela, esta linha também será removida.

Podemos resolver isto de uma maneira simples. Pense um pouco... que elemento desejamos remover da tabela?

Sim, a tr pai do elemento em quem clicamos. Mas em que elemento estamos clicando? Estamos clicando dentro da "célula" da tabela, ou seja, no td.

Mas quando fazemos isto no cabeçalho, na realidade estamos clicando em um th.

Acho que você já pegou a lógica. Não queremos que o pai do th seja removido, somente o pai do td. Ou para tornar mais simples: somente remova o pai se o elemento clicado for um td.

Os elementos de nossa página possuem o atributo tagName que guarda uma string com o nome da tag do elemento. Faça um teste na página da Aparecida Nutrição, abra o console e execute document.querySelector('h1').tagName. O console te retornará o nome da tag do elemento em maiúsculo ("H1").

Em nosso caso queremos saber o nome da tag do elemento clicado, portanto segue a implementação:

var tabela = document.querySelector('#tabela-pacientes');

tabela.addEventListener('dblclick', function(event) {

    // Somente executará nosso código caso o elemento em que clicamos seja um <td>
    if (event.target.tagName == 'TD') {
        event.target.parentNode.remove()
    }
});

Pronto, agora a nutricionista não vai mais apagar o cabeçalho sem querer. Bom trabalho!
