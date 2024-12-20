> [!attention] Данная инструкция служит исключительно для настройки доступа к легальным сервисам, самостоятельно ограничившим доступ для пользователей из России по собственной политике. Она не предназначена для обхода блокировок, установленных российским законодательством для запрещённых в РФ ресурсов.

# Настраиваем VPN VLESS с XTLS-Reality через 3X-UI панель.

## Введение

Эта инструкция поможет вам настроить свой собственный VPN с использованием протокола VLESS с XTLS-Reality через панель 3X-UI. Данное решение обеспечивает высокий уровень безопасности и скрытность трафика, что делает его подходящим для использования в странах с ограничениями, таких как Китай и Иран. Основная идея заключается в шифровании трафика с использованием HTTPS и маскировке под популярные домены, что затрудняет его блокировку провайдером.

## Что потребуется для настройки?

- Арендованный сервер с установленной Ubuntu 22.04 или новее.
- 15 минут свободного времени.

### Как арендовать сервер для работы VPN?

1. **Регистрация на Timeweb Cloud**. Перейдите на сайт Timeweb Cloud и зарегистрируйтесь.
2. После регистрации выберите "Создать -> Облачный сервис" в общем проекте.

![[Pasted image 20241108183651.png]]

3. В качестве операционной системы выберите Ubuntu 22.04.
4. Выберите страну сервера, например, Польшу. Отключите бэкапы, так как они не нужны, и выберите минимальную конфигурацию сервера.

![[Pasted image 20241108183813.png]]

5. Нажмите "Заказать" и дождитесь завершения настройки сервера.
6. На почту придут IP-адрес сервера и данные для доступа.

## Настройка VPN VLESS с XTLS-Reality на сервере

1. **Подключение к серверу по SSH**  
   ```sh
   ssh root@ip_adress
   ```
   Где `ip_adress` — IP-адрес вашего сервера. При первом подключении подтвердите соединение, введя "yes".

2. **Обновление компонентов системы**  
   ```sh
   apt update && apt upgrade -y
   ```

3. **Установка Curl**  
   Установите утилиту Curl для загрузки файлов:  
   ```sh
   apt install curl -y
   ```

4. **Установка панели 3X-UI**  
   Выполните команду для установки панели 3X-UI:  
   ```sh
   bash <(curl -Ls https://raw.githubusercontent.com/mhsanaei/3x-ui/master/install.sh)
   ```
   Во время установки ответьте утвердительно на запрос настройки, нажав `Y`. 
   Далее введите `username`, `password` и номер порта (любое число от 2000 до 65535).

5. **Настройка веб-панели управления 3X-UI**  
   - Откройте браузер и перейдите по адресу: `http://<IP-адрес вашего сервера>:<порт>/panel/`.

![[Pasted image 20241108184036.png]]

   - Введите логин и пароль, чтобы попасть в панель управления.

![[Pasted image 20241108184150.png]]

6. **Добавление подключения в панель**  
   - Перейдите в раздел "Подключения" и выберите "Добавить подключение".

  ![[Pasted image 20241108184224.png]]

   - В настройках выберите:  
     - **Примечание** — любое название.
     - **Протокол** — `vless`.
     - **Порт** — установите `443`.

7. Переходим к настройкам **Клиента**.

	- **Email** – Напишите название клиента.
	- **Flow** — надо выбрать **xtls-rprx-vision.** Поле Flow появится только после того, как чуть ниже вы поставите галочку на пункте **Reality**.

8. Настроим транспорт.

	- **Протокол** **передачи****:** TCP
	- **AcceptProxyProtocol, HTTP** **Маскировка****, Transparent Proxy, TLS** — всё это должно быть **выключено**
	- **xVer —** оставьте значение **0**
	- **Reality** — должно быть **включено**
	- **XTLS** — наоборот, должно быть **выключено**.
	- **uTLS** — тут надо выбрать то, под какой браузер будет маскироваться наше VPN соединение. Но, можете выбрать **chrome** – так будет лучше всего.
	- **Домен** — на самом деле это адрес для подключения к вашему серверу. Оставьте пустым, и тогда туда автоматически подставится IP-адрес сервера.
	- **Dest —** это destination, то есть «назначение» — тут указываем домен и порт для переадресации **google.com:443**
	- **Server names** — это домен, под который вы будете маскироваться. Меням на **google.com,** **www.google.com**
	- **ShortIds —** это приватный ключ, сгенерируется автоматически.
	- **Public Key, Private Key** — нажмите на кнопку **Get new keys,** и ключи сгенерируются автоматически.
	- **Sniffing, HTTP, TLS, QUIC, fakedns** — оставьте включённым.

9. После нажатия кнопки **Создать**, настройку можно считать завершенной!

## Как использовать VPN на различных устройствах?

- Скачайте соответствующее приложение для **iOS**, **Android**, **macOS** или **Windows**.
- Настройте клиент аналогично, выгрузив конфигурацию с сервера.
- Самый простой способ — сгенерировать QR-код через веб-интерфейс и отсканировать его на устройстве.
- Из этой статьи можно скачать подходящий клиент для различных платформ: [Клиенты VLESS, Shadowsocks, Trojan (Xray, Sing-box) для Windows, Android, iOS, MacOS, Linux](https://itdog.info/klienty-vless-shadowsocks-trojan-xray-sing-box-dlya-windows-android-ios-macos-linux/#v2rayng)

## Заключение

Теперь ваш VPN VLESS с XTLS-Reality настроен и готов к использованию. С его помощью вы можете получать доступ к таким сервисам, как Adobe, OpenAI, Anthropic, Midjourney, Canva, Notion, а также GitHub, Slack, Figma, Trello и Asana — при условии, что ваши учетные записи на этих платформах не заблокированы.

#Vpn 