day 1
//
pr2
123

//code
public class Main {
public static void main(String[] args) {
System.out.println("Група: 34");
System.out.println("Вчитель: Олійник");
System.out.println("Аргументи командного рядка:");
for (String arg : args) {
System.out.println(arg);
}
}
}

day 2
//
pr2
123

import java.io.Serializable;
import java.io.*;

class ДаніОбчислення implements Serializable {
    private final double параметр1;
    private final double параметр2;
    private transient double результат;

    ДаніОбчислення(double парам1, double парам2) {
        this.параметр1 = парам1;
        this.параметр2 = парам2;
        this.результат = 0.0;
    }

    void обчислитиРезультат() {
        this.результат = параметр1 + параметр2;
    }

    double отриматиПараметр1() {
        return параметр1;
    }

    double отриматиПараметр2() {
        return параметр2;
    }

    double отриматиРезультат() {
        return результат;
    }
}

class Калькулятор {
    private final ДаніОбчислення дані;

    Калькулятор(double парам1, double парам2) {
        this.дані = new ДаніОбчислення(парам1, парам2);
        this.дані.обчислитиРезультат();
    }

    double отриматиРезультат() {
        return дані.отриматиРезультат();
    }

    ДаніОбчислення отриматиДані() {
        return дані;
    }
}

class ДемонстраціяСеріалізації {
    static void зберегтиОбєкт(ДаніОбчислення дані, String імʼяФайлу) {
        try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream(імʼяФайлу))) {
            out.writeObject(дані);
            System.out.println("Обʼєкт успішно збережено");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    static ДаніОбчислення завантажитиОбєкт(String імʼяФайлу) {
        try (ObjectInputStream in = new ObjectInputStream(new FileInputStream(імʼяФайлу))) {
            ДаніОбчислення дані = (ДаніОбчислення) in.readObject();
            System.out.println("Обʼєкт успішно завантажено");
            return дані;
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
            return null;
        }
    }
}

class ТестОбчислень {
    static void тестуватиОбчислення() {
        Калькулятор калькулятор = new Калькулятор(5.0, 3.0);
        double очікуваний = 8.0;
        double фактичний = калькулятор.отриматиРезультат();
        
        if (Math.abs(очікуваний - фактичний) < 0.0001) {
            System.out.println("Тест обчислень пройдено");
        } else {
            System.out.println("Тест обчислень не пройдено: очікувалось " + очікуваний + ", отримано " + фактичний);
        }
    }

    static void тестуватиСеріалізацію() {
        Калькулятор калькулятор = new Калькулятор(5.0, 3.0);
        ДемонстраціяСеріалізації.зберегтиОбєкт(калькулятор.отриматиДані(), "тест.ser");
        
        ДаніОбчислення завантажені = ДемонстраціяСеріалізації.завантажитиОбєкт("тест.ser");
        if (завантажені != null && 
            Math.abs(завантажені.отриматиПараметр1() - 5.0) < 0.0001 && 
            Math.abs(завантажені.отриматиПараметр2() - 3.0) < 0.0001) {
            System.out.println("Тест серіалізації пройдено");
        } else {
            System.out.println("Тест серіалізації не пройдено");
        }
        
        if (завантажені != null && завантажені.отриматиРезультат() == 0.0) {
            System.out.println("Тест поля transient пройдено");
        } else {
            System.out.println("Тест поля transient не пройдено");
        }
    }
}

public class Main {
    static int порахуватиЧергування(int число) {
        String двійковеПодання = Integer.toBinaryString(число);
        int кількістьЧергувань = 0;
        
        for (int i = 1; i < двійковеПодання.length(); i++) {
            if (двійковеПодання.charAt(i) != двійковеПодання.charAt(i - 1)) {
                кількістьЧергувань++;
            }
        }
        return кількістьЧергувань;
    }

    public static void main(String[] args) {
        System.out.println("Группа: 34");
        System.out.println("Учитель: Олейник");
        System.out.println("Аргументы командной строки:");
        for (String arg : args) {
            System.out.println(arg);
        }

        Калькулятор калькулятор = new Калькулятор(5.0, 3.0);
        System.out.println("Результат расчета: " + калькулятор.отриматиРезультат());

        ДемонстраціяСеріалізації.зберегтиОбєкт(калькулятор.отриматиДані(), "дані_обчислення.ser");
        
        ДаніОбчислення завантаженіДані = ДемонстраціяСеріалізації.завантажитиОбєкт("дані_обчислення.ser");
        if (завантаженіДані != null) {
            System.out.println("Завантажений параметр1: " + завантаженіДані.отриматиПараметр1());
            System.out.println("Завантажений параметр2: " + завантаженіДані.отриматиПараметр2());
            System.out.println("Завантажений результат (transient): " + завантаженіДані.отриматиРезультат());
        }

        ТестОбчислень.тестуватиОбчислення();
        ТестОбчислень.тестуватиСеріалізацію();

        int число = 10;
        System.out.println("Число: " + число);
        System.out.println("Двійкове подання: " + Integer.toBinaryString(число));
        System.out.println("Кількість чергувань 0 та 1: " + порахуватиЧергування(число));
    }
}


day 3 
//
pr2
123


import java.io.Serializable;
import java.io.*;
import java.util.ArrayList;

class ДаніОбчислення implements Serializable {
    private final double параметр1;
    private final double параметр2;
    private transient double результат;

    ДаніОбчислення(double парам1, double парам2) {
        this.параметр1 = парам1;
        this.параметр2 = парам2;
        this.результат = 0.0;
    }

    void обчислитиРезультат() {
        this.результат = параметр1 + параметр2;
    }

    double отриматиПараметр1() {
        return параметр1;
    }

    double отриматиПараметр2() {
        return параметр2;
    }

    double отриматиРезультат() {
        return результат;
    }
}

class Калькулятор {
    private final ДаніОбчислення дані;

    Калькулятор(double парам1, double парам2) {
        this.дані = new ДаніОбчислення(парам1, парам2);
        this.дані.обчислитиРезультат();
    }

    double отриматиРезультат() {
        return дані.отриматиРезультат();
    }

    ДаніОбчислення отриматиДані() {
        return дані;
    }
}

class ДемонстраціяСеріалізації {
    static void зберегтиОбєкт(ДаніОбчислення дані, String імʼяФайлу) {
        try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream(імʼяФайлу))) {
            out.writeObject(дані);
            System.out.println("Обʼєкт успішно збережено");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    static ДаніОбчислення завантажитиОбєкт(String імʼяФайлу) {
        try (ObjectInputStream in = new ObjectInputStream(new FileInputStream(імʼяФайлу))) {
            ДаніОбчислення дані = (ДаніОбчислення) in.readObject();
            System.out.println("Обʼєкт успішно завантажено");
            return дані;
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
            return null;
        }
    }

    static void зберегтиКолекцію(ArrayList<ДаніОбчислення> колекція, String імʼяФайлу) {
        try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream(імʼяФайлу))) {
            out.writeObject(колекція);
            System.out.println("Колекція успішно збережена");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    @SuppressWarnings("unchecked")
    static ArrayList<ДаніОбчислення> завантажитиКолекцію(String імʼяФайлу) {
        try (ObjectInputStream in = new ObjectInputStream(new FileInputStream(імʼяФайлу))) {
            ArrayList<ДаніОбчислення> колекція = (ArrayList<ДаніОбчислення>) in.readObject();
            System.out.println("Колекція успішно завантажена");
            return колекція;
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
            return null;
        }
    }
}

class ТестОбчислень {
    static void тестуватиОбчислення() {
        Калькулятор калькулятор = new Калькулятор(5.0, 3.0);
        double очікуваний = 8.0;
        double фактичний = калькулятор.отриматиРезультат();
        
        if (Math.abs(очікуваний - фактичний) < 0.0001) {
            System.out.println("Тест обчислень пройдено");
        } else {
            System.out.println("Тест обчислень не пройдено: очікувалось " + очікуваний + ", отримано " + фактичний);
        }
    }

    static void тестуватиСеріалізацію() {
        Калькулятор калькулятор = new Калькулятор(5.0, 3.0);
        ДемонстраціяСеріалізації.зберегтиОбєкт(калькулятор.отриматиДані(), "тест.ser");
        
        ДаніОбчислення завантажені = ДемонстраціяСеріалізації.завантажитиОбєкт("тест.ser");
        if (завантажені != null && 
            Math.abs(завантажені.отриматиПараметр1() - 5.0) < 0.0001 && 
            Math.abs(завантажені.отриматиПараметр2() - 3.0) < 0.0001) {
            System.out.println("Тест серіалізації пройдено");
        } else {
            System.out.println("Тест серіалізації не пройдено");
        }
        
        if (завантажені != null && завантажені.отриматиРезультат() == 0.0) {
            System.out.println("Тест поля transient пройдено");
        } else {
            System.out.println("Тест поля transient не пройдено");
        }
    }
}

interface Відображуваний {
    void відобразитиПараметри();
    void відобразитиРезультат();
}

interface ФабрикаВідображення {
    Відображуваний створитиВідображувач(ДаніОбчислення дані);
}

class ТекстовийВідображувачПараметри implements Відображуваний {
    private final ДаніОбчислення дані;

    ТекстовийВідображувачПараметри(ДаніОбчислення дані) {
        this.дані = дані;
    }

    public void відобразитиПараметри() {
        System.out.println("Параметр 1: " + дані.отриматиПараметр1() + ", Параметр 2: " + дані.отриматиПараметр2());
    }

    public void відобразитиРезультат() {
        System.out.println("Результат (лише параметри): недоступно");
    }
}

class ТекстовийВідображувачРезультат implements Відображуваний {
    private final ДаніОбчислення дані;

    ТекстовийВідображувачРезультат(ДаніОбчислення дані) {
        this.дані = дані;
    }

    public void відобразитиПараметри() {
        System.out.println("Параметри (лише результат): недоступно");
    }

    public void відобразитиРезультат() {
        System.out.println("Результат: " + дані.отриматиРезультат());
    }
}

class ФабрикаПараметри implements ФабрикаВідображення {
    public Відображуваний створитиВідображувач(ДаніОбчислення дані) {
        return new ТекстовийВідображувачПараметри(дані);
    }
}

class ФабрикаРезультат implements ФабрикаВідображення {
    public Відображуваний створитиВідображувач(ДаніОбчислення дані) {
        return new ТекстовийВідображувачРезультат(дані);
    }
}

public class Main {
    static int порахуватиЧергування(int число) {
        String двійковеПодання = Integer.toBinaryString(число);
        int кількістьЧергувань = 0;
        
        for (int i = 1; i < двійковеПодання.length(); i++) {
            if (двійковеПодання.charAt(i) != двійковеПодання.charAt(i - 1)) {
                кількістьЧергувань++;
            }
        }
        return кількістьЧергувань;
    }

    public static void main(String[] args) {
        System.out.println("Группа: 34");
        System.out.println("Учитель: Олейник");
        System.out.println("Аргументы командной строки:");
        for (String arg : args) {
            System.out.println(arg);
        }

        ArrayList<ДаніОбчислення> колекціяОбчислень = new ArrayList<>();
        Калькулятор калькулятор1 = new Калькулятор(5.0, 3.0);
        Калькулятор калькулятор2 = new Калькулятор(10.0, 20.0);
        колекціяОбчислень.add(калькулятор1.отриматиДані());
        колекціяОбчислень.add(калькулятор2.отриматиДані());
        System.out.println("Результат 1: " + калькулятор1.отриматиРезультат());
        System.out.println("Результат 2: " + калькулятор2.отриматиРезультат());

        ДемонстраціяСеріалізації.зберегтиКолекцію(колекціяОбчислень, "колекція_обчислень.ser");
        ArrayList<ДаніОбчислення> завантаженаКолекція = ДемонстраціяСеріалізації.завантажитиКолекцію("колекція_обчислень.ser");

        if (завантаженаКолекція != null) {
            for (ДаніОбчислення дані : завантаженаКолекція) {
                System.out.println("Завантажені параметри: " + дані.отриматиПараметр1() + ", " + дані.отриматиПараметр2());
            }
        }

        ДемонстраціяСеріалізації.зберегтиОбєкт(калькулятор1.отриматиДані(), "дані_обчислення.ser");
        ДаніОбчислення завантаженіДані = ДемонстраціяСеріалізації.завантажитиОбєкт("дані_обчислення.ser");
        if (завантаженіДані != null) {
            System.out.println("Завантажений параметр1: " + завантаженіДані.отриматиПараметр1());
            System.out.println("Завантажений параметр2: " + завантаженіДані.отриматиПараметр2());
            System.out.println("Завантажений результат (transient): " + завантаженіДані.отриматиРезультат());
        }

        ТестОбчислень.тестуватиОбчислення();
        ТестОбчислень.тестуватиСеріалізацію();

        int число = 10;
        System.out.println("Число: " + число);
        System.out.println("Двійкове подання: " + Integer.toBinaryString(число));
        System.out.println("Кількість чергувань 0 та 1: " + порахуватиЧергування(число));

        ФабрикаВідображення фабрикаПараметри = new ФабрикаПараметри();
        ФабрикаВідображення фабрикаРезультат = new ФабрикаРезультат();
        Відображуваний відображувачПараметри = фабрикаПараметри.створитиВідображувач(калькулятор1.отриматиДані());
        Відображуваний відображувачРезультат = фабрикаРезультат.створитиВідображувач(калькулятор1.отриматиДані());
        відображувачПараметри.відобразитиПараметри();
        відображувачПараметри.відобразитиРезультат();
        відображувачРезультат.відобразитиПараметри();
        відображувачРезультат.відобразитиРезультат();
    }
}



day 4
//
pr2
123

import java.io.Serializable;
import java.io.*;
import java.util.ArrayList;
import java.util.Scanner;

/**
 * Клас, що представляє дані для обчислень, які можна серіалізувати.
 */
class ДаніОбчислення implements Serializable {
    private final double параметр1;
    private final double параметр2;
    private transient double результат;

    /**
     * Конструктор для створення об’єкта ДаніОбчислення.
     * @param парам1 Перший параметр для обчислень.
     * @param парам2 Другий параметр для обчислень.
     */
    ДаніОбчислення(double парам1, double парам2) {
        this.параметр1 = парам1;
        this.параметр2 = парам2;
        this.результат = 0.0;
    }

    /**
     * Обчислює результат як суму параметрів.
     */
    void обчислитиРезультат() {
        this.результат = параметр1 + параметр2;
    }

    /**
     * Повертає перший параметр.
     * @return Перший параметр.
     */
    double отриматиПараметр1() {
        return параметр1;
    }

    /**
     * Повертає другий параметр.
     * @return Другий параметр.
     */
    double отриматиПараметр2() {
        return параметр2;
    }

    /**
     * Повертає результат обчислень.
     * @return Результат обчислень.
     */
    double отриматиРезультат() {
        return результат;
    }
}

/**
 * Клас для виконання обчислень на основі даних.
 */
class Калькулятор {
    private final ДаніОбчислення дані;

    /**
     * Конструктор для створення калькулятора.
     * @param парам1 Перший параметр.
     * @param парам2 Другий параметр.
     */
    Калькулятор(double парам1, double парам2) {
        this.дані = new ДаніОбчислення(парам1, парам2);
        this.дані.обчислитиРезультат();
    }

    /**
     * Повертає результат обчислень.
     * @return Результат обчислень.
     */
    double отриматиРезультат() {
        return дані.отриматиРезультат();
    }

    /**
     * Повертає об’єкт даних.
     * @return Об’єкт ДаніОбчислення.
     */
    ДаніОбчислення отриматиДані() {
        return дані;
    }
}

/**
 * Клас для демонстрації серіалізації та десеріалізації колекцій.
 */
class ДемонстраціяСеріалізації {
    /**
     * Зберігає колекцію у файл.
     * @param колекція Колекція для збереження.
     * @param імʼяФайлу Ім’я файлу для збереження.
     */
    static void зберегтиКолекцію(ArrayList<ДаніОбчислення> колекція, String імʼяФайлу) {
        try (ObjectOutputStream out = new ObjectOutputStream(new FileOutputStream(імʼяФайлу))) {
            out.writeObject(колекція);
            System.out.println("Колекція успішно збережена");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    /**
     * Завантажує колекцію з файлу.
     * @param імʼяФайлу Ім’я файлу для завантаження.
     * @return Завантажена колекція.
     */
    @SuppressWarnings("unchecked")
    static ArrayList<ДаніОбчислення> завантажитиКолекцію(String імʼяФайлу) {
        try (ObjectInputStream in = new ObjectInputStream(new FileInputStream(імʼяФайлу))) {
            ArrayList<ДаніОбчислення> колекція = (ArrayList<ДаніОбчислення>) in.readObject();
            System.out.println("Колекція успішно завантажена");
            return колекція;
        } catch (IOException | ClassNotFoundException e) {
            e.printStackTrace();
            return null;
        }
    }
}

/**
 * Інтерфейс для об’єктів, які можуть відображати результати обчислень.
 */
interface Відображуваний {
    /**
     * Відображає параметри обчислень.
     */
    void відобразитиПараметри();

    /**
     * Відображає результат обчислень.
     */
    void відобразитиРезультат();

    /**
     * Відображає дані у вигляді таблиці з заданою шириною стовпців.
     * @param ширинаСтовпця Ширина стовпців таблиці.
     */
    void відобразитиЯкТаблицю(int ширинаСтовпця);
}

/**
 * Інтерфейс для фабрики, яка створює відображувачі.
 */
interface ФабрикаВідображення {
    /**
     * Створює відображувач для даних.
     * @param дані Дані для відображення.
     * @return Об’єкт, що реалізує Відображуваний.
     */
    Відображуваний створитиВідображувач(ДаніОбчислення дані);
}

/**
 * Клас для текстового відображення параметрів.
 */
class ТекстовийВідображувачПараметри implements Відображуваний {
    private final ДаніОбчислення дані;

    /**
     * Конструктор для створення відображувача параметрів.
     * @param дані Дані для відображення.
     */
    ТекстовийВідображувачПараметри(ДаніОбчислення дані) {
        this.дані = дані;
    }

    public void відобразитиПараметри() {
        System.out.println("Параметр 1: " + дані.отриматиПараметр1() + ", Параметр 2: " + дані.отриматиПараметр2());
    }

    public void відобразитиРезультат() {
        System.out.println("Результат (лише параметри): недоступно");
    }

    public void відобразитиЯкТаблицю(int ширинаСтовпця) {
        System.out.println("Відображення параметрів у вигляді таблиці:");
        String заголовок = String.format("|%-" + ширинаСтовпця + "s|%-" + ширинаСтовпця + "s|", "Параметр 1", "Параметр 2");
        String роздільник = "-".repeat(заголовок.length());
        String рядок = String.format("|%-" + ширинаСтовпця + ".2f|%-" + ширинаСтовпця + ".2f|", дані.отриматиПараметр1(), дані.отриматиПараметр2());
        System.out.println(роздільник);
        System.out.println(заголовок);
        System.out.println(роздільник);
        System.out.println(рядок);
        System.out.println(роздільник);
    }
}

/**
 * Клас для текстового відображення результату.
 */
class ТекстовийВідображувачРезультат implements Відображуваний {
    private final ДаніОбчислення дані;

    /**
     * Конструктор для створення відображувача результату.
     * @param дані Дані для відображення.
     */
    ТекстовийВідображувачРезультат(ДаніОбчислення дані) {
        this.дані = дані;
    }

    public void відобразитиПараметри() {
        System.out.println("Параметри (лише результат): недоступно");
    }

    public void відобразитиРезультат() {
        System.out.println("Результат: " + дані.отриматиРезультат());
    }

    public void відобразитиЯкТаблицю(int ширинаСтовпця) {
        System.out.println("Відображення результату у вигляді таблиці:");
        String заголовок = String.format("|%-" + ширинаСтовпця + "s|", "Результат");
        String роздільник = "-".repeat(заголовок.length());
        String рядок = String.format("|%-" + ширинаСтовпця + ".2f|", дані.отриматиРезультат());
        System.out.println(роздільник);
        System.out.println(заголовок);
        System.out.println(роздільник);
        System.out.println(рядок);
        System.out.println(роздільник);
    }
}

/**
 * Клас для повного текстового відображення (параметри + результат).
 */
class ТекстовийВідображувачПовний implements Відображуваний {
    private final ДаніОбчислення дані;

    /**
     * Конструктор для створення повного відображувача.
     * @param дані Дані для відображення.
     */
    ТекстовийВідображувачПовний(ДаніОбчислення дані) {
        this.дані = дані;
    }

    public void відобразитиПараметри() {
        System.out.println("Параметр 1: " + дані.отриматиПараметр1() + ", Параметр 2: " + дані.отриматиПараметр2());
    }

    public void відобразитиРезультат() {
        System.out.println("Результат: " + дані.отриматиРезультат());
    }

    public void відобразитиЯкТаблицю(int ширинаСтовпця) {
        System.out.println("Повне відображення у вигляді таблиці:");
        String заголовок = String.format("|%-" + ширинаСтовпця + "s|%-" + ширинаСтовпця + "s|%-" + ширинаСтовпця + "s|", "Параметр 1", "Параметр 2", "Результат");
        String роздільник = "-".repeat(заголовок.length());
        String рядок = String.format("|%-" + ширинаСтовпця + ".2f|%-" + ширинаСтовпця + ".2f|%-" + ширинаСтовпця + ".2f|", 
                                     дані.отриматиПараметр1(), дані.отриматиПараметр2(), дані.отриматиРезультат());
        System.out.println(роздільник);
        System.out.println(заголовок);
        System.out.println(роздільник);
        System.out.println(рядок);
        System.out.println(роздільник);
    }

    /**
     * Перевантажений метод для відображення таблиці з додатковим заголовком.
     * @param ширинаСтовпця Ширина стовпців таблиці.
     * @param заголовокТаблиці Заголовок таблиці.
     */
    public void відобразитиЯкТаблицю(int ширинаСтовпця, String заголовокТаблиці) {
        System.out.println(заголовокТаблиці);
        відобразитиЯкТаблицю(ширинаСтовпця);
    }
}

/**
 * Фабрика для створення відображувача параметрів.
 */
class ФабрикаПараметри implements ФабрикаВідображення {
    public Відображуваний створитиВідображувач(ДаніОбчислення дані) {
        return new ТекстовийВідображувачПараметри(дані);
    }
}

/**
 * Фабрика для створення відображувача результату.
 */
class ФабрикаРезультат implements ФабрикаВідображення {
    public Відображуваний створитиВідображувач(ДаніОбчислення дані) {
        return new ТекстовийВідображувачРезультат(дані);
    }
}

/**
 * Фабрика для створення повного відображувача.
 */
class ФабрикаПовний implements ФабрикаВідображення {
    public Відображуваний створитиВідображувач(ДаніОбчислення дані) {
        return new ТекстовийВідображувачПовний(дані);
    }
}

/**
 * Клас для тестування основної функціональності.
 */
class ТестФункціональності {
    /**
     * Тестує створення відображувачів і відображення даних.
     */
    static void тестуватиВідображення() {
        Калькулятор калькулятор = new Калькулятор(5.0, 3.0);
        ФабрикаВідображення фабрикаПараметри = new ФабрикаПараметри();
        ФабрикаВідображення фабрикаРезультат = new ФабрикаРезультат();
        ФабрикаВідображення фабрикаПовний = new ФабрикаПовний();

        Відображуваний відображувачПараметри = фабрикаПараметри.створитиВідображувач(калькулятор.отриматиДані());
        Відображуваний відображувачРезультат = фабрикаРезультат.створитиВідображувач(калькулятор.отриматиДані());
        Відображуваний відображувачПовний = фабрикаПовний.створитиВідображувач(калькулятор.отриматиДані());

        відображувачПараметри.відобразитиПараметри();
        відображувачРезультат.відобразитиРезультат();
        відображувачПовний.відобразитиЯкТаблицю(15);
    }

    /**
     * Тестує збереження та завантаження колекції.
     */
    static void тестуватиСеріалізацію() {
        ArrayList<ДаніОбчислення> колекція = new ArrayList<>();
        Калькулятор калькулятор = new Калькулятор(5.0, 3.0);
        колекція.add(калькулятор.отриматиДані());

        ДемонстраціяСеріалізації.зберегтиКолекцію(колекція, "тест_колекція.ser");
        ArrayList<ДаніОбчислення> завантаженаКолекція = ДемонстраціяСеріалізації.завантажитиКолекцію("тест_колекція.ser");

        if (завантаженаКолекція != null && завантаженаКолекція.size() == 1) {
            ДаніОбчислення дані = завантаженаКолекція.get(0);
            if (Math.abs(дані.отриматиПараметр1() - 5.0) < 0.0001 && Math.abs(дані.отриматиПараметр2() - 3.0) < 0.0001) {
                System.out.println("Тест серіалізації пройдено");
            } else {
                System.out.println("Тест серіалізації не пройдено");
            }
        } else {
            System.out.println("Тест серіалізації не пройдено: колекція не завантажена");
        }
    }
}

/**
 * Основний клас програми.
 */
public class Main {
    /**
     * Основний метод програми.
     * @param args Аргументи командного рядка.
     */
    public static void main(String[] args) {
        Scanner сканер = new Scanner(System.in);

        System.out.println("Введіть перший параметр:");
        double парам1 = сканер.nextDouble();
        System.out.println("Введіть другий параметр:");
        double парам2 = сканер.nextDouble();

        ArrayList<ДаніОбчислення> колекціяОбчислень = new ArrayList<>();
        Калькулятор калькулятор = new Калькулятор(парам1, парам2);
        колекціяОбчислень.add(калькулятор.отриматиДані());
        System.out.println("Результат: " + калькулятор.отриматиРезультат());

        ДемонстраціяСеріалізації.зберегтиКолекцію(колекціяОбчислень, "колекція_обчислень.ser");
        ArrayList<ДаніОбчислення> завантаженаКолекція = ДемонстраціяСеріалізації.завантажитиКолекцію("колекція_обчислень.ser");

        if (завантаженаКолекція != null) {
            for (ДаніОбчислення дані : завантаженаКолекція) {
                System.out.println("Завантажені параметри: " + дані.отриматиПараметр1() + ", " + дані.отриматиПараметр2());
            }
        }

        System.out.println("Введіть ширину стовпця для таблиці:");
        int ширинаСтовпця = сканер.nextInt();

        ФабрикаВідображення фабрикаПараметри = new ФабрикаПараметри();
        ФабрикаВідображення фабрикаРезультат = new ФабрикаРезультат();
        ФабрикаВідображення фабрикаПовний = new ФабрикаПовний();

        Відображуваний відображувачПараметри = фабрикаПараметри.створитиВідображувач(калькулятор.отриматиДані());
        Відображуваний відображувачРезультат = фабрикаРезультат.створитиВідображувач(калькулятор.отриматиДані());
        Відображуваний відображувачПовний = фабрикаПовний.створитиВідображувач(калькулятор.отриматиДані());

        відображувачПараметри.відобразитиПараметри();
        відображувачПараметри.відобразитиРезультат();
        відображувачПараметри.відобразитиЯкТаблицю(ширинаСтовпця);

        відображувачРезультат.відобразитиПараметри();
        відображувачРезультат.відобразитиРезультат();
        відображувачРезультат.відобразитиЯкТаблицю(ширинаСтовпця);

        відображувачПовний.відобразитиПараметри();
        відображувачПовний.відобразитиРезультат();
        відображувачПовний.відобразитиЯкТаблицю(ширинаСтовпця);
        ((ТекстовийВідображувачПовний) відображувачПовний).відобразитиЯкТаблицю(ширинаСтовпця, "Повна таблиця обчислень");

        ТестФункціональності.тестуватиВідображення();
        ТестФункціональності.тестуватиСеріалізацію();

        сканер.close();
    }
}
