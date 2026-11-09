# ai-engineering-course

# Troubleshooting

### 1. `'ascii' codec can't encode characters`
**Что видел:** ошибка при запуске после того, как вписал сломанный ключ.

**Почему:** в `GIGACHAT_CREDENTIALS` попали русские буквы, а ключ уходит в HTTP-заголовок, где допустим только латинский текст.

**Что сделал:** вернул настоящий ключ (латиница + цифры). Заодно убедился, что благодаря fallback скрипт не упал, а ответил через `[HuggingFace]`.


### 2. Invalid credentials format. Please use only base64 credentials (Authorization data, not client secret!)
**Что видел:** ошибка при запуске после того, как вписал случайный набор латинских букв и цифр после первой буквы ключа.

**Почему:** большинство современных API используют Base64 для передачи токенов или иных данных. Сервер ожидает увидеть строку определенной длины и набора символов. При вставке случайных символов нарушается структура Base64

**Что сделал:** исправил ключ. Кроме того, благодаря fallback скрипт не упал, а ответил через `[HuggingFace]`.


### 3. ModuleNotFoundError: No module named 'dotenv'
**Что видел:** ошибка при запуске после деактивирования .venv следующего содержания:
Traceback (most recent call last):
  File "C:\Users\IgorA\source\repos\MyProjects\Магистратура_1курс_2026\ИИ в Промтехе\Lab1\ai-engineering-course\module_01\llm_client.py", line 21, in <module>
    from dotenv import load_dotenv

**Почему:** пакет python dotenv установлен внутри виртуального окружения, но отсутствует в глобальной системе Python. При деактивации окружения .venv терминал переключился на использование глобального интерпретатора Python.

**Что сделал:** активировал окружение .venv\Scripts\activate в корне проекта


### 4. 401 Anauthorized
**Что видел:** сообщение об ошибке вида
[!] GigaChat недоступен: (URL('https://ngw.devices.sberbank.ru:9443/api/v2/oauth'), 401, b'{"code":6,"message":"credentials doesn\'t match db data"}', Headers([('server', 'SynGX'), ('date', 'Tue, 15 Sep 2026 13:51:50 GMT'), ('content-type', 'application/json'), ('content-length', '56'), ('connection', 'keep-alive'), ('vary', 'Origin'), ('vary', 'Access-Control-Request-Method'), ('vary', 'Access-Control-Request-Headers'), ('cache-control', 'no-cache, no-store, max-age=0, must-revalidate'), ('pragma', 'no-cache'), ('expires', '0'), ('x-content-type-options', 'nosniff'), ('strict-transport-security', 'max-age=31536000 ; includeSubDomains'), ('x-frame-options', 'DENY'), ('x-xss-protection', '0'), ('referrer-policy', 'no-referrer'), ('allow', 'GET, POST'), ('strict-transport-security', 'max-age=31536000; includeSubDomains')]))

**Почему:** был указан неверный ключ для доступа к модели в файле .env

**Что сделал:** вернул корректный ключ. Кроме того, убедился, что смена провайдера была совершена корректно.




