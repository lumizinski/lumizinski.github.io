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

Este esqueleto criará o model, controllers e views para incluir, editar e listar todos os objetos. 

O nome do objeto criado é dado no singular e o Rails se encarrega de criar uma tabela do banco de dados com o nome  no plurar (tabela objetos).
{% highlight bash %}
  $ rails generate scaffold Objeto nome:string descricao:text preco:decimal

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

[comment]: pagina 68