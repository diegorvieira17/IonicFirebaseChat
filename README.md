# IonicFirebaseChat

> Aplicativo simples de chat criado para demonstrar em aula como é simples construir um aplicativo sem a necessidade de um backend (ou melhor, com o backend facilitado) com o Firebase. Com ele conseguimos tratar nossos dados diretamente com o javascript. Abaixo preparei um resumo simples das principais funções do serviço.

> Com o firebase é bem simples constuirmos um app. Para "instalar" o banco basta utilizar uma das opções abaixo:

>>+ Inserir a referência ao js em seu projeto - <script src="https://cdn.firebase.com/js/client/2.4.1/firebase.js"></script>
>>+ Instalar localmente com o Bower - $ bower install firebase
>>+ Instalar o firebase com o Node - $ npm install firebase --save - E adicionar no projeto como dependência - var Firebase = require("firebase");

> O formato de dados também é extremamente simples. É apenas um array de chave: valor. Quem está acostumado com o json... Está em casa...

>>+ Ex.: {
           "users": {
             "mchen": {
               "friends": { "brinchen": true },
               "name": "Mary Chen",
               // our child node appears in the existing JSON tree
               "widgets": { "one": true, "three": true }
             },
             "brinchen": { ... },
             "hmadi": { ... }
           }
         }

> Tudo muito bom... Tudo muito bem... Mas como eu crio esse banco??? Simples... basta usar o comando abaixo:

>>+ new Firebase('[url do seu banco criado no site]');
>>>* Ex.: var meubanco = new Firebase('https://ionicfirebasechat.firebaseio.com/');

> Como incluir registros no banco?

>>+ set() - Escrever ou alterar registros no banco
>>>* Ex.: meubanco.set({ "usuario": "fulano" });

>>+ push() - Adiciona um novo registro (filho) ao banco
>>>* Ex.: meubanco.push({ "usuario": "beltrano" });

>>+ update() - Altera vários registros

> Como recuperar dados?

>>+ value - Retorna todo o conteudo do banco
>>>* Ex.: meubanco.value (retorna um array com todos os dados do banco)

>>+ child_added - Retorna um callback sempre que um filho for adicionado
>>>* Ex.: meubanco.on('child_added', function(snapshot) {
            var message = snapshot.val(); (nessa linha pegamos um snapshot do registro gravado no banco)
            alert("O registro" + message + "foi adicionado com sucesso!");
          });

>>+ child_changed - Igual ao child_added porém retorna o callback sempre que um registro for alterado
>>>* Ex.: myDataRef.on('child_changed', function(snapshot) {
            var message = snapshot.val();
            alert("O registro" + message + "foi alterado com sucesso!");
          });

>>+ child_removed - Igual aos anteriores porém retorna o callback sempre que um registro for excluido
>>>* Ex.: myDataRef.on('child_changed', function(snapshot) {
            var message = snapshot.val();
            alert("O registro" + message + "foi excluido com sucesso!");
          });

>>+ Temos também alguns comandos de query como "orderByChild()", "orderByKey()", "orderByValue()", "equalTo()" entre outros, mas não vou entrar em detalhes sobre eles.

>>+ Além dessas funcionalidades descritas, ainda temos outros diversos pontos interessantes como Segurança, Autenticação entre outros. Recomendo a leitura do guide do firebase no link https://www.firebase.com/docs/web/guide

