<div align="center">

<h1 align="center"> <img alt="shine" src="https://github.com/user-attachments/assets/26606edd-32dd-4234-ab5f-2c837129c6f6" /> </h1>

**Форк DeltaV с уникальным контентом и геймплеем**

[![Discord](https://img.shields.io/discord/1039584848689496065?style=for-the-badge&logo=discord&logoColor=white&label=Discord&color=%237289da)](https://discord.gg/qcK4ZKFNUb)
[![GitHub License](https://img.shields.io/github/license/ss14-art/shine?style=for-the-badge)](https://github.com/ss14-art/shine/blob/master/LICENSE-AGPLv3.txt)
[![.NET](https://img.shields.io/badge/.NET-10.0-512BD4?style=for-the-badge)](https://dotnet.microsoft.com/)

</div>

---

## 📋 О проекте

**shine Project** — это форк [DeltaV](https://github.com/DeltaV-Station/Delta-v/), который в свою очередь основан на [Space Station 14](https://github.com/space-wizards/space-station-14). Проект сочетает классический хаос SS13 с экспериментальными механиками, возможными только на новом движке.

Space Station 14 — это remake SS13, работающий на [Robust Toolbox](https://github.com/space-wizards/RobustToolbox) — собственном движке, написанном на C#.

## 📚 Документация

- **[Официальная документация SS14](https://docs.spacestation14.io/)** — движок, контент, геймдизайн
- **[Robust Generic Attribution](https://docs.spacestation14.com/en/specifications/robust-generic-attribution.html)** — информация об атрибуции
- **[Robust Station Image](https://docs.spacestation14.com/en/specifications/robust-station-image.html)** — правила использования изображений

## 🤝 Контрибуция

Мы всегда рады помощи от всех желающих! Присоединяйтесь к [Discord](https://discord.gg/qcK4ZKFNUb), если хотите внести свой вклад.

У нас есть [список задач](https://github.com/ss14-art/shine/issues), которые нужно решить. Не стесняйтесь спрашивать помощь!

> **📖 Обязательно прочитайте [CONTRIBUTING.md](./CONTRIBUTING.md) перед отправкой Pull Request!**

## 🚀 Сборка проекта

### Требования

- **Git** — [скачать](https://git-scm.com/downloads)
- **.NET SDK 10.0 или выше** — [скачать](https://dotnet.microsoft.com/download/dotnet/10.0)
- **Python 3.11+** — [скачать](https://www.python.org/downloads/)

### Инструкция

> [!IMPORTANT]
> Убедитесь, что путь к папке проекта не содержит кириллицу или пробелы!

#### Windows / Linux / macOS

```bash
# 1. Клонируйте репозиторий
git clone https://github.com/ss14-art/shine.git
cd shine

# 2. Инициализируйте подмодули и загрузите движок
python RUN_THIS.py

# 3. Соберите проект
dotnet build

# 4. Запустите сервер
cd Content.Server
dotnet run

# 5. В отдельном терминале запустите клиент
cd ../Content.Client
dotnet run
```

#### Быстрый запуск (скриптами)

Если в проекте есть скрипты быстрого запуска:

```bash
# Windows
runclient.bat
runserver.bat

# Linux / macOS
chmod +x runclient.sh
chmod +x runserver.sh
runclient.sh
runserver.sh
```

После запуска подключитесь к **localhost** в окне клиента.

> **Более подробная инструкция**: [официальное руководство по сборке SS14](https://docs.spacestation14.com/en/general-development/setup.html)

## 📜 Лицензия

Подробную информацию о лицензиях смотрите в файле **[LEGAL.md](./LEGAL.md)**.

### Код

Весь код в этом репозитории распространяется под лицензией **GNU AGPLv3** (или более поздней версии). Каждый файл содержит информацию о лицензии в заголовке REUSE или отдельном `.license` файле.

### Ассеты (графика, звуки, спрайты)

Большинство ассетов лицензированы под **[CC-BY-SA 3.0](https://creativecommons.org/licenses/by-sa/3.0/)**, если не указано иное. Лицензия и информация об авторских правах содержатся в metadata файлах. [Пример](https://github.com/ss14-art/shine/blob/master/Resources/Textures/Objects/Tools/crowbar.rsi/meta.json).

> [!NOTE]
> Некоторые ассеты имеют некоммерческую лицензию **[CC-BY-NC-SA 3.0](https://creativecommons.org/licenses/by-nc-sa/3.0/)**. Они будут удалены, если вы планируете использовать проект в коммерческих целях.

---

<div align="center">

**🌟 shine Project — там, где станция сияет! 🌟**

</div>
