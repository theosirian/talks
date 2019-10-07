---
title: Flutter Adventures
subtitle: Construindo uma Pokédex com Flutter
date: Outubro, 2019
author:
- Tiago Nascimento,
- Ricardo Brunetto
---

## What?

Flutter é um framework de desenvolvimento de aplicativos open-source mantido pela Google.

Seu principal característica  é a possibilidade de desenvolver uma  vez e exportar tanto para iOS,  quanto para Android,
sem perda de performance nativa.

## How?

Uma das  maneiras empregadas pelo  principal competidor nessa  área multi-plataforma, o React  Native, é de  utilizar um
motor javascript para executar seu código e traduzí-lo em componentes e chamadas de cada sistema operacional.

## How?

O Flutter  usa outra abordagem, seu  código, escrito na linguagem  Dart, é transpilado para  C ou C++ e  então compilado
nativamente para cada sistema operacional com NDK (Android) ou LLVM (iOS).

## Why?

Isso mantém a facilidade  de escrever apenas um código e  gerar dois produtos finais, sem perda  de performance nativa e
sem muitos dos problemas de incosistências de interface originadas da tradução, como no React Native.

## Dart

A linguagem Dart  é uma linguagem orientada a  objetos, tal como Java, C#  e C++. Ela possui um  motor de interpretação,
utilizado pelo  Flutter para  trazer o `hot-reload`  para seu arsenal  de desenvolvimento,  ou seja, além  de perfomance
nativa, também é possível iterar rapidamente sem precisar recompilar, como foi popularizado pelo desenvolvimento Web com
Javascript.

## Flutter

O framework já possui várias bibliotecas úteis: 

- Material Design;
- Cupertino;
- Interação nativa:
  - Bluetooth, Câmera, GPS, etc;
- Componentes de UI variados.

## Componentes

A unidade básica de uma aplicação Flutter é um `Widget`.

Ele pode ser de três tipos básicos:

- Stateless
- Stateful
- Inherited

## Stateless

Um `StatelessWidget` é um componente de UI que não gerencia nenhum tipo de estado.

## Stateful

Um `StatefulWidget` é um componente de UI que gerencia estado.

Para construí-lo são necessárias duas classes:

- `StatefulWidget` e
- `State<T>`.

## Inherited

Um `InheritedWidget`  é um componente  não-visual que está  na árvore para  disponibilizar dados e  funcionalidades para
todos os seus filhos.

Um exemplo disso é a configuração do tema Material que seu aplicativo utilizará.

Geralmente será possível  ter vários `InheritedWidget`s ao longo da  sua árvore, sendo que os componentes  de nível mais
baixo sobrescrevem os de níveis superiores. Sendo possível, por  exemplo, trocar o tema Material em uma seção específica
do seu aplicativo.

## POC

Nosso  objetivo nesse  curso  será implementar  uma  Pokédex  simples, com  informações  obtidas de  uma  API remota,  a
`http://pokeapi.co`.

## Professor Oak

> Your very own Pokémon adventure is about to unfold!

> A world of dreams and adventures with Pokémon awaits!

> Let's go!
