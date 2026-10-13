## 1. Gate маршрута

- [x] 1.1 Подтвердить route-контракт MOS-1041, traced_sec/untraced_sec и источник operator_actions; результат — принятое решение в design и явное отсутствие обещания step/message deep links без IDs.

## 2. Вкладка

- [x] 2.1 Добавить список шагов и легенду пяти kind в приватную вкладку карточки; component-тестами проверить исходный порядок, одинаковые времена, длительности ms, null detail и безопасный текст.
- [x] 2.2 Добавить блок сбоя и серверные итоги покрытия; тестами проверить failed=true, отличие суммы duration_ms от traced_sec, traced_sec>duration_sec, untraced_sec=0 и null без клиентского пересчёта.
- [x] 2.3 Добавить available=false/empty и блок действий операторов; component-тестами проверить недоступность без блокирования переписки, пустой список действий, двух авторов и 0–2 строки details.

## 3. Приёмка

- [x] 3.1 Проверить замену snapshot и отсутствие route-запросов/синтетических событий при смене вкладки component-тестами; выполнить `yarn typecheck`, `yarn lint`, `yarn test`, `yarn format:check` и `yarn api:check` при изменении DTO. Просмотреть diff; browser/E2E не создавать/не запускать, `yarn build` — при изменении сборки.
