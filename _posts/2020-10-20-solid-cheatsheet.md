---
layout :  post
title :  "SOLID - cheatsheet"
tags: analisis diseño solid principios
comments: true
---

### SRP - Single responsability principle

Responsable de cambiar un solo cosa.

***Mal***.

``` java
class NOSRP{
    Sring readFile();
    void saveUserData();
}
```

***Bueno.***

``` java
class File{
    String read();
}
class Users{
    void save(UserData user);
}
```

### OCP - Open closed principle

Extensible pero no para modificaciones.

***Mal***.

```c#
double areaTotal(Shape[] shapes){
    double total = 0;
    foreach(Shape item in shapes){
        if(item is Rectangle){
            total +=  ...;
        } else if (item is Circle) {
            total +=  ...;
        } else {
            total += ...;
        }
    }
    return total;
}
```

***Bueno.***

```c#
interface Shape{
    double getArea();
}

double areaTotal(Shape[] shapes){
    double total = 0;
    foreach(Shape item in shapes){
        total += item.getArea();
    }
    return total;
}
```

### LSP - Liskov substitucion principle

***Bueno.***

```C#
interface Vehicule{
    double getSpeed();
    double getCubicCapacity();
}

void main(){
    Vehicule car = new Car();
    Vehicule bus = new Car();
}
```

### ISP - Interface segregation principle
Dependecia entre clases debe ser la mas pequeña posible

***Mal***.

```c#
interface Animal{
    feed();
    groom(); //limpiar
} 

class Dog : Animal{
    feed();
    groom();
}
class Tiger: Animal{
    feed();
    groom(); // mala implementación
}
```

***Bueno.***

```c#
interface Animal{
    feed();
}
class Pet : Animal {
    groom();
}
class Dog : Pet{}
class Tiles: Animal{}

```
### DIP - Dependency inversion principle

***Mal.***

```c#
void test(){
    var book = new PdfBook();
    var reader = new PdfReader(PdfBook);
}

class PdfBook{}
class PdfReader{
    PdfReader(PdfBook book);
}
```

***Bueno.***

```c#
void test(){
    var book = new pdfBook();
    var reader = new EBookReaer(book);
}

interface EBook{
    String read();
}

class EBookReader{
    EBookReader(EBook book);
}

class PdfBook : EBook{}
class MobiBook : EBook{}
```


#### Resources

* https://dotnetfreakblog.wordpress.com/2013/10/07/single-responsibility-principle/
* https://www.youtube.com/watch?v=yxf2spbpTSw
* https://www.javabrahman.com/programming-principles/liskov-substitution-principal-java-example/
* https://code.tutsplus.com/tutorials/solid-part-4-the-dependency-inversion-principle--net-36872
