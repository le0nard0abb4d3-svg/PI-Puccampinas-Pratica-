Orientações para a Entrega
O exercício deverá ser desenvolvido com base nos conteúdos apresentados durante a aula prática sobre Listas e Tabelas em HTML.

O objetivo será construir uma página de Currículo Acadêmico, aplicando corretamente listas, tabelas semânticas, organização do conteúdo, acessibilidade e boas práticas de SEO.

Criar o arquivo:

curriculo.html

1. Cabeçalho da Página
Criar o cabeçalho principal do currículo.

Deve conter:

<h1> com o nome completo do aluno

<p> com uma breve descrição, objetivo profissional ou frase de apresentação

2. Habilidades Técnicas
Criar uma seção denominada:

Habilidades Técnicas

Deve utilizar:

<h2>

<ul>

no mínimo 5 habilidades técnicas utilizando <li>

Exemplos:

HTML

CSS

JavaScript

Python

Banco de Dados

3. Cursos e Certificações
Criar uma seção denominada:

Cursos/Certificações

Deve utilizar:

<h2>

<ol>

no mínimo 3 cursos ou certificações

organizar os itens em ordem de relevância

utilizar type="I" para apresentar a numeração em algarismos romanos

4. Glossário Acadêmico
Criar uma seção denominada:

Glossário Acadêmico

Deve utilizar:

<h2>

<dl>

<dt>

<dd>

Apresentar no mínimo 3 termos relacionados à área de Computação, acompanhados de suas respectivas definições.

Exemplos:

Algoritmo

Framework

API

5. Histórico de Notas
Criar uma tabela denominada:

Histórico de Notas

A tabela deverá conter:

<table>

<caption>Histórico de Notas</caption>

cabeçalhos das colunas utilizando <th>

scope="col" nos cabeçalhos

colunas:

Disciplina

Carga Horária

Nota Final

no mínimo 4 disciplinas

utilização de <tfoot> para apresentar a Média Geral

6. Grade Semanal
Criar uma segunda tabela denominada:

Grade Semanal

A tabela deverá conter as colunas:

Dia da Semana

19h–20h

20h–21h

Deve conter:

no mínimo 3 dias da semana

disciplinas diferentes

utilização de rowspan ou colspan para representar uma disciplina ocupando mais de um horário

7. Rodapé da Página
Criar o rodapé utilizando:

<footer>

<address>

O rodapé deverá apresentar:

nome completo do aluno

e-mail utilizando link com mailto:

LinkedIn utilizando a tag <a>

Desafio Extra
Para complementar a atividade, implementar também:

atributo lang="pt-br" na tag <html>

pelo menos uma tag semântica adicional, como <main> ou <section>

<meta name="description"> no <head> para contribuir com a otimização para mecanismos de busca

Entrega
A entrega deverá conter obrigatoriamente:

curriculo.html

imagens ou demais arquivos utilizados, caso existam

Organizar todos os arquivos utilizados em uma única pasta e realizar a entrega conforme orientação do professor.

Identificação
Informar:

Nome completo do aluno

RA

Importante
Antes da entrega:

testar a página no navegador

verificar se todas as listas foram estruturadas corretamente

conferir a utilização de <ul>, <ol>, <dl>, <dt> e <dd>

verificar a estrutura das tabelas

conferir a utilização de <caption>

verificar o uso correto de <th>, <td> e scope

conferir o funcionamento de rowspan ou colspan

verificar o <tfoot> com a Média Geral

conferir os links de e-mail e LinkedIn

verificar a organização e indentação do código HTML

O resultado esperado é uma página curriculo.html clara, organizada, semântica e acessível, demonstrando domínio dos conteúdos de listas e tabelas em HTML.