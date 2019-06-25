# Python Style Guide

## Conteúdo

  1. [Tipos](#tipos)
  1. [Referências](#referências)
  1. [Dicionários](#dicionários)

## Tipos

  <a name="tipos--primitivos"></a><a name="1.1"></a>
  - [1.1](#tipos--primitivos) **Primitivos**: Quando você acessa um tipo primitivo você trabalha direto com seu valor.

    - `string`
    - `number`
    - `boolean`
    - `None`

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
  - [3.2](#dicionarios--spread) Prefira utilizar o conceito `spread` ao invés de `copy()` para copiar e extender dicionários.

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

  <a name="dictionaries--braces-newline"></a><a name="3.3"></a>
  - [3.3](#dictionaries--braces-newline) Se o dicionário tiver mais de um item, utilize sempre uma quebra de linha antes e depois do conteúdo do dicionário.

    ```python
    # bad - single item will not exceed one line
    single_map = {
        'a': 1,
    }

    # bad - single line
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

  <a name="dictionaries--use-get"></a><a name="3.4"></a>
  - [3.4](#dictionaries--use-get) Use `dict.get(key)` para acessar um item do dicionário.

    > Por que? Usando `dict[key]` seu código irá quebrar ao tentar acessar uma key inexistente no dicionário, e isso requere validações desnecessárias ao tentar acessar um item.

    ```python
    item_map = {
        'a': 1,
        'b': 2,
    }

    # bad - throws error
    item_map['c']

    # bad - bloated code
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
