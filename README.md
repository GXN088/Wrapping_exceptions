# Wrapping_exceptions
В методе copyFile перехвати исключения, которые бросают методы readFile и writeFile.
Перехваченные исключения оберни в RuntimeException и пробрось дальше.

Псевдокод:

```
ПРОГРАММА Оборачивание исключений

КЛАСС FileUtils:
    МЕТОД readFile(строка filePath) БРОСАЕТ FileNotFoundException:
        Вывести "Читаем содержимое файла " + filePath
    
    МЕТОД writeFile(строка filePath) БРОСАЕТ FileSystemException:
        Вывести "Записываем данные в файл " + filePath

КЛАСС Solution:
    МЕТОД main(строка[] args):
        copyFile("book.txt", "book_final_copy.txt")
        copyFile("book_final_copy.txt", "book_last_copy.txt")
    
    МЕТОД copyFile(строка sourceFile, строка destinationFile):
        ПОПЫТАТЬСЯ:
            FileUtils.readFile(sourceFile)     // Чтение исходного файла
            FileUtils.writeFile(destinationFile) // Запись в файл назначения
        
        ПЕРЕХВАТИТЬ FileNotFoundException как e:
            ВЫБРОСИТЬ НОВОЕ RuntimeException(e)  // Оборачивание в RuntimeException
        
        ПЕРЕХВАТИТЬ FileSystemException как e:
            ВЫБРОСИТЬ НОВОЕ RuntimeException(e)  // Оборачивание в RuntimeException
```

Логика работы:

1. FileUtils - утилитный класс для работы с файлами:
   · readFile() - имитирует чтение файла, может выбросить FileNotFoundException
   · writeFile() - имитирует запись в файл, может выбросить FileSystemException
2. Solution - основной класс:
   · main() - вызывает копирование файлов
   · copyFile() - копирует файл путем чтения исходного и записи в целевой
   · Перехватывает проверяемые исключения и оборачивает их в непроверяемые RuntimeException

Особенности:

· Используется паттерн "оборачивания исключений"
· Проверяемые исключения преобразуются в непроверяемые
· Сохраняется оригинальная информация об исключении через конструктор с причиной
