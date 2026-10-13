## Purpose

Позволить сотруднику понять автора, основание и источники каждого ответа и увидеть оценку жителя без смешения разных видов оценок.

## ADDED Requirements

### Requirement: Answer views derive from the accepted conversation

После принятия detail-контракта блок «Оценки» SHALL включать messages с rating != null, а вкладка «Ответы» — все non-user сообщения, включая оператора. Оба представления SHALL использовать порядок и данные того же snapshot, что и переписка, без отдельных endpoints. Вопрос SHALL быть ближайшим предшествующим сообщением user; при его отсутствии UI MUST NOT выдумывать вопрос.

#### Scenario: Several answers to one question

- **WHEN** за одним сообщением жителя идут ответы навыка, подсистемы и оператора
- **THEN** все три ответа отображаются с одним предшествующим вопросом и собственным автором

#### Scenario: Question contains only an attachment

- **WHEN** ближайшее user-сообщение имеет text=null и вложение
- **THEN** оно остаётся вопросом ответа и не заменяется более ранним текстовым сообщением

#### Scenario: Answer precedes first user message

- **WHEN** первым сообщением snapshot является ответ
- **THEN** UI явно показывает отсутствие предшествующего вопроса, не падает и сохраняет ответ

### Requirement: Message ratings are distinct from operator performance

Оценка сообщения SHALL показывать good/poor, reason и comment отдельно от operator_rating 1–5 диалога. Poor SHALL оставаться видимой даже без comment; причина и комментарий SHALL быть доступны без обязательного hover и не обозначаться одним цветом. UI MUST NOT предлагать сотруднику изменение оценки без отдельного контракта.

#### Scenario: Poor without comment

- **WHEN** rating.value=poor, reason задана, comment=null
- **THEN** показаны плохая оценка и причина без пустого фиктивного комментария

#### Scenario: Operator message is rated

- **WHEN** сообщение оператора имеет good, а operator_rating диалога равен 3
- **THEN** ответ показывает good, оценка работы оператора остаётся 3 из 5; значения не заменяют друг друга

### Requirement: Author basis and sources are independent

Ответ SHALL различать author, basis.kind и basis.sources. SHALL поддерживаться external_system, knowledge_base, model, operator_template, no_data с соответствующим пояснением. Basis=null SHALL означать, что основание не сообщено, а не no_data. UI MUST NOT выводить вид основания из текста ответа или подставлять модель при отсутствии данных.

#### Scenario: Unknown basis versus no data

- **WHEN** у одного ответа basis=null, а у другого basis.kind=no_data
- **THEN** первый показывает отсутствие сведений об основании, второй — отсутствие подходящих данных в источниках

#### Scenario: Multiple knowledge sources

- **WHEN** knowledge_base содержит две статьи с relevance 0.87 и null
- **THEN** обе статьи показаны в исходном порядке, первая со значением 0,87, вторая без вымышленного нуля

### Requirement: Sources have truthful safe navigation

Источники SHALL показывать доступные title/code/url/relevance. Отсутствующий url MUST NOT превращаться в ссылку-заглушку; небезопасные схемы MUST NOT исполняться. Ссылка на навык SHALL требовать подтверждённое соответствие service_id и route ID. Время ответа SHALL отличаться подписью от времени вопроса; тексты SHALL рендериться безопасно.

#### Scenario: Article has no URL

- **WHEN** статья или операторский шаблон содержит title/code, но url=null
- **THEN** источник показан текстом без кликабельной фиктивной ссылки

#### Scenario: Service identifier is not a route identifier

- **WHEN** author.id=gkh.water и подтверждённый resolver UUID отсутствует
- **THEN** показаны название и код, но не ссылка на несуществующую карточку `/skills/gkh.water`
