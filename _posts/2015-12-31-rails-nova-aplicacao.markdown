---
layout: post
title:  "Criando uma nova aplicação em Rails"
date: 2015-12-31 09:00:00 -0200
categories: Rails
---
**Para criar uma nova aplicação**
{% highlight bash %}
  $ rails new app_nome
{% endhighlight %}

**Para criar o esqueleto de um objeto** 

Este esqueleto criará o model, controllers e views para incluir, editar e listar todos os objetos. Neste caso, criaremos o objeto Tabela

O nome do objeto criado é dado no singular e o Rails se encarrega de criar uma tabela do banco de dados com o nome  no plurar (tabela objetos).
{% highlight bash %}
  $ rails generate scaffold Tarefa nome:string descricao:text data:datetime

{% endhighlight %}

Tipos de dados disponíveis:

- :primary_key
- :string
- :text
- :integer
- :float
- :decimal
- :datetime
- :time
- :date
- :binary
- :boolean

{% highlight ruby %}
  t.decimal :preco, precision: 8, scale: 2
{% endhighlight %}

Após gerar o "scaffold", é preciso aplicar as migrações para o banco de dados de desenvolvimento:
{% highlight bash %}
  $ rake db:migrate
{% endhighlight %}

Aumentando o campo descricao na view.
{% highlight erb %}
  <div>
    <%= f.label :descricao %><br>
    <%= f.text_area :descricao, rows: 8 %>
  </div>
{% endhighlight %}

Para rodar os testes de models e controllers
{% highlight bash %}
  $ rake test
{% endhighlight %}

**Criando um conjunto consistente de dados para teste**

Os dados de teste estão localizados no arquivo *seeds.rb.*
As imagens devem ser copiadas no diretório *app/assets/images*

{% highlight ruby %}
  Tarefa.delete_all
  #...
  Tarefa.create!(nome: 'fazer compras',
    descricao:
      %{<p>
        Precisamos comprar pão, leite e frutas e não podemos nos esquecer
        de comprar muito macarrão para a festa de Domingo.
      </p>},
    data: 2015-12-12)
#...
{% endhighlight %} 

Este código utiliza %{..}, que é uma sintaxe alternativa para string literals de aspas duplas.

Para popular a tabela de tarefas com dados, rode o seguinte comando:

{% highlight bash %}
  $ rake db:seed 
{% endhighlight %}

Se quisermos colocar um pouco de estilo na lista de tarefas que criamos, é preciso incluir dados na folha de estilos que o Rails criou quando rodamos o comando *generate scaffold*. A folha de estilos *tabelas.css.scss* pode ser encontrada no diretório *app/assets/stylesheets.* Esta folha de estilos é pre-processada como CSS Sassy (http://sass-lang.com/). Para saber mais: Pragmatic Guide do Sass.

Como o Rails carrega todas as folhas de estilo ao mesmo tempo, uma boa maneira de controlar as regras para páginas específicas é incluir o nome do controller como o nome da classe do corpo (body) da página.

{% highlight erb %}
  <body class='<%= controller.controller_name %>'>
{% endhighlight %}

**Algumas dicas**

- O método (helper method) **cycle()** inclui as classes *list_line_even* ou *list_line_odd* para cadas uma linhas de uma tabela.
- O método **truncate()** é utilizado para truncar um conjuto de dados.
- O método **strip_tags() é utilizado para remover as tags de HTML de um conjunto de dados
{% highlight erb %}
  <dd><%= truncate (strip_tags(tarefas.descricao), length: 80) %></dd>
{% endhighlight %}

- O parâmetro *data: {confirm:'Are you sure?'} gera uma janela de confirmação quando um conjunto de dados é deletado.
- Para reverter uma migração utilizamos:

{% highlight bash %}
  $ rake db:rollback 
{% endhighlight %}


[comment]: pagina 