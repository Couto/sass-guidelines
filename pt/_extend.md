
# Extend

A directiva `@extend` tem de ser uma das características que fez o Sass tão popular há uns anos atrás. Como lembrete, ela permite dizer ao Sass para estilizar um elemento A, tal como se ele fosse abrangido pelo selector B. Escusado será dizer que isto pode ser um valioso aliados quando se escreve CSS modular.

No entanto sinto-me na necessidade de vos avisar que esta característica, por muito inteligente que seja, é um conceito traiçoeiro, especialmente quando usado indevidamente. O problema é que quando se extende um selector, voçês pouco ou nenhuma forma de responder as seguintes perguntas sem terem um conhecimento profundo de toda a base de código.

* onde é que o selector vai ser colocado?
* é provavel que eu cause efeitos secundários?
* quando grande é o CSS gerado por simples extend?

Por tudo o que sei, o resultado pode variar entre fazer nada e causar efeitos secundários desastrosos. Por causa disso, o meu primeiro conselho é de evitar a directiva `@extend` por completo. Pode soar bruto, mas no fim do dia pode salvar-vos algums problemas e dores de cabeça.

Posto desta forma, voçês conheçem o ditado:

> Nunca digas nunca.<br>
> &mdash; Aparentemente, [não foi a Beyonce](https://github.com/HugoGiraudel/sass-guidelines/issues/31#issuecomment-69112419).

Há cenários onde extender selectores pode valer a pena e ajudar. No entanto, no entanto estejam sempre conscientes destas regras para não ficarem

There are scenarios where extending selectors might be helpful and worthwhile. Yet, always keep in mind those rules so you don't get yourself into trouble:

* Use extend from within a module, not across different modules.
* Use extend on placeholders exclusively, not on actual selectors.
* Make sure the placeholder you extend is present as little as possible in the stylesheet.

If you are going to use extend, let me also remind you that it does not play well with `@media` blocks. As you may know, Sass is unable to extend an outer selector from within a media query. When doing so, the compiler simply crashes, telling you that you cannot do such a thing. Not great. Especially since media queries are almost all we do know.

<div class="code-block">
  <div class="code-block__wrapper" data-syntax="scss">
{% highlight scss %}
.foo {
  content: 'foo';
}

@media print {
  .bar {
    // This doesn't work. Worse: it crashes.
    @extend .foo;
  }
}
{% endhighlight %}
  </div>
  <div class="code-block__wrapper" data-syntax="sass">
{% highlight sass %}
.foo
  content: 'foo'

@media print
  .bar
    // This doesn't work. Worse: it crashes.
    @extend .foo
{% endhighlight %}
  </div>
</div>

> You may not @extend an outer selector from within @media.<br>
> You may only @extend selectors within the same directive.

<div class="note">
  <p>It is often said that <code>@extend</code> helps with the file size since it combines selectors rather than duplicated properties. That is true, however the difference is negligible once <a href="http://en.wikipedia.org/wiki/Gzip">Gzip</a> has done its compression.</p>
  <p>That being said, if you cannot use Gzip (or any equivalent) then switching to a <code>@extend</code> approach might not be that bad as long as you know what you are doing.</p>
</div>

To sum up, I would **advise against using the `@extend` directive**, unless under some specific circumstances, but I would not go as far as to forbid it.



### Leitura Adicional

* [What Nobody Told you About Sass Extend](http://www.sitepoint.com/sass-extend-nobody-told-you/)
* [Why You Should Avoid Extend](http://www.sitepoint.com/avoid-sass-extend/)
* [Don't Over Extend Yourself](http://pressupinc.com/blog/2014/11/dont-overextend-yourself-in-sass/)
* [When to Use Extend; When to Use a Mixin](http://csswizardry.com/2014/11/when-to-use-extend-when-to-use-a-mixin/)
