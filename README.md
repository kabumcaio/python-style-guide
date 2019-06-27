# Python Style Guide

## Conteúdo

  1. [Tipos](#tipos)
  2. [Referências](#referências)
  3. [Dicionários](#dicionários)
  4. [Listas](#listas) 
  5. [Strings](#strings)

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


    number_list = [
        1, 2,
    ]

    # good
    items = [[0, 1], [2, 3], [4, 5]]

    dict_list = [
        {'id': 1},
        {'id': 2},
    ]

    number_list = [1, 2]

    number_list = [
        1,
        2,
    ]
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