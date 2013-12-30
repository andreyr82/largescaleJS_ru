---
layout: page
title: "Тест. Глава 2. Давайте обсудим вашу существующую архитектуру"
---

<!-- ### Давайте обсудим вашу существующую архитектуру -->

Если вы работаете над большим JavaScript приложением, не забывайте уделять 
**достаточно времени** на планирование базовой архитектуры, к которой очень
чувствительны подобного рода приложения. Большие приложения обычно представляют
из себя очень сложные системы. Гораздо более сложные, чем вы себе их
представляете изначально.

Я должен подчеркнуть значение этой разницы — я видел разработчиков, которые,
сталкиваясь с большими приложениями, делали шаг назад и говорили: «Хорошо,
У меня есть несколько идей и подходов, которые хорошо показали себя в моем
предыдущем средне-масштабном проекте. Вне всякого сомнения, они сработают и
на чем-то большем, верно?». Конечно, это может быть до какой-то степени верным,
но, пожалуйста, не принимайте это как доложное — большие приложения в основном
имеют ряд достаточно серьезных проблем, с которыми нужно считаться. Ниже я
приведу немного доводов о том, почему вам стоит потратить чуть больше времени 
на планирование архитектуры своего приложения, и чем это будет вам полезно
в долгосрочной перспективе.

Большинство JavaScript разработчиков в архитектуре своих приложений обычно
использует различные комбинации из следующих компонентов:

*   custom widgets
*   models
*   views
*   controllers
*   templates
*   libraries/toolkits
*   an application core.

Вы, вероятно, так же разбиваете различные функции ваших приложений на наборы
модулей. Либо используете какие-то иные паттерны для подобного разделения. Это
замечательно, но здесь есть несколько потенциальных проблем, с которыми вы
можете столкнуться, используя такой подход.


### 1. Подразумевает ли ваша архитектура к переиспользование кода прямо сейчас?

Могут ли отдельные модули использоваться самостоятельно? Являются ли они
автономными? Мог бы я прямо сейчас взять один из модулей вашего большого 
приложения, просто поместить его на новую веб-страницу, и тут же начать этот
модуль использовать? Вы можете задаться вопросом «Действительно ли это
необходимо?», как бы то ни было, я надеюсь, что вы думаете о будущем. Что, 
если ваша компания начнет создавать все больше и больше нетривиальных
приложений, которые будут имеють некоторую общую функциональность? Если кто-то
скажет «Нашим пользователям очень нравится использовать модуль чата в нашем
email-клиенте. Давайте добавим этот модуль к нашему новому приложению для
совместной работы с докуменатми!», будет ли это возможно, если мы не уделим
должного внимания контролю изменений кода? (???)


### 2. Сколько модулей в вашей системе зависит от других модулей?

Насколько сильно связаны ваши модули? Перед тем, как я погружусь в объяснения,
о важности низкой связанности модулей, я должен отметить, что не всегда есть
возможность создавать модули, не имеющие абсолютно никаких зависимостей
в системе. Фактически, ваши модули могут, к примеру, расширять функции других, 
уже существующих модулей. Эта тема, скорее всего, относится к группировке
модулей на основе некоторого функционала (???). It should be possible 
for all of these distinct sets of modules to work in your application without 
depending on too many other modules being present or loaded in order to function.


### 3. Сможет ли ваше приложение работать дальше, если его отдельная часть сломается?

Если вы разрабатываете приложения, подобные Gmail, и ваш webmail-модуль (или 
группа модулей) перестанет работать из-за ошибки, то это не должно заблокировать
пользовательский интерфейс, или помешать пользователям использовать другие части
вашего приложения, к примеру, такие как чат. В то же время, как было сказано
раньше, было бы идеально, если бы модули могли работать и за пределами вашей
архитектуры. В моей лекции я упоминал динамические зависимости — возможность
загружать модули исходя из определенных действий пользователя. (???) К примеру,
ребята из Gmail могли бы изначально держать модуль чата закрытым, не загружая его
код при открытии страницы. Если же пользователь решит использовать функцию чата,
то соответствующий модуль будет динамически загружен и выполнен. В идеальном
случае, хотелось бы выполнить это без каких-то негативных эффектов в вашем
приложении.


### 4. Насколько легко вы сможете тестировать отдельные модули?

Когда вы работаете над масштабными системами, есть вероятность, что
различные части этой системы будут использовать миллионы пользователей.
Вполне вероятно, что ваши модули будут использоваться не только
в предусмотренных вами ситуациях. В конечном счете, код может использоваться
повторно в целом ряде различных окружений, и важно, чтобы модули были достаточно
протестированны. Тестировать модули неоходимо и внутри архитектуры для которой
он был изначально разработан, и снаружи. По моему мнению, это дает наибольшую
гарантию того, что модуль не сломается при попадании в другую систему.