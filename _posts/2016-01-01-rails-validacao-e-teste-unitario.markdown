---
layout: post
title:  "Validação e teste unitário"
date: 2015-01-01 09:00:00 -0200
categories: Rails
---

Para validar um campo para que não seja vazio, checando se os campos existem e não estejam vazios.
{% highlight ruby %}
  validates :nome, :descricao, presence: true
{% endhighlight %}

Para validar valores numericos:
{% highlight ruby %}
  validates :preco, :numericality: {:greater_than_or_equal_to:0.01}
{% endhighlight %}

Para validar unicidade:
{% highlight ruby %}
  validates :nome, :uniqueness:true
{% endhighlight %}

Para validar o formato de uma entrada:
{% highlight ruby %}
  validates :nome_da_imagem, allow_blank: true, format: {
    with:   %r{\.(gif|jpg|png)|Z}i,
    message: 'deve ser uma imagem nos formatos GIF, JPG ou PNG'
  }
{% endhighlight %}

[comment]: ver testes página 81