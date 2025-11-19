# 1. Установка Renode
Windows:
bash
Скачать с официального сайта:
https://renode.io/
Или через chocolatey:
choco install renode
Linux:
bash
Ubuntu/Debian
wget https://github.com/renode/renode/releases/latest/download/renode_*_amd64.deb
sudo dpkg -i renode_*_amd64.deb
macOS:
bash
brew install --cask renode
# 2. Запуск Renode
bash
renode
После запуска вы увидите:

text
RENODE™
Renode, version X.X.X
(monitor)
# 3. Быстрый запуск STM32 эмулятора
Способ 1: Готовые платформы
python
i @scripts/single-node/stm32f4_discovery.resc
Способ 2: Минимальная конфигурация
python
mach create
machine LoadPlatformDescriptionFromString "cpu: CPU.ArmCortexM4 @ sysbus"
showAnalyzer sysbus.uart2
start
# 4. Проверка что эмулятор работает
python
Проверить регистры
cpu PrintRegisters

Проверить память  
sysbus ReadDoubleWord 0x08000000

Тест записи/чтения
sysbus WriteDoubleWord 0x20000000 0x12345678
sysbus ReadDoubleWord 0x20000000

Запустить эмуляцию
start

Остановить
pause
# 5. Основные команды управления
python
Информация
help
version
mach list

Управление эмуляцией
start
pause
reset

Отладка
cpu PerformanceInMips 1
machine StartGdbServer 3333

Выход
quit
# 6. Загрузка прошивки
python
Загрузка ELF файла
sysbus LoadELF @firmware/test.elf

Загрузка бинарного файла
sysbus LoadBinary @firmware/test.bin 0x08000000
# 7. Работа с периферией
python
Показать все периферийные устройства
machine LogPeripherals

Мониторинг UART
showAnalyzer sysbus.uart2

Работа с GPIO
gpioA Toggle 5
# 8. Решение проблем
Если команда не работает:
Проверьте синтаксис

Убедитесь что находитесь в (monitor)

Используйте правильные имена устройств

Если платформа не найдена:
python
Проверить доступные платформы
include @scripts/single-node/
include @platforms/cpus/
Если не видно результатов:
Проверьте окно UART анализатора

Убедитесь что эмуляция запущена (start)

# 9. Полезные сочетания
Ctrl+C - остановить эмуляцию

Tab - автодополнение команд

Стрелки вверх/вниз - история команд

# 10. Выход из эмулятора
python
quit
Важно: Все команды вводятся в (monitor), а не в окнах UART!

