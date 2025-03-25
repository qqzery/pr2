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
