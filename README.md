# Python Style Guide

## Conteúdo

  1. [Tipos](#tipos)
  2. [Referências](#referências)
  3. [Dicionários](#dicionários)
  4. [Listas](#listas) 
  5. [Strings](#strings)
  6. [Funções](#funções)

## Tipos

  <a name="tipos--primitivos"></a><a name="1.1"></a>
  - [1.1](#tipos--primitivos) **Primitivos**: Quando você acessa um tipo primitivo você trabalha direto com seu valor.

    - `string`
    - `number`
    - `boolean`
    - `None`
    
    <br>

    ```python
    foo = 1
    bar = foo

    bar = 9

    print(foo, bar) # => 1, 9
    ```

  <a name="tipos--complexos"></a><a name="1.2"></a>
  - [1.2](#tipos--complexos)  **Complexos**: Quando você acessa um tipo complexo você trabalha com a sua referência.

    - `dict`
    - `list`
    - `function`

    <br>

    ```python
    foo = [1, 2]
    bar = foo

    bar[0] = 9

    print(foo[0], bar[0]) # => 9, 9
    ```

**[⬆ voltar ao topo](#conteúdo)**

## Referências

  <a name="referencias--prefer-const"></a><a name="2.1"></a>
  - [2.1](#referencias--prefer-const) Python não tem um tipo `constant`, então você precisa se atentar à convenção de sempre utilizar os nomes em UPPERCASE e nunca modificá-los.

    > Por que? Isso garante que você não altere o valor da constante, evitando bugs e não dificultando a compreensão do código.

    ```python
    # bad
    foo = 1
    bar = 2

    # good
    FOO = 1
    BAR = 2
    ```

**[⬆ voltar ao topo](#conteúdo)**

## Dicionários

  <a name="dicionarios--literal"></a><a name="3.1"></a>
  - [3.1](#dicionarios--literal) Use a sintaxe literal para declaração de um dicionário.

    ```python
    # bad
    item = dict()

    # good
    item = {}
    ```

  <a name="dicionarios--spread"></a><a name="3.2"></a>
  - [3.2](#dicionarios--spread) Use spread `**` ao invés de `copy()` para copiar e extender dicionários.

    ```python
    # bad
    original = {'a': 1, 'b': 2}
    clone = original.copy()
    clone.update({'c': 3})

    # good
    original = {'a': 1, 'b': 2}
    clone = {**original, 'c': 3}

    # good
    original = {'a': 1, 'b': 2}
    original_2 = {'c': 3, 'd': 4}
    long_clone = {**original, **original_2, 'e': 5}
    ```

  <a name="dicionarios--newline"></a><a name="3.3"></a>
  - [3.3](#dicionarios--newline) Se o dicionário tiver mais de um item, utilize sempre uma quebra de linha antes e depois do conteúdo do dicionário.

    ```python
    # bad
    single_map = {
        'a': 1,
    }

    # bad
    item_map = {
        'a': 1, 'b': 2, 'c': 3,
    }

    # good
    single_map = {'a': 1}

    item_map = {
        'a': 1,
        'b': 2,
        'c': 3,
    }
    ```

  <a name="dicionarios--get"></a><a name="3.4"></a>
  - [3.4](#dicionarios--get) Use `dict.get(key)` para acessar um item do dicionário.

    > Por que? Usando `dict[key]` seu código irá quebrar ao tentar acessar uma key inexistente no dicionário, e isso requere validações desnecessárias ao tentar acessar um item.

    ```python
    item_map = {
        'a': 1,
        'b': 2,
    }

    # bad - KeyError 'c' não existe
    item_map['c']

    # bad
    try:
        item_map['c']
    except KeyError:
        item_map['c'] = 3
        return item_map['c']

    # good
    item_map.get('c')

    # good
    item_map['c'] = item_map.get('c') or 3
    ```

**[⬆ voltar ao topo](#conteúdo)**

## Listas

  <a name="listas--literal"></a><a name="4.1"></a>
  - [4.1](#listas--literal) Usa a sintaxe literal para a declaração de uma lista.

    ```python
    # bad
    items = list()

    # good
    items = []
    ```

  <a name="listas--spreads"></a><a name="4.2"></a>
  - [4.2](#listas--spreads) Use spreads `*` para copiar e extender listas.

    ```python
    # bad
    items = ['a', 'b']
    clone = items.copy() + ['c']

    # good
    items = ['a', 'b']
    clone = [*items, 'c']

    # good
    items = ['a', 'b']
    items_2 = ['c', 'd']
    clone = [*items, *items2, 'e']
    ```

  <a name="listas--newline"></a><a name="4.3"></a>
  - [4.3](#listas--newline) Sempre utilizar quebra de linhas antes e depois do conteúdo da lista caso ela contenha mais de uma linha.

    ```python
    # bad
    items = [
        [0, 1], [2, 3], [4, 5],
    ]

    # bad
    dict_list = [{
        'id': 1
    }, {
        'id': 2
    }]

    # bad
    number_list = [
        1, 2,
    ]

    # good
    items = [[0, 1], [2, 3], [4, 5]]

    # good
    dict_list = [
        {'id': 1},
        {'id': 2},
    ]

    # good
    number_list = [1, 2]

    # good
    number_list = [
        1,
        2,
    ]
    ```

  <a name="list-comprehension"></a><a name="4.3"></a>
  - [4.4](#list-comprehension) Utilizar list comprehension sempre que possível

    ```python
    # bad
    my_input_numbers = [1, 2, 3, 4, 5, 6, 7, 8]
    for number in my_input_numbers:
        if number % 2 != 0:
            my_odd_numbers.append(number)

    #good
    my_input_numbers = [1, 2, 3, 4, 5, 6, 7, 8]
    my_odd_numbers = [x for x in my_input_numbers if x % 2 != 0]

    ```

**[⬆ voltar ao topo](#conteúdo)**

## Strings

  <a name="strings--quotes"></a><a name="5.1"></a>
  - [5.1](#strings--quotes) Use aspas simples `''` para strings.

    > Por que? Menos necessidade de "escapar" caracteres, código mais limpo e mais fácil de realizar buscas.

    ```python
    # bad
    name = "Kabum Comércio Eletrônico S.A."

    # bad
    json_string = "{\"a\": 1}"

    # good
    name = 'Kabum Comércio Eletrônico S.A.'

    # good
    json_string = '{"a": 1}'
    ```

  <a name="strings--line-length"></a><a name="5.2"></a>
  - [5.2](#strings--line-length) Strings que ultrapassem 79 caracteres não devem conter quebra de linhas utilizando concatenação de strings.

    > Por que? Strings com quebra de linha utilizando concatenação deixa o código mais poluído e dificulta a busca.

    ```python
    # bad
    error_msg = 'This is a super long error that was thrown because \
    of Batman. When you stop to think about how Batman had anything to do \
    with this, you would get nowhere \
    fast.'

    # bad
    error_msg = 'This is a super long error that was thrown because ' + \
        'of Batman. When you stop to think about how Batman had anything to do ' + \
        'with this, you would get nowhere fast.'

    # good
    error_msg = 'This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.'
    ```

  <a name="template-literais"></a><a name="5.3"></a>
  - [5.3](#template-literais) Quando construir strings programaticamente, utilizar `format()` ao invés de concatenação.

    ```python
    # bad
    def hello(name):
        return 'Hello, ' + name + '!'

    # bad
    def hello(name):
        return ''.join(['Hello, ', name, '!'])

    # good
    def hello(name):
        return 'Hello, {}!'.format(name)
    ```

    ```python
    a = 1
    b = 2
    c = 3

    'a: {} b: {} c: {}'.format(a, b, c)

    'a: {a} b: {b} c: {c}'.format(a=a, b=b, c=c)

    param = {'a': a, 'b': b, 'c': c}
    'a: {a} b: {b} c: {c}'.format(**param)

    ```

  <a name="strings--eval"></a><a name="5.4"></a>
  - [5.4](#strings--eval) Nunca use `eval()` em uma string, fazer isso abre muitas [vulnerabilidades](https://nedbatchelder.com/blog/201206/eval_really_is_dangerous.html) no código.

  <a name="strings--escaping"></a><a name="5.5"></a>
  - [5.5](#strings--escaping) Não "escape" strings desnecessariamente. 
    > Barras invertidas atrapalham a leitura do código, por isso só use quando for necessário.


    ```python
    # bad
    foo = '\'this\' \i\s \"quoted\"'

    # good
    foo = '\'this\' is "quoted"'
    ```

**[⬆ voltar ao topo](#conteúdo)**

## Funções

  <a name="parametros-default"></a><a name="6.1"></a>
  - [6.1](#parametros-default) Use parâmetros com valor default ao invés de alterar o parâmetro da função

    ```python
    # really bad
    def do_something(opt):
        # Não devemos alterar o valor dos parâmetros da função.
        opt = opt or 'foo'
        # ...

    # still bad
    def do_something(opt):
        if (opt is None):
            opt = 'foo'
        # ...

    # good
    def do_something(opt='foo'):
        # ...
    ```

  <a name="parametros-default-nao-complexos"></a><a name="6.2"></a>
  - [6.2](#parametros-default-nao-complexos) Não use tipos complexos como parâmetros default.

    > Por que? Como vimos [aqui](#tipos--complexos), uma variável de tipo complexo é uma referência, ou seja, somente uma única instância dessa referência vai ser alterada.

    ```python
    # bad
    def init_list(value, new_list=[]):
        new_list.append(value)
        return new_list

    init_list(1)
    # => [1]
    init_list(2)
    # => [1, 2]

    # good
    def init_list(value, new_list=None):
        if new_list is None:
            new_list = []
        new_list.append(value)
        return new_list

    init_list(1)
    # => [1]
    init_list(2)
    # => [2]
    ```

  <a name="assinatura--função-sem-espaços"></a><a name="6.3"></a>
  - [6.3](#assinatura--função-sem-espaços) Não utilizar espaços na assinatura da função

    > Por quê? Código mais legível e facilita nas buscas.

    ```python
    # bad
    def foo(a): print(a)
    def bar (b): print(b)

    # good
    def foo(a): print(a)
    def bar(b): print(b)
    ```

  <a name="funções--alterar-param"></a><a name="6.4"></a>
  - [6.4](#funções--alterar-param) Nunca altere o valor de um parâmetro de função.

    > Por que? Alterar o valor de um parâmetro pode ocasionar bugs e comportamentos inesperados.

    ```python
    # bad
    def fn_1(a):
        a = 1
        # ...

    # bad
    def fn_2(a):
        if (a > 10): a = 10
        # ...

    # good
    def fn_3(a):
        b = a or 10
        # ...

    # good
    def fn_3(a):
        b = a
        if (b > 1): b = 1
        # ...

    # good
    def fn_4(a=1):
        # ...
    ```

  <a name="funções--assinatura-indentação"></a><a name="6.5"></a>
  - [6.5](#funções--assinatura-indentação) Funções com assinatura em mais de uma linha devem ser indentadas como qualquer outra lista ou dicionário multilinha.

    ```python
    # bad
    def some_fn(foo,
                bar,
                baz):
        # ...

    # bad
    def some_fn(foo,
      bar,
      baz):
        # ...

    # good
    def some_fn(
        foo,
        bar,
        baz,
    ):
        # ...

    ```

  <a name="funções--param-nome"></a><a name="6.6"></a>
  - [6.6](#funções--param-nome) Utilize o nome do parâmetro ao chamar a função.

    > Por que? Fica mais claro qual o propósito daquela função e futuramente em uma necessidade de alterar a assinatura da função é menos provável que aconteça erros por utilizar "keyword arguments" ao invés de "normal arguments". [Veja aqui](https://treyhunner.com/2018/04/keyword-arguments-in-python/)

    ```python
    def move(x, y, roll=False):
        # ...

    # bad - não é claro o que a função faz
    move(1, 0, True)

    # good
    move(x=1, y=0, roll=True)

    # futuramente fica mais fácil adicionar novos parâmetros
    def move(x, y, z=0, roll=False):
        # ...
    ```

**[⬆ voltar ao topo](#conteúdo)**