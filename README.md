# Event-driven architectures

---
# Зачем?

## 3-tier MSA

---
## ACID

[ACID](https://ru.wikipedia.org/wiki/ACID)

> Требования к [транзакционной системе](https://ru.wikipedia.org/wiki/%D0%A2%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D0%BE%D0%BD%D0%BD%D0%B0%D1%8F_%D1%81%D0%B8%D1%81%D1%82%D0%B5%D0%BC%D0%B0 "Транзакционная система") (например, к [СУБД](https://ru.wikipedia.org/wiki/%D0%A1%D0%A3%D0%91%D0%94 "СУБД")), обеспечивающие наиболее надёжную и предсказуемую её работу. Требования ACID были в основном сформулированы в конце 70-х годов [Джимом Греем](https://ru.wikipedia.org/wiki/%D0%94%D0%B6%D0%B8%D0%BC_%D0%93%D1%80%D0%B5%D0%B9 "Джим Грей")

    - [1 Atomicity — Атомарность](https://ru.wikipedia.org/wiki/ACID#Atomicity_—_Атомарность)
    - [2 Consistency — Согласованность](https://ru.wikipedia.org/wiki/ACID#Consistency_—_Согласованность)
    - [3 Isolation — Изолированность](https://ru.wikipedia.org/wiki/ACID#Isolation_—_Изолированность)
    - [4 Durability — Надежность](https://ru.wikipedia.org/wiki/ACID#Durability_—_Надежность)

---
## Изоляция транзакций

[Проблемы параллельного доступа с использованием транзакций](https://ru.wikipedia.org/wiki/%D0%A3%D1%80%D0%BE%D0%B2%D0%B5%D0%BD%D1%8C_%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8_%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D0%B9#Проблемы_параллельного_доступа_с_использованием_транзакций)

- [1 Потерянное обновление](https://ru.wikipedia.org/wiki/%D0%A3%D1%80%D0%BE%D0%B2%D0%B5%D0%BD%D1%8C_%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8_%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D0%B9#Потерянное_обновление)
- [2 «Грязное» чтение](https://ru.wikipedia.org/wiki/%D0%A3%D1%80%D0%BE%D0%B2%D0%B5%D0%BD%D1%8C_%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8_%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D0%B9#«Грязное»_чтение)
- [3 Неповторяющееся чтение](https://ru.wikipedia.org/wiki/%D0%A3%D1%80%D0%BE%D0%B2%D0%B5%D0%BD%D1%8C_%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8_%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D0%B9#Неповторяющееся_чтение)
- [4 Чтение «фантомов»](https://ru.wikipedia.org/wiki/%D0%A3%D1%80%D0%BE%D0%B2%D0%B5%D0%BD%D1%8C_%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8_%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D0%B9#Чтение_«фантомов»)

---
## Изоляция транзакций

[Уровень изолированности транзакций — Википедия](https://ru.wikipedia.org/wiki/%D0%A3%D1%80%D0%BE%D0%B2%D0%B5%D0%BD%D1%8C_%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8_%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D0%B9)

- [1 Read uncommitted (чтение незафиксированных данных)](https://ru.wikipedia.org/wiki/%D0%A3%D1%80%D0%BE%D0%B2%D0%B5%D0%BD%D1%8C_%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8_%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D0%B9#Read_uncommitted_(чтение_незафиксированных_данных))
- [2 Read committed (чтение фиксированных данных)](https://ru.wikipedia.org/wiki/%D0%A3%D1%80%D0%BE%D0%B2%D0%B5%D0%BD%D1%8C_%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8_%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D0%B9#Read_committed_(чтение_фиксированных_данных))
- [3 Repeatable read (повторяющееся чтение)](https://ru.wikipedia.org/wiki/%D0%A3%D1%80%D0%BE%D0%B2%D0%B5%D0%BD%D1%8C_%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8_%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D0%B9#Repeatable_read_(повторяющееся_чтение))
- [4 Serializable (упорядочиваемость)](https://ru.wikipedia.org/wiki/%D0%A3%D1%80%D0%BE%D0%B2%D0%B5%D0%BD%D1%8C_%D0%B8%D0%B7%D0%BE%D0%BB%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%BE%D1%81%D1%82%D0%B8_%D1%82%D1%80%D0%B0%D0%BD%D0%B7%D0%B0%D0%BA%D1%86%D0%B8%D0%B9#Serializable_(упорядочиваемость))

---
## Партиционирование

![](https://www.voltactivedata.com/wp-content/uploads/2017/02/cap-blog.jpg)

---
## CAP

`Iron triangle` of CAP theorem:

- consistency
- availability
- persistence

---
## CAP
![CAP](https://camo.githubusercontent.com/9ada962191fd954f77807669f350921fc69f6f8196af10af6812934b2ce77894/68747470733a2f2f6c68362e676f6f676c6575736572636f6e74656e742e636f6d2f2d424e5f383648544e6d4c452f54577248323775676e54492f41414141414141414151552f716f4f42337631573243772f73313630302f4341502e706e67)

---
## (A) vs функциональность

| Возьмите A | И откажитесь от ... |
|---|---|
| c(A)p | repeateble read; complete transactions |

---
## PIE

- Pattern Flexibility
    
- Efficiency
    
- Infinite Scale

---
## PIE
![PIE](https://camo.githubusercontent.com/1726e48fee17c0513a7cd88a88ff735927459396e02ee804f639de00bf74add1/68747470733a2f2f7062732e7477696d672e636f6d2f6d656469612f447746536f7675576b4149686e6b582e6a70673a6c61726765)


---
## CAP vs ACID consistency

| ACID consistency | CAP consistency |
|---|---|
|Уровень БД.  | Уровень кластера |
| ( уникальность значения, требования внешнего ключа) | ( копия значения в узлах - eventualy consistent ) | 


---
## BASE - Eventual Consistency

[best-practices/best-practices-for-building-a-microservice-architecture.md at master · katopz/best-practices](https://github.com/katopz/best-practices/blob/master/best-practices-for-building-a-microservice-architecture.md)

### Межсервисные транзакции

[Distributed transaction](https://en.wikipedia.org/wiki/Distributed_transaction)

### "Подумаю об этом завтра"

### "Правда всегда одна"

### А если-таки нужна консистентность?


---
# Итак, EDA

---
## EDA - Событийно-ориентированная архитектура 

[Событийно-ориентированная архитектуа](https://ru.wikipedia.org/wiki/%D0%A1%D0%BE%D0%B1%D1%8B%D1%82%D0%B8%D0%B9%D0%BD%D0%BE-%D0%BE%D1%80%D0%B8%D0%B5%D0%BD%D1%82%D0%B8%D1%80%D0%BE%D0%B2%D0%B0%D0%BD%D0%BD%D0%B0%D1%8F_%D0%B0%D1%80%D1%85%D0%B8%D1%82%D0%B5%D0%BA%D1%82%D1%83%D1%80%D0%B0)

Архитектура, управляемая событиями  (event-driven architecture, EDA) - шаблон архитектуры , позволяющий создание, определение, потребление и реакцию на события.

_Событие_ можно определить как «существенное изменение состояния. Например, когда покупатель приобретает автомобиль, состояние автомобиля изменяется с «продаваемого» на «проданный». Системная архитектура продавца автомобилей может рассматривать это изменение состояния как событие, создаваемое, публикуемое, определяемое и потребляемое различными приложениями в составе архитектуры.


---
## Событие

![](https://ic.pics.livejournal.com/legart/14901733/565645/565645_original.jpg)

---
## Event Collaboration. 

---
## Event for Transfer State

---
## Event Sourcing.

# Примеры

---
## lambda-refarch-webapp

[aws-samples/lambda-refarch-webapp: The Web Application reference architecture is a general-purpose, event-driven, web application back-end that uses AWS Lambda, Amazon API Gateway for its business logic. It also uses Amazon DynamoDB as its database and Amazon Cognito for user management. All static content is hosted using AWS Amplify Console.](https://github.com/aws-samples/lambda-refarch-webapp)

The Web Application reference architecture is a general-purpose, event-driven, web application back-end that uses [AWS Lambda](https://aws.amazon.com/lambda), [Amazon API Gateway](https://aws.amazon.com/apigateway) for its business logic. It also uses [Amazon DynamoDB](https://aws.amazon.com/dynamodb) as its database and [Amazon Cognito](https://aws.amazon.com/cognito) for user management. All static content is hosted using [AWS Amplify Console](https://aws.amazon.com/amplify/console).

This application implements a simple To Do app, in which a registered user can create, update, view the existing items, and eventually, delete them.

---
###  lambda-refarch-webapp - Architectural Diagram

[![Reference Architecture - Web Application](https://github.com/aws-samples/lambda-refarch-webapp/raw/master/img/serverless-refarch-webapp.png)](https://github.com/aws-samples/lambda-refarch-webapp/blob/master/img/serverless-refarch-webapp.png)
