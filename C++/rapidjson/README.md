# RapidJSON

**RapidJSON** é uma biblioteca de alto desempenho para manipulação de JSON em C++. Ela permite fazer parsing, modificar e gerar JSON de forma eficiente, com suporte a encodings como UTF-8 e UTF-16, além de recursos como parsing in-situ para economia de memória. Ideal para aplicações que exigem processamento rápido de grandes volumes de dados.

[Site Oficial do RapidJSON →](https://rapidjson.org)

[Repositório no GitHub →](https://github.com/Tencent/rapidjson)

## Tópicos
- [RapidJSON](#rapidjson)
  - [Tópicos](#tópicos)
  - [Instalação](#instalação)
    - [Requisitos](#requisitos)
    - [Passos](#passos)
  - [Uso Básico](#uso-básico)
    - [Estrutura Básica](#estrutura-básica)
    - [Parsear JSON](#parsear-json)
      - [Inserido no C++](#inserido-no-c)
      - [Como String](#como-string)
      - [Como Stream](#como-stream)
    - [Criar JSON](#criar-json)
  - [Manipulação de Tipos](#manipulação-de-tipos)
    - [Verificar se um Membro Existe](#verificar-se-um-membro-existe)
    - [Verificar e Acessar Tipos](#verificar-e-acessar-tipos)
    - [Iterar Objetos](#iterar-objetos)
    - [Iterar Arrays](#iterar-arrays)
      - [Alternativa com Índices](#alternativa-com-índices)
  - [Tratamento de Erros](#tratamento-de-erros)
  - [Considerações de Desempenho](#considerações-de-desempenho)
  - [Exemplos Práticos](#exemplos-práticos)
    - [1. Parsear JSON de Arquivo (Baseado em R-c1.cpp)](#1-parsear-json-de-arquivo-baseado-em-r-c1cpp)
    - [2. Parsear JSON Inline (Baseado em R-c2.cpp)](#2-parsear-json-inline-baseado-em-r-c2cpp)
    - [3. Criar e Modificar JSON](#3-criar-e-modificar-json)
  - [Conclusão](#conclusão)

## Instalação

### Requisitos
- Compilador C++ moderno (ex.: g++ 13 com suporte a C++23, como nos seus exemplos).
- Sistema operacional: Windows, Linux, macOS.

### Passos
1. **Baixe a Biblioteca**  
   Clone o repositório ou baixe um release:
   ```bash
   git clone https://github.com/Tencent/rapidjson.git
   ```
2. **Inclua no Projeto**  
   - **Sem CMake**: Adicione o diretório `include` do RapidJSON ao caminho de inclusão (ex.: `-Irapidjson/include`) ou baixar o arquivo [rapidjson][rapidjson].
   - **Com CMake**: Adicione como subdiretório:
     ```cmake
     add_subdirectory(rapidjson)
     target_include_directories(seu_projeto PUBLIC rapidjson/include)
     ```
3. **Compilação**  
   Exemplo baseado nos seus anexos:
   ```bash
   $ g++-13 -O3 -std=c++23 -I..rapidjson/ ../arquivo.cpp
   
   $ time ./a.out
   ```

## Uso Básico

### Estrutura Básica
Inclua o header principal e, se quiser, use o namespace:
```cpp
#include "rapidjson/document.h"
using namespace rapidjson;  //Opcional
```

### Parsear JSON
RapidJSON oferece várias formas de parsear JSON, dependendo da origem dos dados. Abaixo estão os métodos mais comuns: diretamente no código, a partir de uma string e como um fluxo (stream).

- **Verificação de Erros**: Sempre use `HasParseError()` após o parsing para garantir que o JSON é válido.
```cpp
if (!d.HasParseError())
{
    std::cout << "Parsed from file: " << d["hello"].GetString() << std::endl; // Saída: world
} else
{
    std::cerr << "Parse error!" << std::endl;
}
```
- **Performance**: O modo "[Como Stream](#como-stream)" é ideal para JSONs grandes, enquanto "[Inserido no C++](#inserido-no-c)" e "[Como String](#como-string)" são melhores para dados menores ou embutidos.
- **Flexibilidade**: O método `Parse()` aceita tanto strings terminadas em `null` quanto ponteiros brutos, mas o uso correto depende do tipo de entrada.

#### Inserido no C++
Quando o JSON está embutido diretamente no código como uma string literal, você pode parseá-lo usando o método `Parse()` diretamente:

```cpp
Document d;
d.Parse("{\"hello\": \"world\"}");
```
- **O que faz?** Converte uma string JSON embutida no código em um objeto `Document`.
- **Nota**: Ideal para testes rápidos ou JSONs fixos.

#### Como String
Para parsear JSON armazenado em uma variável string (como `std::string` ou `std::string_view`), passe o conteúdo da string para o método `Parse()`. Use `.c_str()` para `std::string` ou `.data()` para `std::string_view`:

Para usar esse parse é necessário importar a lib `<string>` caso use a string ou `<string_view>` caso string_view seja usada.

```cpp
std::string json_string = "{\"name\": \"Alice\", \"age\": 25}";
Document d;
d.Parse(json_string.c_str());
```

- **O que faz?** Lê uma string JSON de uma variável e a converte em um objeto manipulável.
- **Variação com `std::string_view`**:
```cpp
const std::string_view json_view = "{\"name\": \"Bob\", \"active\": true}";
Document d;
d.Parse(json_view.data());
```
> **Nota**: Use `const std::string_view` para evitar cópias desnecessárias em JSONs grandes.

#### Como Stream
Para JSONs provenientes de arquivos ou outras fontes de entrada (como `std::ifstream`), você pode usar o modo de stream com `IStreamWrapper` para processar os dados incrementalmente, o que é útil para arquivos grandes:

Para usar esse parse é necessário importar a lib `"rapidjson/filereadstream.h"` e `<fstream>`.

```cpp
std::ifstream file("example.json"); // Suponha que example.json contém: {"hello": "world"}
if (!file.is_open())
{
    std::cerr << "Erro ao abrir o arquivo!" << std::endl;
    return 1;
}
Document d;
IStreamWrapper is(file);
d.ParseStream(is);
file.close();
```

- **O que faz?** Lê o JSON de um fluxo de entrada (como um arquivo) e o converte em um objeto `Document`.
- **Vantagem**: Eficiente para arquivos grandes, pois não carrega tudo na memória de uma vez.
- **Nota**: Inclua `rapidjson/filereadstream.h` para usar `IStreamWrapper`.

### Criar JSON
```cpp
Document d;
d.SetObject();
Value key("name", doc.GetAllocator());
Value value("Alice", doc.GetAllocator());
doc.AddMember(key, value, doc.GetAllocator());
```

## Manipulação de Tipos

### Verificar se um Membro Existe
```cpp
if (d.HasMember("hello")) {
    std::cout << "Chave 'hello' existe!\n";
}
```

### Verificar e Acessar Tipos
| Tipo     | Verificação  | Acesso                                  |
| -------- | ------------ | --------------------------------------- |
| String   | `IsString()` | `GetString()`                           |
| Inteiro  | `IsInt()`    | `GetInt()`                              |
| Double   | `IsDouble()` | `GetDouble()`                           |
| Float    | `IsFloat()`  | `GetFloat()`                            |
| Booleano | `IsBool()`   | `GetBool()`                             |
| Nulo     | `IsNull()`   | (nenhum)                                |
| Objeto   | `IsObject()` | Itera com `MemberBegin()`/`MemberEnd()` |
| Array    | `IsArray()`  | Itera com `GetArray()`                  |

**Exemplo:**
```cpp
Document d;
d.Parse(R"({ "name": "Pedro", "age": 25, "active": true })");
if (d["name"].IsString()) {
    std::cout << d["name"].GetString() << std::endl; // Pedro
}
if (d["age"].IsInt()) {
    std::cout << d["age"].GetInt() << std::endl;    // 25
}
```

### Iterar Objetos
Para percorrer os membros de um objeto JSON, você pode usar o método `GetObject()`, que retorna um iterador sobre os pares chave-valor. Isso é útil para acessar dinamicamente todas as propriedades de um objeto sem conhecer as chaves previamente.

```cpp
Document d;
d.Parse(R"({ "name": "Alice", "age": 25 })");
for (auto& member : d.GetObject())
{
    std::cout << member.name.GetString() << ": " << member.value.GetInt() << std::endl;
}
```

- **O que faz?** Itera sobre cada par chave-valor do objeto JSON.

---

### Iterar Arrays
Para percorrer os elementos de um array JSON, você pode usar o método `GetArray()`, que permite acessar os itens por índice. Nos seus códigos (R-c1.cpp e R-c2.cpp), você utiliza um loop com `Size()` e `GetArray()` para iterar, controlando manualmente a contagem de elementos restantes com uma variável (`j`). Aqui está uma adaptação desse método:

```cpp
Document d;
d.Parse(R"({ "numbers": [10, 20, 30, 40] })");
const Value& array = d["numbers"];
size_t j = array.Size();    // Número de elementos no array
for (auto& item : array.GetArray()) {
    std::cout << item.GetInt();
    if (j > 1) {
        std::cout << ", ";  // Adiciona vírgula se não for o último elemento
    }
    j--;
}
```

- **O que faz?** Itera sobre os elementos de um array JSON, usando `GetArray()` para acessar os itens e `Size()` para determinar o tamanho total.
- **Saída**: 
  ```
  10, 20, 30, 40
  ```
- **Nota**: O controle com `j` reflete seu estilo nos anexos, onde você decrementa uma variável para gerenciar separadores (como vírgulas). Isso é útil para formatar a saída manualmente.

#### Alternativa com Índices
Outra abordagem comum é usar índices diretamente com `Size()`:
```cpp
#include "rapidjson/document.h"
#include <iostream>
using namespace rapidjson;

int main() {
    Document d;
    d.Parse(R"({ "numbers": [10, 20, 30, 40] })");
    const Value& array = d["numbers"];
    for (SizeType i = 0; i < array.Size(); i++) {
        std::cout << array[i].GetInt();
        if (i < array.Size() - 1) {
            std::cout << ", ";
        }
    }
    std::cout << std::endl;
    return 0;
}
```

- **O que faz?** Usa um contador de índice (`i`) para acessar cada elemento do array.
- **Saída**: 
  ```
  10, 20, 30, 40
  ```
- **Nota**: Esta alternativa é mais explícita e pode ser mais clara para iniciantes, mas ambos os métodos são equivalentes em funcionalidade.

## Tratamento de Erros

Verifique erros de parsing:
```cpp
Document d;
d.Parse("invalido");
if (d.HasParseError()) {
    std::cerr << "Erro: " << GetParseError_En(d.GetParseError())
              << " na posição " << d.GetErrorOffset() << std::endl;
}
```


## Considerações de Desempenho

- **Parsing In-Situ**: Economiza memória ao modificar a string original:
  ```cpp
  char json[] = "{\"key\": \"value\"}";
  Document d;
  d.ParseInsitu(json);
  ```
- **Alocação**: Use `GetAllocator()` para evitar cópias desnecessárias.
- **Benchmarking**: Meça o desempenho (adaptado do seu código):
  ```cpp
  #include <chrono>
  auto start = std::chrono::high_resolution_clock::now();
  for (int i = 0; i < 1000000; ++i) {
      ParseJSON("{\"name\": \"Alice\"}");
  }
  auto end = std::chrono::high_resolution_clock::now();
  std::cout << "Tempo: " << std::chrono::duration_cast<std::chrono::milliseconds>(end - start).count() << " ms\n";
  ```

Seus anexos mostram interesse em desempenho, com loops de 1 milhão de iterações, indicando que RapidJSON é eficiente mesmo em cargas altas.


## Exemplos Práticos

### 1. Parsear JSON de Arquivo (Baseado em R-c1.cpp)
```cpp
#include <fstream>
#include "rapidjson/document.h"
int ParseJSON(const std::string& json_content) {
    rapidjson::Document d;
    d.Parse(json_content.c_str());
    return d.HasParseError() ? 1 : 0;
}
int main() {
    std::ifstream file("example.json");
    std::string json((std::istreambuf_iterator<char>(file)), std::istreambuf_iterator<char>());
    file.close();
    for (int i = 0; i < 1000000; ++i) {
        ParseJSON(json);
    }
    return 0;
}
```

### 2. Parsear JSON Inline (Baseado em R-c2.cpp)
```cpp
#include "rapidjson/document.h"
int ParseJSON(std::string_view json_content) {
    rapidjson::Document d;
    d.Parse(json_content.data());
    return d.HasParseError() ? 1 : 0;
}
int main() {
    const std::string_view json = R"({"name": "Alice", "age": 25})";
    for (int i = 0; i < 1000000; ++i) {
        ParseJSON(json);
    }
    return 0;
}
```

### 3. Criar e Modificar JSON
```cpp
#include "rapidjson/writer.h"
#include "rapidjson/stringbuffer.h"
int main() {
    Document d;
    d.SetObject();
    Document::AllocatorType& alloc = d.GetAllocator();
    d.AddMember("name", "Bob", alloc);
    d.AddMember("age", 30, alloc);
    Value array(kArrayType);
    array.PushBack(1, alloc).PushBack(2, alloc);
    d.AddMember("scores", array, alloc);
    StringBuffer buffer;
    Writer<StringBuffer> writer(buffer);
    d.Accept(writer);
    std::cout << buffer.GetString() << std::endl; // {"name":"Bob","age":30,"scores":[1,2]}
    return 0;
}
```

## Conclusão

RapidJSON é uma biblioteca robusta e eficiente para manipulação de JSON em C++. Este README cobre desde a instalação até exemplos avançados, aproveitando os códigos que você forneceu para ilustrar parsing e desempenho. Para mais detalhes, consulte a [documentação oficial](https://rapidjson.org/md_doc_tutorial.html).

[rapidjson]: https://github.com/pedcravo/Praticando-Cpp/tree/main/Desafios-do-Rodrigo/Parce-JSON/rapidjson