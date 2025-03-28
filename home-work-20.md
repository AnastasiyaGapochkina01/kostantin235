1) Запустить на ВМ gitlab-runner как systemd-unit
2) Создать пустой репозиторий в gitlab, подключить к нему запущенный runner
3) Написать пайплайн, который будет состоять из 3 stages: bulid, test, deploy. В каждом stage должна быть одна job
- run build должна выводить сообщение ```Building project release```
- run tests должна выводить сообщение ```Running tests```
- run deploy должна выводить сообщение ```Deploy to ENV```
4) Создать репозиторий, который будет содержать следующие файлы
main.py
```
import argparse
from markdown_pdf import MarkdownPdf, Section

def convert_markdown_to_pdf(input_file, output_file):
    pdf = MarkdownPdf(toc_level=2)  # Уровень оглавления (TOC)

    try:
        with open(input_file, 'r', encoding='utf-8') as file:
            markdown_content = file.read()
    except FileNotFoundError:
        print(f"Файл {input_file} не найден.")
        return

    pdf.add_section(Section(markdown_content))

    pdf.save(output_file)
    print(f"PDF успешно создан: {output_file}")

if __name__ == "__main__":
    parser = argparse.ArgumentParser(description='Конвертирует Markdown в PDF')
    parser.add_argument('-i', '--input', help='Путь к входному Markdown файлу', required=True)
    parser.add_argument('-o', '--output', help='Путь к выходному PDF файлу', required=True)

    args = parser.parse_args()

    input_markdown = args.input
    output_pdf = args.output

    convert_markdown_to_pdf(input_markdown, output_pdf)

```
main.go
```
package main

import (
    "bufio"
    "fmt"
    "os"
    "strconv"
)

func main() {
    // Создаем новый сканер для чтения ввода пользователя
    scanner := bufio.NewScanner(os.Stdin)

    fmt.Println("Simple calculator")
    fmt.Println("1. addition")
    fmt.Println("2. subtraction")
    fmt.Println("3. multiplication")
    fmt.Println("4. division")

    // Запрашиваем у пользователя номер операции
    fmt.Print("Enter the operation number: ")
    scanner.Scan()
    operation, err := strconv.Atoi(scanner.Text())
    if err != nil {
        fmt.Println("Incorrect input")
        return
    }

    // Запрашиваем два числа
    fmt.Print("Enter first number: ")
    scanner.Scan()
    num1, err := strconv.ParseFloat(scanner.Text(), 64)
    if err != nil {
        fmt.Println("Incorrect input")
        return
    }

    fmt.Print("Enter second number: ")
    scanner.Scan()
    num2, err := strconv.ParseFloat(scanner.Text(), 64)
    if err != nil {
        fmt.Println("Incorrect input")
        return
    }

    // Выполняем операцию
    var result float64
    switch operation {
    case 1:
        result = num1 + num2
        fmt.Printf("%.2f + %.2f = %.2f\n", num1, num2, result)
    case 2:
        result = num1 - num2
        fmt.Printf("%.2f - %.2f = %.2f\n", num1, num2, result)
    case 3:
        result = num1 * num2
        fmt.Printf("%.2f * %.2f = %.2f\n", num1, num2, result)
    case 4:
        if num2 != 0 {
            result = num1 / num2
            fmt.Printf("%.2f / %.2f = %.2f\n", num1, num2, result)
        } else {
            fmt.Println("Division by zero!")
        }
    default:
        fmt.Println("Incorrect operation number")
    }
}

```
- написать пайплайн, состоящий из одного stage с двумя jobs: одна из них должна прогонять линтер для main.py (код на python); вторая должна прогонять линтер для main.go (код на golang) (линтеры найти самостоятельно)
