Код для исследования
public class JvmComprehension {

    public static void main(String[] args) {
        int i = 1;                      // 1
        Object o = new Object();        // 2
        Integer ii = 2;                 // 3
        printAll(o, i, ii);             // 4
        System.out.println("finished"); // 7
    }

    private static void printAll(Object o, int i, Integer ii) {
        Integer uselessVar = 700;                   // 5
        System.out.println(o.toString() + i + ii);  // 6
    }
}

Подробное объяснение по строкам:
Загрузка класса:
    Когда программа запускается, ClassLoader загружает класс JvmComprehension в Метаспейс (Metaspace). Метаспейс является областью памяти, в которой хранятся метаданные классов.
Запуск метода main:
    Метод main помещается в фрейм стека вызовов (Stack Frame) в Стэке (Stack). Стек — это область памяти, где хранятся вызовы функций и локальные переменные.
Строка 1:
   int i = 1;
    Переменная i типа int создается в стеке, и ей присваивается значение 1.
Строка 2:
   Object o = new Object();
    Создается новый объект Object в Хипе (Heap).
    Ссылка на этот объект сохраняется в локальной переменной o в стеке.
Строка 3:
   Integer ii = 2;
    Автоматическая упаковка (autoboxing):
    Число 2 типа int упаковывается в объект класса Integer.
    Новый объект Integer создается в хипе (если не используется кэширование значений от -128 до 127, специфичное для данного типа).
    Ссылка на этот объект сохраняется в локальной переменной ii в стеке.
Строка 4:
   printAll(o, i, ii);
    Вызов метода printAll, для которого создается новый фрейм в стеке.
    В параметрах o, i и ii передаются текущие значения переменных.
Строка 5 (внутри метода printAll):
   Integer uselessVar = 700;
    Автоматическая упаковка (autoboxing):
    Число 700 типа int упаковывается в объект класса Integer.
    Новый объект Integer создается в хипе.
    Ссылка на этот объект сохраняется в локальной переменной uselessVar в стеке.
Строка 6 (внутри метода printAll):
   System.out.println(o.toString() + i + ii);
    Вызов метода toString на объекте o, который находится в хипе.
    Значения i и ii конкатенируются с результирующей строкой.
    Строка передается в метод println, который выводит её на консоль.
    Возвращение из метода printAll:
    Фрейм данного метода удаляется из стека. Объекты, которые больше не используются и ссылки на которые отсутствуют, становятся кандидатами для очистки сборщиком мусора (Garbage Collector).
Строка 7:
    System.out.println("finished");
    Выводится строка `"finished"` на консоль.

Сборщик мусора:
    Сборщик мусора периодически проходит по хипу и удаляет объекты, на которые нет ссылок, тем самым освобождая память. В данном примере после выхода из main, все локальные переменные и их ссылки теряют свою актуальность, что делает связанные объекты кандидатами для удаления.
Области памяти:
    Метаспейс (Metaspace):
        Хранит метаданные классов.
    Heap (Хип):
        Хранит все динамически выделенные объекты.
    Stack (Стек):
        Хранит фреймы вызовов методов и локальные переменные.
