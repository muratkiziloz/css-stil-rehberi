# Airbnb CSS/Sass Rehberi

*CSS ve Sass için makul bi yaklaşım*

## İçindekiler

1. [Terminoloji](#terminoloji)
    - [Kural Bildirimi](#kural-bildirimi)
    - [Seçiciler](#seçiciler)
    - [Propertyler](#propertyler)
2. [CSS](#css)
    - [Biçimlendirme](#biçimlendirme)
    - [Yorum Satırları](#yorum-satırları)
    - [OOCSS ve BEM](#oocss-ve-bem)
    - [ID Seçiciler](#id-seçiciler)
    - [JavaScript kancası](#javascript-kancası)
    - [Border](#border)
3. [Sass](#sass)
    - [Syntax](#syntax)
    - [Düzen](#duzen)
    - [Değişkenler](#değişkenler)
    - [Mixin](#mixin)
    - [Extend](#extend)
    - [İç içe geçmiş seçiciler](#İç-içe-geçmiş-seçiciler)
4. [Çeviri](#Çeviri)
5. [Lisans](#lisans)

## Terminoloji

### Kural Bildirimi

Bir kural bildirimi, bir grup seçiciye verilen addır. Örneğin:

```css
.listing {
  font-size: 18px;
  line-height: 1.2;
}
```

### Seçiciler

Bir seçici, DOM ağacındaki elementlerin tanımlı özellikler tarafından biçimlendirilmesini sağlar. Seçiciler, HTML elementlerinin yanı sıra sınıfı, id'yi yada property ile eşleşebilir. İşte bazı örnekler:

```css
.my-element-class {
  /* ... */
}

[aria-hidden] {
  /* ... */
}
```

### Propertyler

Bir seçicinin stillerini içerir. Propertyler, key-value çiftleridir (*Örneğin color: turquoise;*). Propertyler şu şekilde görünür:

```css
/* herhangi bir seçici */ {
  background: #f1f1f1;
  color: #333;
}
```

**[⬆ yukarı çık](#%C4%B0%C3%A7indekiler)**

## CSS

### Biçimlendirme

* Girintiler için 2 boşluk kullanın
* Class adlarında `camelCasing` yerine tire (`-`) kullanın.
  - BEM kullanıyorsanız PascalCasing kullanabilirsiniz. ([OOCSS ve BEM](#oocss-ve-bem)).
* ID seçici kullanmayın
* Birden çok seçici kullandığınızda, her seçiciye yeni satır verin
* `{` parantezinden önce bir boşluk bırakın
* `:`dan önce boşluk kullanmayın fakat sonrasında bir boşluk kullanın
* `}` parantezinden sonra yeni bir satıra geçin
* Kural bildirimleri arasına bir boş satır kullanın

**Kötü Kod**

```css
.avatar{
  border-radius:50%;
  border:2px solid white; }
.no, .nope, .not_good {
  // ...
}
#lol-no {
  // ...
}
```

**İyi Kod**

```css
.avatar {
  border-radius: 50%;
  border: 2px solid white;
}

.one,
.selector,
.per-line {
  // ...
}
```

### Yorum Satırları

* Tek satır yorumlar için `//` tercih edin.
* Yorum satırlarını yeni satırda yazın. Satır sonuna yazmaktan kaçının.
* Kendi kendini belgeleyen kodlar için ayrıntılı yorumlar yazın:
   - z-index kullanımı
   - Tarayıcı uyumluluğu veya tarayıcıya özgü hackler

### OOCSS ve BEM

OOCSS ve BEM kombinasyonlarını teşvik etme nedenlerimiz şunlar:

  * CSS ve HTML arasında net, sıkı ilişkiler oluşturulmasına yardımcı olur
  * Yeniden kullanılabilir, bileşilebilir componentler oluşturmamıza yardımcı olur
  * Daha az yuvalanma (nesting) ve daha düşük özgüllük sağlar
  * Ölçeklenebilir stil sayfalarının oluşturulmasına yardımcı olur

**OOCSS** veya `Obje Yönelimli CSS`, stil sayfalarınızı `objeler` topluluğu olarak düşünmenizi teşvik eden CSS yazmak için bir yaklaşımdır; bir web sitesinde bağımsız olarak kullanılabilen yeniden kullanılabilir, tekrarlanabilir snippetlerdir.

  * Nicole Sullivan'ın [OOCSS wiki](https://github.com/stubbornella/oocss/wiki) hakkında makalesi
  * Smashing Magazine'ın [OOCSS](http://www.smashingmagazine.com/2011/12/12/an-introduction-to-object-oriented-css-oocss/) hakkında makalesi

**BEM** veya `Block-Element-Modifier`, HTML ve CSS classları için bir `_naming` kuralıdır. Orijinal olarak Yandex tarafından büyük kod esasları ve ölçeklenebilirlik göz önünde bulundurularak geliştirildi ve OOCSS'yi uygulamak için sağlam bir dizi kural olarak kullanılabilir.

  * CSS Trick'in [BEM 101](https://css-tricks.com/bem-101/) hakkında makalesi
  * Harry Roberts'in [BEM](http://csswizardry.com/2013/01/mindbemding-getting-your-head-round-bem-syntax/) hakkında makalesi

Özellikle componentlerle birleştirildiğinde (<i>örneğin React</i>) iyi çalışan PascalCased `blokları` ile BEM'in bir varyantını öneriyoruz. Alt çizgiler ve kısa çizgiler hala değiştiriciler ve childlar için kullanılır.

**Örnek**

```jsx
// ListingCard.jsx
function ListingCard() {
  return (
    <article class="ListingCard ListingCard--featured">

      <h1 class="ListingCard__title">Adorable 2BR in the sunny Mission</h1>

      <div class="ListingCard__content">
        <p>Vestibulum id ligula porta felis euismod semper.</p>
      </div>

    </article>
  );
}
```

```css
/* ListingCard.css */
.ListingCard { }
.ListingCard--featured { }
.ListingCard__title { }
.ListingCard__content { }
```

  * `.ListingCard` `block`tur ve en yüksek seviyeli componenti temsil eder
  * `.ListingCard__title` `element`tir ve bloğu bir bütün olarak oluşturmaya yardımcı olan `.ListingCard`ın bir soyunu temsil eder.
  * `.ListingCard--featured`  `modifier`dır ve `.ListingCard` bloğunda farklı bir durumu veya varyasyonu temsil eder.

### ID Seçiciler

CSS'te id seçiciler kullanılabilsede, kullanmaktan kaçınmalıyız. Id seçiciler kural bildirimine gereksiz derecede yüksek bir [özgüllük](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) seviyesi getirir ve tekrar kullanılamazlar.

Bu konu hakkında daha fazla bilgi için, [CSS Sihirbazının makalesini](http://csswizardry.com/2014/07/hacks-for-dealing-with-specificity/) okuyun.

### JavaScript kancası

CSS ve JavaScriptinizde aynı classa bağlanmaktan kaçının. Başka bir developer class adında değişiklik yaptığında çalışan sistemi bozabilir. (<i>o class javascriptte kullanılıyor olabilir.</i>)

JavaScript ile class'ları seçmek için, js'ye özgü `.js-` ön ekli classlar oluşturmanızı öneririz. Bu refactoring sırasında boşa harcanan süreyi en aza indirecektir.

```html
<button class="btn btn-primary js-kitap-istemek">Kitap İstemek</button>
```

### Border

Border'ın olmadığı durumlarda `none` yerine `0` kullanın.

**Kötü Kod**

```css
.foo {
  border: none;
}
```

**İyi Kod**

```css
.foo {
  border: 0;
}
```
**[⬆ yukarı çık](#%C4%B0%C3%A7indekiler)**

## Sass

### Syntax

* `.scss` syntaxı kullanın, orijinal `.sass` syntaxını kullanmayın.
* CSS ve `@include`ları düzenli kullanın (aşağı bakın).

### Düzen

1. Property bildirimleri

Tüm standart propertyleri, `@include` veya nested bir seçici olmayan herhangi bir şeyi listeleyin.

```scss
.btn-green {
  background: green;
  font-weight: bold;
  // ...
}
```

2. `@include` bildirimleri

`@include`ların propertylerin sonunda olması, tüm seçiciyi okumayı kolaylaştırır.

```scss
.btn-green {
  background: green;
  font-weight: bold;
  @include transition(background 0.5s ease);
  // ...
}
```

3. İç içe seçiciler

Kural bildirimleriniz ve iç içe geçmiş seçiciler ile bitişik iç içe geçmiş seçiciler arasında boşluk ekleyin. İç içe geçmiş seçicilerinize yukarıdaki aynı yönergeleri uygulayın.

```scss
.btn {
  background: green;
  font-weight: bold;
  @include transition(background 0.5s ease);

  .icon {
    margin-right: 10px;
  }
}
```

### Değişkenler

`camelCased` veya `snake_cased` değişken adları yerine `dash-cased` değişken isimlerini tercih edin (örneğin, `$my-variable`). Aynı dosya içinde yalnızca bir alt çizgi (örneğin, `$_my-variable`) ile kullanılması amaçlanan değişken adlarını önek kabul etmek mümkündür.

### Mixin

Temiz ve daha anlaşılır kod yazımı için iyi adlandırılmış mixinler kullanılmalıdır. Ancak css kodlarını gereksiz yere çoğaltmayacağınızdan emin olun.

### Extend

`@extend`ten kaçınılmalıdır, çünkü özellikle iç içe geçmiş seçicilerle kullanıldığında beklenmedik ve potansiyel olarak tehlikeli davranışları vardır. Üst düzey placeholder seçicilerini genişletmek bile, seçici sırasının daha sonra değişmesiyle sorunlara neden olabilir. Gzipping, `@extend` kullanarak elde edeceğiniz tasarrufların çoğunu üstlenmeli ve stil sayfalarınızı mixinlerle güzelce canlandırabilirsiniz.

### İç içe geçmiş seçiciler

**İç içe seçicileri en fazla 3 seviye kullanın!**

```scss
.page-container {
  .content {
    .profile {
      // DUR!
    }
  }
}
```

Seçiciler bu kadar uzun olduğunda, CSS'iniz:

* HTML'e çok sıkı bağlanır
* Aşırı spesifiktir
* Yeniden kullanılamaz, refactoringi zor hale gelir

Tekrar: **Hiçbir zaman ID seçiciyi iç içe seçicilerde kullanmayın!**

Bir ID seçiciyi ilk etapta kullanmanız gerekiyorsa, asla iç içe seçicilerde kullanılmamalıdır. Bunu yaptığınızda, kodunuzu tekrar gözden geçirmeniz veya bu kadar güçlü özgüllüğün neden gerekli olduğunu bulmanız gerekir. İyi oluşturulmuş bir HTML ve CSS yazıyorsanız, bunu **asla** yapmanıza gerek yoktur.

**[⬆ yukarı çık](#%C4%B0%C3%A7indekiler)**

## Çeviri

Bu rehberin diğer dillerde çeviriside mevcuttur:

  - ![en](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/England.png) **English**: [airbnb/css](https://github.com/airbnb/css)
  - ![id](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Indonesia.png) **Bahasa Indonesia**: [mazipan/css-style-guide](https://github.com/mazipan/css-style-guide)
  - ![tw](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Taiwan.png) **Chinese (Traditional)**: [ArvinH/css-style-guide](https://github.com/ArvinH/css-style-guide)
  - ![cn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/China.png) **Chinese (Simplified)**: [Zhangjd/css-style-guide](https://github.com/Zhangjd/css-style-guide)
  - ![fr](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/France.png) **French**: [mat-u/css-style-guide](https://github.com/mat-u/css-style-guide)
  - ![ja](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Japan.png) **Japanese**: [nao215/css-style-guide](https://github.com/nao215/css-style-guide)
  - ![ko](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/South-Korea.png) **Korean**: [CodeMakeBros/css-style-guide](https://github.com/CodeMakeBros/css-style-guide)
  - ![PT-BR](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Brazil.png) **Portuguese (Brazil)**: [felipevolpatto/css-style-guide](https://github.com/felipevolpatto/css-style-guide)
  - ![pt-PT](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Portugal.png) **Portuguese (Portugal)**: [SandroMiguel/airbnb-css-style-guide](https://github.com/SandroMiguel/airbnb-css-style-guide)
  - ![ru](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Russia.png) **Russian**: [Nekorsis/css-style-guide](https://github.com/Nekorsis/css-style-guide)
  - ![es](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Spain.png) **Spanish**: [ismamz/guia-de-estilo-css](https://github.com/ismamz/guia-de-estilo-css)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Vietnam.png) **Vietnamese**: [trungk18/css-style-guide](https://github.com/trungk18/css-style-guide)
  - ![vn](https://raw.githubusercontent.com/gosquared/flags/master/flags/flags/shiny/24/Italy.png) **Italian**: [antoniofull/linee-guida-css](https://github.com/antoniofull/linee-guida-css)

**[⬆ yukarı çık](#%C4%B0%C3%A7indekiler)**

## Lisans

(The MIT License)

Copyright (c) 2015 Airbnb

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and associated documentation files (the 'Software'), to deal in the Software without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

**[⬆ yukarı çık](#%C4%B0%C3%A7indekiler)**
