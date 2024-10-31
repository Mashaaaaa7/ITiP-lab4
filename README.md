# ITiP-lab4
//1
public class ArrayAverage {

    public static double calculateAverage(int[] arr) {
        if (arr == null || arr.length == 0) {
            System.err.println("Массив пуст или равен нулю");
            return Double.NaN;// Возвращаем NaN для пустого массива
        }
        int sum = 0;
        for (int num : arr) {
            sum += num;
        }
        return (double) sum / arr.length;
    }

    public static void main(String[] args) {
        int[] arr = {3,4,5,5};
        double sum;

        try {
            sum = calculateAverage(arr);
            if (Double.isInfinite(sum)) { // Проверка на бесконечность
                System.err.println("Ошибка: деление на ноль.");
            } else {
                System.out.println("Среднее арифметическое " + sum);
            }
        } catch (Exception a) {
            System.err.println("Другая причина ошибки" + a.getMessage());
        }
    }
}

//2
import java.io.FileWriter;
import java.io.IOException;

public class CustomAgeException extends Exception { //Exception-исключение
    public CustomAgeException(String message) {
        super(message);//принимает строку message, которую использует для сообщения об ошибке.
    }
}

class CheckAge {

    public static void main(String[] args) {
        int age = 150;

        try {
            checkAge(age);
            System.out.println("Возраст корректен");
        } catch (CustomAgeException e) {
            System.err.println("Ошибка: " + e.getMessage());
            logException(e); // пишет исключения в файл
        }
    }

    private static void checkAge(int age) throws CustomAgeException { //метод, который проверяет возраст throw-бросить
        if (age < 0 || age > 120) {
            throw new CustomAgeException("Недопустимый возраст: " + age);
        }
    }

    private static void logException(Exception e) {
        try (FileWriter writer = new FileWriter("error.log", true)) { // открываем файл для записи
            writer.write(e.getMessage() + "\n"); // записываем сообщение об ошибке
        } catch (IOException ex) {
            System.err.println("Ошибка при записи в файл: " + ex.getMessage());
        }
    }
}

//3
import java.io.BufferedReader;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;

public class readFile {

    public static void main(String[] args) {

        try (BufferedReader reader = new BufferedReader(new FileReader("src/readfile"))) {

            String line;

            while ((line = reader.readLine()) != null) {
                System.out.println(line);
            }

        } catch (FileNotFoundException e) {
            System.out.println("Файл не найден");
        } catch (IOException e) {
            System.err.println("Ошибка: " + e.getMessage());
        }

    }

}
