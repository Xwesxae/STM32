# Установка и первый запуск Renode
1. Зайти на https://renode.io/#downloads и скачать эмулятор
    
* Установть эмулятор (требуются права администратора)
2. Базовый рабочий процесс (на примере STM32)

* Смоделируем простую плату на базе STM32.

*В консоли Monitor вы создаете "машину" — это корневой объект, к которому будет привязана платформа.*

    (monitor) mach create
    (machine-0)

*Команда создаст машину с именем "machine-0"*

    (machine-0) peripherals
**peripherals** показывает подключенные перифирийные устройства 
# Сборка прошивки
 Теперь переходим к сборке прошивки для микроконтроллера при помощи одного их готовых инструментов:

        git clone https://github.com/PhanCuong91/data.git
        Клонирование репозитория с инструментом 

        cd data/renode
        Переход в подпапку /renode в /data

        Дальше следует запуск  build.bat

        После этого создается файл прошивки по пути
        "...data\renode\build\src\STM32F4Template.elf"

        Теперь у нас есть готовый файл прошивки

# Установка на эмулируемый контроллер
В Renode:

        mach create
        # Создание машины (По умолчанию machine-0)

        machine LoadPlatformDescription @platforms/boards/stm32f4_discovery-kit.repl
        # Загрузка готовой конфигурации микроконтроллера

        sysbus LoadELF "C:\working\data\renode\build\src\STM32F4Template.elf"
         # Здесь должен быть путь к файлу прошивки

        # открытие терминала для отображения данных UART
        showAnalyzer sysbus.usart2

        # запуск симуляции
        start

**Как итог в новом терминале у нас должно появиться сообщение "Hello World"**
