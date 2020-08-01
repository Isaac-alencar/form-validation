# Validação de Formulários com HTML e CSS

Pequeno formulário para demonstrar recursos de HTML e CSS para lidar com a validação de formulários diretamente no Front-End. É muito importante que o Front-end seja responsável por filtrar a maioria das informações erradas em inputs de senhas e emails(por exemplo), pois, desta forma, o Back-end se beneficia por não precisar de muito tempo para processar os dados recebidos.

## Vantagens de usar esses recursos

- Filtro das informações que serão recebidas no Back-end;
- **O Usuário agradece**, pois assim tudo fica claro em relação ao que deve ser preenchido naquele campo. Especialmente se ele tiver que conter muitos caractéres específicos

# Getting started

### Validando Campo de Email

```html
<div>
  <label for="email">Email</label
  ><input type="email" required id="email" spellcheck="false" placeholder=" " />

  <!--
    spellcheck, atributo utilizado para desativar a verificação de ortografia. 
    Covenhamos que é muito chato você ver aquele tipo de erro que é exibido ao digitar endereços
    de email.

    O básico para validar um formulário é que cada campo seja obrigatório(a menos que ele realmente não seja), portanto a tag input disponibiliza um atributo chamado "required" que torna o campo obrigatório. Por si só, ele não tem muito efeito, pois se em um campo de email for enviado, por exemplo, "fdfagdfadhfgdajf" o usuário não vai conseguir logar ou se cadastrar.

    Então, por isso, existe o atributo type, que aplica um certo nível de filtro sobre o que está sendo digitado. Exigindo, por exemplo, um "@" e um ".algo' nos campos type="email".

    -->

  <div class="requirements">Digite um email válido.</div>
</div>
```

### Validando campo de senha

```html
<div>
  <label for="password">Password</label>
  <input
    type="password"
    required
    id="password"
    placeholder=" "
    pattern="(?=.*\d)(?=.*[a-z])(?=.*[A-Z]).{6,}"
  />
  <!-- 
    pattern, atributo usado para definir uma nova expressão regular 
    para validar a senha com especificações como tamanho, e caracteres obrigatórios  -->
  <div class="requirements">
    Sua senha deve ter no mínimo 6 caractéres, sendo ao menos uma letra
    maiúscula, uma minúscula e um número.
  </div>
</div>

<!-- No caso específico do password, além de utilizarmos o atributo type="password"
para ocultar os caracteres digitados pelo usuário, podemos acrescentar o atributo pattern que define uma expressão regular (se você não conhece, pesquise sobre), em que especificamos tamanho mínimo da senha, caracteres desejados para que a senha seja forte o suficiente -->
```

# Melhorando a experiência do usuário com CSS

Pra melhorar a experiência do usuário quando o assunto é formulários, é necessário utilizar recursos visuais que mostre ao usuário qunado ele está digiitando algo corretamente ou quando está digitando algo errado. Assim como, alguma mensagem que mostre o motivo do erro.

### Input sem nenhum dado

```css
/*
  A pseudo-classe CSS de negação, :not(X) é uma notação funcional que recebe um seletor simples X como argumento. Ela seleciona um elemento que não é representado por seu argumento. X não pode conter outro seletor de negação. 

  No trecho abaixo foi utilizado a combinação de :invalid:not(:focus), pois quando você utiliza somente :invalid() o simples fato de não conter nenhum dado, já o torna inválido e quando você adiciona o 
  :not(:focus) indica que ele terá a estilização a seguir se, e somente se, o input não estiver em foco.

*/
/*
  Note que usei o :invalid(), a pseudo-classe CSS :invalid representa qualquer <input> ou outro elemento do <form> cujo conteúdo não foi validado com sucesso. Isso permite, facilmente, adicionar uma aparência que ajude o usuário a identificar os campos inválidados.

  Isso só é possível graças a atributos como pattern e type, que atuam como um verificador dos dados que estão sendo informados pelo usuário.
 */

/* Estilização do input de email e senha, qundo não estão em foco (aparência padrão) */
.bg-color .form-sign-in form input,
.bg-color .form-sign-in form input:invalid:not(:focus) {
  width: 290px;
  margin: 0 auto 20px;
  padding: 11px;
  border: 1px solid var(--border);
  border-radius: 5px;
}
```

### Entradas válidas e inválidas do usuário

```css
/* Sem muitas cerimônias o seletor :valid() funciona de forma silimar ao :invalid(), contudo como o nome sugere, ele representa qualquer elemento <input> ou outro elemento do <form> que foi validado com sucesso */

/* Estilização de como o input deve se comportar quando estiver tudo correto, 
gerando um respaldo visual, quando o que está sendo digitado foi validado com sucesso */
.bg-color .form-sign-in form input:valid {
  background: url(/assets/ckeck.svg);
  background-size: 18px;
  background-repeat: no-repeat;
  background-position: 265px 10px;
  border: 1px solid #3bb54a;
}

/* Estilização de como o input deve se comportar quando estiver tudo errado  */
.bg-color .form-sign-in form input:invalid:focus:not(:placeholder-shown) {
  background: url(/assets/error.svg);
  background-size: 18px;
  background-repeat: no-repeat;
  background-position: 265px 10px;
  border: 1px solid #e21b1b;
}

/* No trecho de código acima é mais uma estratégia combinando seletores para estilizar quando a entrada de dados pelo usuário não é válido.

:invalid:focus:not(:placeholder-shown), foi utilizado da seguinte forma.

1- :ivalid() - Para identificar o erro;
2- :focus()  - Para indicar que o usuário está com o foco no input em questão;
3- :not(:placeholder-shown) - Que só terá efeito caso o placeholder não esteja sendo exibido. E quando o placeholder não está sendo exibido? Exatamente, quando algo está sendo digitado. Por isso ele é o mais importante pois sem ele, como mencionado anteriormente, o simples fato de não existir algo digitado já torna o campo inválido.

*/
```

### Mensagem de Erro

```css
/* No código abaixo foi definido como a mensagem deve aparecer para o usuário, lógico quando, enquanto o que ele estiver digitando estiver incorreto para o que o input pede */

/* Estilização de como o input deve se comportar quando estiver tudo errado  */
.bg-color .form-sign-in form input:invalid:focus:not(:placeholder-shown) {
  background: url(/assets/error.svg);
  background-size: 18px;
  background-repeat: no-repeat;
  background-position: 265px 10px;
  border: 1px solid #e21b1b;
}

/* Aqui, a propriedade max-height do .requirements é definida com um valor diferente do inicial, 
para que quando tenha algum erro no texto digitado no input, a mensagem seja exibida */
.bg-color
  .form-sign-in
  form
  input:invalid:focus:not(:placeholder-shown)
  ~ .requirements {
  max-height: 200px;
}

/* 
  Sobre o seletor ~ 

  O ~ só selecionará o primeiro elemento, imediatamente, após o elemento inicial, esse é mais generalista. Ele selecionará, usando o nosso exemplo acima, qualquer elemento .requirements, desde que ele venha depois de um elemento .bg-color .form-sign-in form input:invalid:focus:(:placeholder-shown).
*/
```
