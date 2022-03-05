# Javascripte Veri Tipi Kontrolü Ve Veri Tipi Değişimi

Gün içerisinde projelerimizde kullandığımız veriler ve veri tipleri değişmekte. Bu verileri sağlıklık bir şekilde kullanabilmek için veri dönüşümlerine ihtiyaç duymaktayız. 
İlk ele almamız gereken konu elimizdeki verinin veri tipini öğrenmek olacak:
Javascripte bu konuyu iki şekilde ele almaktayız;

- Veri tipini öğrenirken en sık kullanılan operatör **typeof()** nasıl kullanıldığını kısaca bakalım.

```jsx
//ilk olarak değişkenizimizi tanımlıyoruz. 
let degisken="Bu bir metinsel ifadedir."
//console.log()u ekrana basmak için kullanıyoruz. Veri tipini öğrenmek için ise typeof() fonksiyonunu kullanıyoruz.typeof() parantezleri arasına ise
console.log(typeof(degisken));
// kodumuzu çalıştırdığımıda ise bize string olarak bir çıktı vermektedir.
```

Şimdide diğer veri tiplerine bakalım 

```jsx
let hasPass=true;

console.log(typeof(hasPass));

//çalıştırdığımızda hasPass adlı değişkinin türü boolean olduğunu  rahatlıkla görebilriiz

let not=23;

console.log(typeof(not))

//buradaki not değişkenimizin veri tipi number olduğunu typeof() ile rahatlıkla görmekteyiz

```

typeof() ile öğrenebildiğimiz gibi `isInteger( )`, `isFinite( )` veya `isNaN( )` kullanarak da kontrol sağlayabiliriz.

isInteger () ile değişkenimizin tam sayı olup olmadığını öğrenebiliriz:

```jsx
Number.isInterger(25) //true
Number.isInterger(-125) //true
Number.isInterger(1.23) //false
```

isFinite() ile bir değerin sonlu sayı olup olamadığını rahatlıkla görebiliriz:

```jsx
Number.isFinite(0)//true
Number.isFinite("143")//false
Number.isFinite("Merhaba")//false
Number.isFinite(-Infinity) //false
Number.isFinite(0 / 0) //false sonuçlarını rahatlıkla görebiliriz.
```

 Diğer bir yöntem olan isNan ile bir değerin NaN (Not-A-Number) olup olamadığını belirlemektedir.

```jsx
Number.isNaN(123) //false
Number.isNaN(0) //false
Number.isNaN('123') //false
Number.isNaN('Hello') //false
Number.isNaN('') //false
Number.isNaN(true) //false
Number.isNaN(undefined) //false
Number.isNaN('NaN') //false
Number.isNaN(NaN) //true
```

`isInteger( )`, `isFinite( )` veya `isNaN( )` kullanılarak kontrolü sağlanan değerler true veya false olarak dönereler

## Değişken Türünü Değiştirmek (Type Coercion)

Nedir bu Type Coercion? Sorusunun cevabı olarak şunu diyebiliri:

Type Coercion: Bir değişken türünü, başka bir değişkene döğüştürmemize imkan sağlayan yöntemdir.

Type Coercion iki türde karşımıza çıkmatadır

Explicit : Metotlarla yapılan dönüşümlerdir.

Implicit:  Operatörlerle veya JavaScriptin kendi yaptığı dönüşümledir.

Explicit’e örnek verecek olursak :

```jsx
String(1212) //"1212"  string fonksiyonu ile number ifadeyi stringe çevirevibiliriz

ParseInt("123") //123 parseint ile stringi numbere çevirebiliriz
```

Implicit’den bahsedip örneksiz bırakmak olmaz buyrun impcilit örneklerimiz;

```jsx
If(3<5) // karşılaştırmalarda karşımıza çıkar ve bu karşılaştırmamızı doğru veya yanlış olarak dönecektir.
console.log(‘ ’+123) // “123” ile string ile numberın toplamını javascript artık bir string olarak dönüşüm sağlamış oldu.
12/”6” // 2  sonucu otamatik olarak bize number tipte vermektedir.
```

Peki bu dönüşümler nasıl yapılıyor? 

### String Dönüşümü

Eğer bir değeri açık bir şekilde String’e dönüştürmek istiyorsak String(), fonksiyonunu kullanırız.

Binary (ikili) + operatörü bir string ifadeye uygulandığında implicit coercion tetiklenir. Örneklerle bunu daha iyi anlayalım:

```jsx
String(123) // “123” explicit
123 + '' // “123”    implicit
```

İlkel veri tipleri (primative varibles) stringe dönüşebilmektedir.

**Primitive type nedir?**

Değerleri stack (yığıt) üzerinde tutulan ilkel tiplerdir. Örneğin; long, int ve double gibi.

 İşte örneğimiz;

```jsx
String(123) // “123”
String(-12.3) // “-12.3”
String(null) // “null”
String(undefined) // “undefined”
String(true) // “true”
String(false) // “false”
```

Sembollerde işler biraz değişiyor. Çünkü dönüşümleri sadece explicit bir şekilde yapılabiliyor. Maalesef implicit bir şekilde yapılamaz.

```jsx
String(Symbol('my symbol')) // 'Symbol(my symbol)'
'' + Symbol('my symbol') // TypeError error dönmekte
```

### **Boolean Dönüşümü**

Bir değişkenin değerini booleanı explicit(fonksiyon kullanarak değiştirme) şekilde dönüştürmek için Boolean() fonksiyonunu kullanabiliriz.

Implicit coercion ise mantıksal operatörlerinin kullanıldığı, mantıksal işlemlerin yapıldığı alanlarda tetiklenir. (|| && !)

```jsx
Boolean(2) // explicit
var a=!!2 //explicit
if (2) { ... } // mantıksal işlem yapıldığı için implicit 
'ahmet' && 3 //mantıksal işlem yapıldığı için implicit 
```

Boolean tiplerle uğraşırken truthy, falsy değerler işin içine girerler. Kısaca açıklayacak olursak javascriptin kendi doğası gereği true veya false dönen değerler mevcuttur. Bunlar;

```jsx
Boolean('') // false
Boolean(0) // false 
Boolean(-0) // false
Boolean(NaN) // false
Boolean(null) // false
Boolean(undefined) // false
Boolean(false) // false
```

Yukarıdaki listede olmayan herhangi bir değer, true'ya dönüştürülür. Fonksiyon, Dizi (Array),Tarih (Date), kullanıcı tanımlı tip (user-defined-type) vb Symboller gerçek değerlidir (truthy value). Hatta boş nesneler (objectler) ve diziler (arrayler) gerçek değerlidir (truthy value).

```jsx
Boolean({}) // true
Boolean([]) // true
Boolean(Symbol()) // true
!!Symbol() // true
Boolean(function() {}) // true
```

> Önemli bir nokta ise : Mantıksal operatörlerden `||` ve `&&`, dönüşüm işlemini internally (dahili olarak) yapar. Ama gerçekte ifadenin operand değerini döndürür, değer boolean tipinde olmasa bile.
> 

Örneklendirecek olursak;

```jsx
// veya “||” operatörü ilk bulduğu true değeri döner
var a= 2 || s || 4 || 5; // 2
// eğer true dönecek değer bulamazsa en son buluğu false değeri döndürür
var b=0 || ”” || false || -0 || 0 // 0
var c= 0 ||  “”  ||  “ 123 ” || 4 ; // ”123” dolu string true dönecektir
// ve ”&&” operatörü ilk bulduğu false değeri döner.
var d=2 && 3 && 0 && 5 && 7; // 0
// eğer false dönecek değer bulamazsa en son buluğu true değeri döndürür
var e= 2 && 3 && 5 && 7 // 7
```

## Nesneler (Objects) için Type Coercion

Şimdiye kadar primitif değerler için type coercion hakkında bilgi sahibi olduk. Nesneler için bu durum biraz daha farklı. JavaScript'te nesneler referans tipler olduğundan üzerinde işlem yapabilmek zordur. İşlem yapabilmek için elimizde primitif değerler olması gerekir. Bu durumda referans tipler primitif tiplere zorlanır. Nesneler için en kolay tip dönüşümü boolean'dır. Primitif olmayan herhangi bir değer örneğin içi dolu veya boş bir nesne (object), dizi (array) fark etmez her zaman true olarak zorlanır. (coerced)

```jsx
console.log(Boolean({})) // true
console.log(Boolean([])) // true
console.log(Boolean([1,2,3])) // true
console.log(Boolean({13:234})) //true
```

Nesnelerde de matematiksel veya mantıksal işlemler yapmak mümkündür. İlk paragrafta belirttiğim gibi bu işlemi ancak primitif bir değere dönüştürerek yapabiliriz. Bu dönüşüm için, giriş nesnesinin (input object) valueOf ve toString metotlarından faydalanılır. Bu iki metot Object.prototype da tanımlanmıştır. Bu sayede türetilmiş tüm tiplerde kullanılır. Örneğin Tarih (Date), Dizi (Array) gibi. İlk olarak nesneler toString() e girer ve çıkan değer primitifse o değeri döner. Primitif değilse valueOf() içine girer. valueOf()'tan çıkan sonuç primitifse o değeri döner değilse error fırlatır.

```jsx
console.log([1]+[1,2,3])
```

İşlem yapabilmek için [ 1 ] ve [ 1,2,3 ] öncelikli olarak primitif türe zorlanır

```jsx
[ 1 ].toString(); // sonuç "1" verir
[ 1,2,3 ].toString() // sonuç "1,2,3" verir. Bu durumda iki string ifadenin toplanmasından çıkan sonuç "1" + "1,2,3" --> "11,2,3" olacaktır.
```

Algoritması genellikle aşağıdaki gibidir:

**Primitif tipler için:**

1. Eğer değer(input) primitif ise herhangi bir işlem yapma, dön.
2. input.toString() metodunu çağır(Call). Eğer sonuç primitif ise dön.
3. input.valueOf() metodunu çağır(Call). Eğer sonuç primitif ise dön.
4. Ne input.toString() ne de input.valueOf() primitif sonuç vermiyorsa; TypeError fırlat.

**Referans tipler için:**

1. input.toString() metodunu çağır(Call). Eğer sonuç primitif ise dön.
2. input.valueOf()metodunu çağır(Call). Eğer sonuç primitif ise dön.
3. Ne input.toString() ne deinput.valueOf() primitif sonuç vermiyorsa; TypeError fırlat.

> `==` operatörünün (lose equality- zayıf eşitlik) farklı iki tipteki a ve b değişkenleri için pratikte nasıl farklı davrandığını, **[JavaScript Comparison Table](https://dorey.github.io/JavaScript-Equality-Table/)** ’de gösteren matristen görebilirsiniz.
>