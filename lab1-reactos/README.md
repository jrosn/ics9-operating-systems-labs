# Лабораторная работа 1, ReactOS
## На Unix/Linux
### Этап 1, RosBE
Для начала скачаем, распакуем RosBE.
```sh
curl https://10gbps-io.dl.sourceforge.net/project/reactos/RosBE-Unix/2.1.2/RosBE-Unix-2.1.2.tar.bz2 | tar xvjf -
```
Установим RosBE.  
Иногда может потребоваться установить дополнительные пакеты. (легко гуглится, contrubute)
```sh
# На все вопросы жмем ENTER
sudo RosBE-Unix-2.1.2/RosBE-Builder.sh
```
### Этап 2, меняем исходники ReactOS'а
Скачаем исходники React'а и перейдем в каталог с ними.
```sh
git clone https://github.com/reactos/reactos reactos-src --depth=1 && cd reactos-src
```
Открываем файл `reactos-src/ntoskrnl/kd/kdio.c` и ищим в нем такую функцию.
```c
/* See also: kd64\kdinit.c */
static VOID
INIT_FUNCTION
KdpPrintBanner(IN SIZE_T MemSizeMBs)
{
    DPRINT1("-----------------------------------------------------\n");
    DPRINT1("ReactOS " KERNEL_VERSION_STR " (Build " KERNEL_VERSION_BUILD_STR ") (Commit " KERNEL_VERSION_COMMIT_HASH ")\n");
    DPRINT1("%u System Processor [%u MB Memory]\n", KeNumberProcessors, MemSizeMBs);
    DPRINT1("Command Line: %s\n", KeLoaderBlock->LoadOptions);
    DPRINT1("ARC Paths: %s %s %s %s\n", KeLoaderBlock->ArcBootDeviceName, KeLoaderBlock->NtHalPathName, KeLoaderBlock->ArcHalDeviceName, KeLoaderBlock->NtBootPathName);

    DPRINT1("Lab1, Roman Sosnovsky, special for ICS9\n"); // Вписываем эту строчку и меняем имя и фамилию на свою.
}
```
## Этап 3, сборка
Запускаем окружение разработчика -- RosBE.
```sh
/usr/local/RosBE/RosBE.sh
```
Переходим в каталог с исходники ReactOS'а, сконфигурируемся и начнем сборку.
```sh
cd reactos-src && ./configure.sh && cd output-MinGW-i386/reactos && ninja hybridcd
```
Все, мы собрали файл `hybridcd.iso`.
Загружаемся с него в VirtualBox и ставим.
