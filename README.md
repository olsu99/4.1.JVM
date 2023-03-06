# 4.1.JVM
``` java
public class JvmComprehension { /класс JvmComprehension загружается ClassLoader'ом в специальную область metaspace

    public static void main(String[] args) { / в стеке создаётся фрейм main
        int i = 1;                      // 1 : во фрейм main записывается переменная i со значением 1
        Object o = new Object();        // 2 : в heap выделяется память для объекта Object, во фрейм main записывается переменная о, которой присваивается ссылка на 
        // Object в heap
        Integer ii = 2;                 // 3 : в heap выделяется память для объекта Integer, во фрейм main записывается переменная ii, которой присваивается ссылка на 
        // Integer в heap
        printAll(o, i, ii);             // 4 : в стеке создаётся фрейм printAll
        System.out.println("finished"); // 7 : фреймы printAll, System.out, println, toString удаляются сборщиком мусора. В стеке создаются фреймы System.out, println
        // в пуле строк создаётся строка "finished" и выводится в консоль
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5 : во фрейм printAll помещается переменная uselessVar содержащая ссылку на объект Integer в heap
        System.out.println(o.toString() + i + ii);  // 6 : в стеке создаются фреймы System.out, println, toString.
        // toString создает в heap объект типа String, потом в heap создается результирующая строка (o.toString() + i + ii),
        // ссылка на эту строку в heap передается println, System.out выводит значение строки в консоль.
    }
}
```
