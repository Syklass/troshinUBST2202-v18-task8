# Trivy Scan Workflow

## Описание
Данный репозиторий содержит GitHub Actions workflow для автоматического сканирования публичного Docker-образа `alpine/openssl` на наличие уязвимостей с помощью Trivy.

## Как это работает
- Workflow запускается автоматически при push, pull request или вручную через вкладку Actions.
- Используется официальный образ `alpine/openssl:latest` с Docker Hub.
- Сканирование выполняется с помощью Trivy, который запускается через Docker (без использования actions).
- Если найдены уязвимости уровня HIGH или CRITICAL, workflow завершится с ошибкой.
- Если таких уязвимостей нет — workflow будет успешным.

## Файл workflow
Файл находится по пути: `.github/workflows/trivy-scan.yml`

## Основные шаги workflow
1. Checkout репозитория
2. Запуск Trivy через Docker:
   ```sh
   docker run --rm -v /var/run/docker.sock:/var/run/docker.sock aquasec/trivy:latest image --exit-code 1 --severity HIGH,CRITICAL alpine/openssl:latest
   ```

## Автор
Выполнено студентом группы УБСТ2202 Трошиным В.А.

---

### Пример вывода
- **Успех:** Нет уязвимостей высокого уровня — зелёный статус.
- **Ошибка:** Найдены HIGH/CRITICAL уязвимости — красный статус.

## Как проверить
1. Залейте репозиторий на GitHub.
2. Перейдите во вкладку Actions.
3. Убедитесь, что workflow запускается и корректно реагирует на наличие/отсутствие уязвимостей.
