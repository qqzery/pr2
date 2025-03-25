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

import java.io.Serializable;

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
