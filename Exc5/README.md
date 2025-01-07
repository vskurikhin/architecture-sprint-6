# Задание 5. Проектирование GraphQL API


## Чек-лист:
- [x] проанализировать Swagger контракт client-inf
- [x] разработать эквивалентную схему GraphQL
- [x] определите сущности, их поля, а также необходимые запросы


## Примеры из Swagger:
1. Получить информацию о клиенте по ID:
```json
{
  "id": "string",
  "name": "string",
  "age": 0
}
```
2. Список документов клиента:
```json
[
  {
    "id": "string",
    "type": "string",
    "number": "string",
    "issueDate": "string",
    "expiryDate": "string"
  }
]
```
3. Информация о родственниках клиента
```json
[
  {
    "id": "string",
    "relationType": "string",
    "name": "string",
    "age": 0
  }
]
```