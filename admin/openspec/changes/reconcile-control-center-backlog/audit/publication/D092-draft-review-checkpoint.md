# D092 — результат независимого review drafts

Reviewer run 84521471-9dec-4b29-812c-39f23fbea4ab завершён на Astra low. Parent полностью прочитал reviews/R-D092-DRAFTS.md.

- Surface package: ACCEPT локального planning draft, без обязательных правок. Публикация удерживается до успешной source freshness проверки.
- Dialog package: REVISE. Трёх row corrections замечание не касается; полный MODIFIED block lossless. Reset-предикат applied selection + pending quick filters неполон: при default applied/quick и изменённом неприменённом complex draft он скрывает существующий глобальный reset, сейчас очищающий draft через remount. Формулировка «policy вне scope» не сохраняет поведение. Нужен явный продуктовый выбор либо незавершённый implementation gate до такой развилки; автор/parent не выбирают поведение автоматически.

Вопрос пользователю: считать изменения только в неприменённых сложных условиях основанием показывать общий сброс? Рекомендуется да — это сохраняет имеющуюся возможность очистить draft глобальным сбросом. После ответа требуется согласованная правка proposal/design/reset delta/tasks и component-сценарий complex-only draft; сохранить отдельную очистку группы/закрытие без применения.

Последняя попытка freshness Jira завершилась Failed to fetch; причина не установлена. Не подменять её историческим snapshot и не объявлять freshness пройденным. Новые changes не scaffolded/published. Нет работающих agents или новых feature-checkbox отметок; global11/28. Existing evidence counts 86P/1B/86U, не feature completion.
