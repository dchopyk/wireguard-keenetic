# Генератор конфига WireGuard-сервера для роутеров Keenetic

**Этот скрипт предназначен для генерирования конфигурационных файлов [WireGuard](https://www.wireguard.com/) VPN для Keenetic-роутеров.**

Wire Guard - это протокол VPN типа "точка-точка", который предлагает различные возможности использования. В данном контексте мы имеем в виду VPN, при котором трафик клиента надежно туннелируется к серверу.

Этот скрипт пока поддерживает только IPv4. При обнаружении багов, пожалуйста сообщайте в [проблемы](https://gitflic.ru/project/denischopyk/wireguard-keenetic/issue) постараюсь решить по возможности.

Скрипт я полностью не писал с нуля, а лишь портировал с аналогичного: [wireguard-mikrotik](https://github.com/IgorKha/wireguard-mikrotik)


## Требования

Пакеты:

- wireguard-tools
- qrencode

Поддерживаемые дистрибутивы:

- Ubuntu >= 16.04
- Debian >= 10
- Fedora
- CentOS
- Arch Linux
- Oracle Linux

## Ипользование

Скачайте и выполните этот скрипт от root-пользователя.

```bash
wget https://raw.githubusercontent.com/dchopyk/wireguard-keenetic/main/wireguard-keenetic.sh -O wireguard-keenetic.sh
chmod +x wireguard-keenetic.sh
./wireguard-keenetic.sh
```

Как только запустите скрипт, вам предложит ввести имя Wireguard-подключения. Перед тем, как выбрать имя, подключитесь по SSH к роутеру и введите 

```
show interfaces
```

В списке интерфейсов ищите с именем Wireguard1, Wireguard2, Wireguard3. Выберите следующий свободный и укажите его в скрипте.
После того, как скрипт сгенерировал конфиг - найдите в папке wireguard/Wireguard1/Wireguard1.cfg, откройте в любом редакторе и скопируйте с него всё содержимое в консоль Keenetic.  
## Структура

```text
.
├── wireguard
│   ├── Wireguard1 - WireGuard interface name (server name)
│   │   ├── client - clients config folder
│   │   │   └── user1
│   │   │       ├── keenetic-peer-Wireguard1-client-user1.cfg  - Keenetic peer config [server side]
│   │   │       ├── Wireguard1-client-user1.conf - config file for your client
│   │   │       └── Wireguard1-client-user1.png - and QR client config
│   │   ├── keenetic
│   │   │   └── Wireguard1.cfg - paste in your keenetic console
│   │   ├── params
│   │   └── Wireguard1.conf
│   └── Wireguard2 - WireGuard interface name (server name)
│       ├── client - clients config folder
│       │   ├── user1
│       │   │   ├── keenetic-peer-Wireguard2-client-user1.cfg - paste in your keenetic console
│       │   │   ├── Wireguard2-client-user1.conf
│       │   │   └── Wireguard2-client-user1.png
│       │   └── user2
│       │       ├── keenetic-peer-Wireguard2-client-user2.cfg - paste in your keenetic console
│       │       ├── Wireguard2-client-user2.conf
│       │       └── Wireguard2-client-user2.png
│       ├── keenetic
│       │   └── Wireguard2.cfg - paste in your keenetic console
│       ├── params
│       └── Wireguard2.conf
└── wireguard-keenetic.sh
```
