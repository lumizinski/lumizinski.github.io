---
layout: post
title:  "Rails - ifs, elses e whiles"
date: 2015-01-02 08:30:00 -0200
categories: Ruby
---

Se quiser adicionar a ideia de documentos *read-only* não modificáveis, pode-se escrever algo como:

{% highlight ruby %}
  class Document
    attr_accessor :writable
    attr_reader :title, :author, :content
  
    # Much of the class omitted...
  
    def title=( new_title )
      **if @writable**
        @title = new_title
      end
    end
  
    # Similar author= and content= methods omitted...

  end
{% endhighlight %}

Utilizando **unless** o código somente é executado se a condição for falsa:
{% highlight ruby %}
  def title=( new_title )
    unless @read_only
      @title = new_title
    end
  end
{% endhighlight %} 

O que pode ser escrito da seguinte maneira:
{% highlight ruby %}
  @title = new_title unless @read_only
{% endhighlight %} 

**Until** é o negativo de while:
{% highlight ruby %}
  until document.printed?
    document.print_next_page
  end
{% endhighlight %}

O que também pode ser escrito como:
{% highlight ruby %}
  document.print_next_page while document.pages_available?
{% endhighlight %}

Ou pode ser escrito como:
{% highlight ruby %}
  document.print_next_page until document.printed?
{% endhighlight %}

É possível escrever um laço em Ruby utilizando o comando **for**, porém normalmente utiliza-se o comando **each** nestes casos, já que o comando for é na verdade uma chamada ao comando each em Ruby. Exemplo:
{% highlight ruby %}
  fonts = [ 'courier', 'times roman', 'helvetica' ]

  fonts.each do |font|
    puts font
  end
{% endhighlight %}

[comment]: The code block in the each version actually introduces a new scope. Any variables introduced into a code block are local to that block and go away at the end of the block. The more traditional for version of the loop does not introduce a new scope, so that variables introduced inside a for are also visible outside the loop. 

O comando **case** tem um grande número de variações, mas é mais comumente utilizado para selecionar um determinado pedaço de código a ser executado:
{% highlight ruby %}
  case title
    when 'War And Peace'
      puts 'Tolstoy'
    when 'Romeo And Juliet'
      puts 'Shakespeare'
    else
      puts "Don't know"
    end
{% endhighlight %}

Ou pode-se utilizar o comando case para um valor computado:
{% highlight ruby %}
  author = case title
    when 'War And Peace'
      'Tolstoy'
    when 'Romeo And Juliet'
      'Shakespeare'
    else
      "Don't know"
    end
{% endhighlight %}

Ou, o equivalente:
{% highlight ruby %}
  author = case title
    when 'War And Peace' then 'Tolstoy'
    when 'Romeo And Juliet' then 'Shakespeare'
    else "Don't know"
  end
{% endhighlight %}

[comment]: These last two examples rely on the fact that virtually everything in Ruby returns a value. Logically enough, a case statement returns the values of the selected when or else clause—or nil if no when clause matches and there is no else . Thus the following just might evaluate to nil :
{% highlight ruby %}
  author = case title
    when 'War And Peace' then 'Tolstoy'
    when 'Romeo And Juliet' then 'Shakespeare'
  end
{% endhighlight %}

[comment]: A key thing to keep in mind about all of these case statements is that they use the === 2 operator to do the comparisons. We will leave the details of === to Chapter 12, but the practical effect of the case statement’s use of === is that it can make your life easier. For example, since classes use === to identify instances of themselves, you can use a case statement to switch on the class of an object:
{% highlight ruby %}
  case doc
  when Document
    puts "It's a document!"
  when String
    puts "It's a string!"
  else
    puts "Don't know what it is!"
  end
{% endhighlight %}

[comment]: In the same spirit, you can use a case statement to detect a regular expression match:
{% highlight ruby %}
  case title
  when /War And .*/
    puts 'Maybe Tolstoy?'
  when /Romeo And .*/
    puts 'Maybe Shakespeare?'
  else
    puts 'Absolutely no idea...'
  end
{% endhighlight %}

[comment]: when you are making decisions in Ruby, only false and nil are treated as false. Ruby treats everything else—and I do mean everything—as true.

[comment]: Ruby’s treatment of booleans means that there are two things that are false and an infinite number of things that are true. Thus you should avoid testing for truth by testing for specific values.

{% highlight ruby %}
  doc = Document.new( 'A Question', 'Shakespeare', 'To be...' )
  flag = defined?( doc )
{% endhighlight %}

[comment]: The rub is that although defined? does indeed return a boolean, it never, ever returns true or false . Instead, defined? returns either a string that describes the thing passed in—in the example above, defined?( doc ) will return *local-variable* . On the other hand, if the thing passed to defined? is not defined, then defined? will return nil . So defined? —like many Ruby methods—works in a boolean context, as long as you don’t explicitly ask if it returns true or false .

{% highlight ruby %}
  file = all ? 'specs' : 'latest_specs'
{% endhighlight %}

[comment]: The ?: operator acts like a very compact if statement with the condition part coming right before the question mark. If the condition (in the example, the value of all ) is true, then the value of the whole expression is the thing between the question mark and the colon— *specs* in the example. If the condition is false, then the expression evaluates to the last part, the bit after the colon, *latest_specs* in the example. The ?: operator has been around since at least the C programming language, but many programming communities tend to ignore it. Ruby coders, always looking for a succinct way getting the point across, do use ?: quite a bit.

[comment]: Another common expression-based idiom helps with a familiar initialization problem: Sometimes you are just not sure if you need to initialize a variable. For example, you might want to ensure that an instance variable is not nil . If the variable has a value you want to leave it alone, but if it is nil you want to set it to some default:
{% highlight ruby %}
  @first_name = '' unless @first_name
  @first_name ||= ''
{% endhighlight %}

[comment]: Although this code does work, an experienced Ruby programmer is much more likely to write it this way:

