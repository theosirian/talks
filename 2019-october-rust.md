---
title: Rust
subtitle: Confiabilidade e segurança
date: Outubro, 2019
author:
- Tiago Nascimento,
- Guilherme Chichanoski
---

## Propósito
Rust  é uma  linguagem de  programação de  sistemas que  se propõe  a equiparar  C e  C++ em  desempenho sem  sacrificar
características de linguagens de alto-nível, como facilidades  do paradigma funcional, sintaxe moderna, tipos genéricos,
além de optar por segurança por padrão.

## Hello World

Típico exemplo ~~bosta~~ de código

```rust
fn main() {
  println!("Hello, world!");
}
```

## Básicos
Criar uma variável

```rust
let x = 5;
```

## Básicos
Imutabilidade por padrão

```rust
let x = 5;
x += 1;
```

Produz um erro ao tentar reatribuição

```
error[E0384]: cannot assign twice to immutable variable `x`
  |     let x = 5;
  |         - first assignment to `x`
  |     x += 1;
  |     ^^^^^^ cannot assign twice to immutable variable
in order to modify them, you need to say they're mutable:
```

## Váriaveis
Para modificar uma variável é necessário declará-la como mutável

```rust
let mut x = 5;
x += 1;
```

## Variáveis
Rust é estaticamente tipado, mas tem inferência de tipos

```rust
let x = 5;
let x: i32 = 5;
let x = 5i32;
```

## Tipos primitivos
Alguns dos tipos primitivos disponíveis

- **Booleans**: `true` e `false`
- **Inteiros**: *signed* e *unsigned*, `u8`/`i8`, `u16`/`i16`, `u32`/`i32`, `u64`/`i64`, `u128`/`i128`, `usize`/`isize`
- **Floats**: `f32` e `f64`
- **Tuplas**: para agrupar tipos diferentes, `(i32, f32, bool)`
- **Vetores de tamanho fixo**: `[u32; 4]`, e.g. `[1, 2, 3, 4]`
- **Referências**: ponteiros seguros, `&u32` e `&mut u32`
- **Slices**: partes de um vetor, `&[u32]`
- **char**: um único **_Unicode Scalar Value_**, `'☺'`
- **&str**: uma string UTF-8 imutável, `"emoji: ☺"`

## Funções
Na declaração de funções é um dos poucos lugares onde é obrigatório declarar os tipos, para que a inferência funcione

```rust
fn add_one(x: i32) -> i32 {
  x + 1
}
```

Como tudo é uma expressão, na versão acima o retorno é a própria expressão

Mas também existe a keyword `return`, como visto abaixo

```rust
fn add_one(x: i32) -> i32 {
  return x + 1;
}
```

## Print
O macro de print também pode ser usado com interpolação e formatação de valores

```rust
println!("Um número: {} e outro número: {}", 42, 100);

println!("Display: {}", "hello"); // printa "Display: hello"
println!("Debug: {:?}", "hello"); // printa "Debug: "hello""
```

## Comentários

Regular comments for your own use:

```rust
// Comentando a gambiarra

/// Comentário de documentação da função `foo`.
///
/// Você pode usar o  `rustdoc` por meio do `cargo doc` pra
/// gerar documentação em HTML a partir destes comentários!
fn foo() {
    // ...
}
```

## Condicional

Expressões condicionais

```rust
if something {
    println!("it was true!");
} else {
    println!("it was false");
}
```

Em Rust não há um operador ternário dedicado

Mas como tudo é uma expressão

```rust
let power = if too_powerful { 0 } else { 100 };
```

## Loops

```rust
// for
for i in 0..5 {
    println!("{}", i);
}
let list = [1, 5, 3, 17];
for i in &list {
    println!("{}", i);
}
```

## Loops

```rust
// while
let mut done = false;
let mut i = 0;
while !done {
    // do stuff with i
    if i > 5 { done = true; }
}
```

## Structs

```rust
struct Point {
    x: i32,
    y: i32,
}
let origin = Point {
    x: 0,
    y: 0,
};
```

## Enums

```rust
enum TrafficLight {
    Green,
    Yellow,
    Red,
}
let light = TrafficLight::Green;
```

## Métodos

```rust
struct Point {
    x: i32,
    y: i32,
}
impl Point {
    fn print(&self) {
        println!("({}, {})", self.x, self.y);
    }
}
let origin = Point { x: 0, y: 0 };
point.print(); // prints "(0, 0)"
```

## *Pattern Matching*

No `rust` não há o conceito de `switch case`, porem temos o match.

Com ele podemos fazer o seguinte:
``` rust
let x = 1;

match x {
    1 => println!("one"),
    2 => println!("two"),
    3 => println!("three"),
    _ => println!("anything"),
}
```

## *Pattern Matching*

É obrigatório satisfazer todas as possibilidades num bloco `match`.

``` rust
let x = Some(1); // enum Option<T> { Some(T), None }

match x {
    Some(e) => println!("{}", e)
}
```

## *Pattern Matching*

```
error[E0004]: non-exhaustive patterns: `None` not covered
 --> test.rs:4:11
  |
4 |     match x {
  |           ^ pattern `None` not covered
  |
  = help: ensure that all possible cases are being handled, possibly by adding wildcards or more match arms

error: aborting due to previous error

For more information about this error, try `rustc --explain E0004`.
```

## *Pattern Matching*

Mas também existe uma maneira de tratar todos os casos restantes de uma vez só.

``` rust
let x = Some(1); // enum Result<T> { Some(T), None }

match x {
    Some(1) => println!("11"),
    Some(2) => println!("22"),
    Some(e) => println!("{}", e),
    _ => println!("None")
}
```

## *Macros*

- declarativas;
- procedurais.

Provê geração de código a partir de anotações.

```rust
#[derive(Debug)] // procedural macro
struct VoidStruct;

fn main() {
    println!("Hello World!") // declarative macro
}
```

## *Macros*

```rust
#[macro_export]
macro_rules! vec {
    ( $( $x:expr ),* ) => {
        {
            let mut temp_vec = Vec::new();
            $(
                temp_vec.push($x);
            )*
            temp_vec
        }
    };
}

fn main() {
    let x = vec![1,2,3];
}
```

## Cargo
Cargo é uma ferramenta para ajudar no fluxo de desenvolvimento do Rust.

- `cargo build` pra compilar o projeto
- `cargo test` pra executar os testes
- `cargo run` pra compilar e executar
- `cargo new` pra inicializar um novo projeto
- `cargo init` pra inicializar um novo projeto em um diretório já existente

## *crates*

- Um programa ou biblioteca é chamado de *crate*
- Um pacote pode conter várias *crates*
- Você pode encontrá-los em http://crates.io/
- Você define suas dependências no `Cargo.toml`
- O arquivo `Cargo.lock` mantém as dependências do seu projeto

## *Zero Cost Abstraction*

Rust possui tipos  genéricos e interfaces, ou Traits,  para construir suas abstrações, mas não  sacrifica seu desempenho
por isso, já que tudo isso é resolvido em tempo de compilação.

## *Zero Cost Abstraction*

> C++ implementations  obey the zero-overhead principle: What you  don't use, you don't pay for  [Stroustrup, 1994]. And
> further: What you do use, you couldn't hand code any better. -- Stroustrup

## *Traits*
Traits são a única noção de interfaces no Rust.

## *Traits*
Traits podem ser despachadas estaticamente.

- Mas, ao contrário de C++ e seus templates, os traits são completamente type-checked resultando em
  - Erros mais esclarecedores
  - Menor overhead de compilação

## *Traits*
Traits podem ser despachadas dinâmicamente.

- Porque as vezes é necessária a indireção e resolução em tempo de execução

## *Traits*
Traits resolvem problemas além da abstração.

- Podem ser usados para "marcar" tipos
- Podem ser usados para definir extensões para tipos externos
- Previnem a necessidade de sobrecarga tradicional de métodos
- Tornam mais simples a sobrecarga de operadores

## *Traits*
Alguns exemplos de uso:

- Closures
- APIs Condicionais

```rust
struct Pair<A, B> { first: A, second: B }
impl<A: Hash, B: Hash> Hash for Pair<A, B> {
    fn hash(&self) -> u64 {
        self.first.hash() ^ self.second.hash()
    }
}
```

## *Traits*
Alguns exemplos de uso:

- Closures
- APIs condicionais
- Métodos de extensão
- Marcação
- Sobrecarga
  - Métodos
  - Operadores

## *Traits*
E no futuro, traits poderão também:

- Especialização
- Polimorfismo de Maior Ordem


## Tipos de Dados Algébricos

Rust traz tipos de dados  algébricos, que permitem uma flexibilidade muito grande na hora  de definir suas estruturas de
dados e enumerações.

Exemplo:
```rust
enum Option<T> {
  Some(T),
  None,
}
```

## Tratamento de Erros
Esses tipos algébricos contribuem para o tratamento de erros da linguagem.

Operações que falham optam por retornar um tipo genérico `Result<T, E>`.
```rust
enum Result<T, E> {
  Ok(T),
  Err(E),
}
```

## Tratamento de Erros
Dessa maneira você pode optar por tentar se recuperar da falha ou finalizar a execução.

Por exemplo, considerando o que segue:

```rust
enum MyError {
  Timeout,
  Other(String),
}
```

## Tratamento de Erros
```rust
mod example {
  pub fn get_input_with_timeout(
    timeout: std::time::Duration
  ) -> Result<usize, MyError> {
    [...]
  }
}
```

## Tratamento de Erros
```rust
fn main() {
  let timeout = std::time::Duration::from_secs(5);
  let res = example::get_input_with_timeout(timeout);

  if let MyError::Other(err) = res {
    panic!("Ocorreu um erro: {}", res);
  }

  let res = res.unwrap_or(0);
  
  println!("Você escolheu {}", res);
}
```

## Tratamento de Erros
Outra maneira de tratar os erros e tipos.

```rust
fn main() {
  let timeout = std::time::Duration::from_secs(5);
  let res = example::get_input_with_timeout(timeout);

  let res = match res {
    Ok(val) => val,
    Err(MyError::Timeout) => 0,
    Err(MyError::Other(err)) =>
      panic!("Ocorreu um erro: {}", err),
  };
  
  println!("Você escolheu {}", res);
}
```

## Ownership

```rust
fn make_vec() -> Vec<i32> {
    let mut vec = Vec::new();
    vec.push(0);
    vec.push(1);
    vec // transfere ownership para quem chamar
}
```

## Ownership

```rust
fn print_vec(vec: Vec<i32>) {
    // o parâmetro `vec` é parte deste escopo
    // então `print_vec` é seu dono

    for i in vec.iter() {
        println!("{}", i)
    }

    // agora, `vec` é desalocado
}
```

## Ownership

```rust
fn use_vec() {
    let vec = make_vec(); // obtem ownership do vetor
    print_vec(vec);       // transfere ownership pro `print_vec`
}
```

## *Borrow Checker*
Rust utiliza um sistema de *borrow checking* para conseguir garantir segurança sem sacrificar eficiência.

Existem dois tipos de referências:

- Referências compartilhadas (`&T`)
- Referências exclusivas (`&mut T`)

## *Borrow Checker*

```rust
struct Point(u32,u32);
let mut pt = Point(6, 9);
let x = pt;
let y = pt; // ERRO: pt já foi movido
```

## *Borrow Checker*

```rust
struct Point(u32,u32);
let mut pt = Point(6, 9);
let x = &pt;
let y = &pt; // sem erro, pt está sendo compartilhado
```

## *Borrow Checker*

```rust
struct Point(u32,u32);
let mut pt = Point(6, 9);
let x = &mut pt;
let y = &mut pt; // ERRO: pt só pode ser emprestado
                 // exclusivamente uma vez
... // resto do código usando x e y
```

## *Borrow Checker*

```rust
struct Point(u32,u32);
let mut pt: Point = Point(6, 9);
let x: &'a mut Point = &mut pt;
let y: &'b Point = &pt;
//                 ^~~
// ERRO: não é possível emprestar enquanto
// uma referência mutável está ativa
... // resto do código usando x e y
```

## *Borrow Checker*

```rust
struct Point(u32,u32);
let mut pt: Point = Point(6, 9);
let x: &'a mut u32 = &mut pt.0;
let y: &'b mut u32 = &mut pt.1;
// sem erro, a referência não intersecta
```

## *Borrow Checker*

```rust
struct Point(u32,u32);
let mut pt = Point(6, 9);
let x = &mut pt;
let y = &mut pt;
... // resto do código usando apenas y
```

# Dúvidas?

## Referências

- https://doc.rust-lang.org/book/
- https://docs.rs/dtolnay/0.0.6/dtolnay/
- https://steveklabnik.github.io/rust-in-ten-slides/getting-started.html
- https://steveklabnik.github.io/rust-in-ten-slides/basic-syntax.html
- https://blog.rust-lang.org/2015/04/10/Fearless-Concurrency.html
- https://blog.rust-lang.org/2015/05/11/traits.html
- Oxide: The Essence of Rust (https://arxiv.org/pdf/1903.00982.pdf)
