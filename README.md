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

    > Por que? Isso garante que você não altere o valor da constante, evitando bugs e dificuldade na compreensão do código.

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

  <a name="dictionaries--literals"></a><a name="3.1"></a>
  - [3.1](#dictionaries--literals) Use the literal syntax for dictionary creation.

    ```python
    # bad
    item = dict()

    # good
    item = {}
    ```

  <a name="computed-key"></a><a name="3.2"></a>
  - [3.2](#computed-key) Use computed key names when creating dictionaries with dynamic key names.

    > Why? They allow you to define all the key of a dictionary in one place.

    ```python

    def get_key(k):
        return f'a key named {k}'

    # bad
    obj = {
        'id': 5,
        'name': 'San Francisco',
    }
    obj[get_key('enabled')] = True

    # good
    obj = {
        'id': 5,
        'name': 'San Francisco',
        get_key('enabled'): True,
    }
    ```

  <a name="dictionaries--spread"></a><a name="3.3"></a>
  - [3.3](#dictionaries--spread) Prefer the dictionary spread operator over `copy()` to shallow-copy and extend dictionaries.

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

  <a name="dictionaries--braces-newline"></a><a name="3.4"></a>
  - [3.4](#dictionaries--braces-newline) Use line breaks after open and before close dictionary braces only if a dictionary has multiple lines.

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

  <a name="dictionaries--use-get"></a><a name="3.5"></a>
  - [3.5](#dictionaries--use-get) Use `dict.get(key)` to get properties.

    > Why? Getting via `dict[key]` will break on missing key, and requires bloated code to guard against.

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
