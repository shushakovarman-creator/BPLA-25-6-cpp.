# СРС#2 и СРС#3 — Информационная система ВУЗа

## Инструкция по компиляции и запуску
```bash
g++ main.cpp -o bot -pthread
./bot
## Code Review & Vulnerability Analysis

### 1. Бесконечный цикл при некорректном типе ввода (std::cin)
* **Описание проблемы:** При запросе пункта меню (ожидается `int`) ввод символа или строки (например, `"abc"`) переводит поток `std::cin` в состояние ошибки (`failbit`). Переменная не считывается, и цикл `while(true)` уходит в бесконечный вывод меню.
  * *Тестовый ввод:* Ввод строки `"test"` вместо номера пункта меню.
  * *Результат:* Зависание программы, зацикливание вывода в консоль.
* **Потенциальные последствия:** В реальной системе ВУЗа лаборант или студент потеряет несохраненные данные протокола, программа перестанет отвечать на команды, потребуется принудительное завершение процесса.
* **Предлагаемое решение:** Добавить сброс флагов ошибки и очистку буфера ввода.
  ```cpp
  if (!(std::cin >> choice)) {
      std::cin.clear(); // Сброс флагов ошибки
std::string filename = "protocol.txt"; // Сохраняем в текущую директорию программы
std::ofstream file(filename, std::ios::app);
if (index >= 0 && index < articles.size()) {
    auto selected = articles.at(index);
} else {
    std::cout << "Неверный номер статьи!\n";
}
constexpr int MAX_DAYS_WITHOUT_PENALTY = 30;
constexpr double PENALTY_COEFFICIENT = 1.5;
std::ofstream file("protocol.txt", std::ios::app);
if (!file.is_open()) {
    std::cerr << "Ошибка: Не удалось открыть файл для записи протокола!\n";
    return false;
}

      std::cin.ignore(std::numeric_limits<std::streamsize>::max(), '\n'); // Очистка буфера
      std::cout << "Ошибка! Введите число.\n";
  }
