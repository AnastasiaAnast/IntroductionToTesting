# Техники тест-дизайна

Разработка тест-кейсов один из важных этапов в жизненном цикле тестирования. Создавать наиболее эффективные тест-кейсы позволяют техники тест-дизайна. Непосредственно тестирование на этапе теск-дизайне НЕ выполняется.

1. Что такое тест-дизайн.
2. Цели тест-дизайна.
3. Техники тест-дизайна.

Процесс тестирования начинается с проверки и анализа требований: насколько они полные, четкие, тестируемые. Приоритезируем требования. Далее - этап написания тест-кейсов, это и есть тест дизайн.

**Тест-дизайн** — **этап тестирования ПО, где проектируются и создаются тестовые случаи (тест-кейсы)** в соответствии с определенными ранее критериями качества, целями тестирования.
Нужны, чтобы формировать конечный набор тест-кейсов, без проверки всего подряд.

## Цели тест-дизайна

1. максимально покрыть функциональность тестами (создать тестовое покрытие _без слепых зон_ - без проверок);
2. обнаружить самые серьезные баги;
3. сократить кол-во тестов исключая непродуктивные тест-кейсы;
4. не пропустить важные тесты.

## Техники тест-дизайна

Позволяют выпонить тестирование наиболее эффективно, не проверяя лишние кейсы и завершить тестирование в установленные сроки. _Главное - выявить критичные дефекты, тк невозможно выявить абсолютно все баги_.

- классы эквивалентности (эквивалентное разделение);
- граничные значения (анализ граничных значений, метод граничных значений);
- попарное тестирование (тестовая комбинаторика);
- тестирование состояний и переходов;
- таблицы принятия решений;
- исследовательское тестирование.

**Класс эквивалентности** — _входные (иногда - выходные) данные, обрабатываемые одинаковым образом, приводящие к одному результату_. Выбираем значение из группы значений и делаем вывод о том, что все остальные значения из этой группы будут такие же. Повышает эффективность и скорость тестов.

кнопки не попадают в класс эквивалентности
поля для заполнения - попадают в класс эквивалентности

**Эквивалентное разбиение (equivalence partitioning)** - второе название этого процесса.

Тестирование на основе классов эквивалентности — техника тест-дизайна на основе **метода черного ящика** - у тестировщика нет _никакого_ доступа к коду. Помогает разрабатывать, выполнять меньше тест-кейсов, сохраняя достаточное тестовое покрытие.

Признаки эквивалентных классов:

- если один тест выявит ошибку — остальные, скорее всего, тоже это сделают;
- если один из тестов не выявит ошибку — остальные, скорее всего, тоже этого не сделают.

Классы эквивалентности. Пример
0–15 Не нанимать
16–17 Наем, только сокращенный рабочий день (part time)
18–64 Наем на полный рабочий день (full time)
65–99 Не нанимать

        If (applicantAge >= 0 && applicantAge <16)
        hireStatus="NO";
        If (applicantAge >= 16 && applicantAge <18)
        hireStatus="PART";
        If (applicantAge >= 18 && applicantAge <65)
        hireStatus="FULL";
        If (applicantAge >= 65 && applicantAge <=99)
        hireStatus="NO";

Что можно разбить на классы эквивалентности:

1. числа;
2. символы;
3. длину строки;
4. размер файла;
5. объем памяти;
6. разрешение экрана;
7. версии операционных систем, библиотек;
8. объем передаваемых данных.

Исчерпывающее тестирование - проверка всех возможных вариантов

При проверках лучше выбирать _серединные_ значения, не крайние

**Линейные** (есть диапазон валидных значений, есть значения слева и справа от диапазона - они невалидны) и нелинейные/неупорядоченные (нельзя упорядочить, _разложить на числовой прямой или как-то последовательно_; есть только валидные и невалидные значения, расположены в отношении друг друга хаотично) классы эквавалентности.

По каким признакам можно отличить линейные/упорядоченные от нелинейных/неупорядоченных: (тайминг16-11)

## Анализ граничных значений

Проверка поведения продукта на крайних/граничных значениях входных данных - чаще всего обнаруживаются ошибки. **Для линейных значений**.

Алгоритм анализа граничных значений:

1. Выделить классы эквивалентности.
2. Определить граничные значения этих классов.
3. Определить, к какому классу будет относиться каждая граница.
4. Для каждой границы провести тесты по проверке значения до границы, на ней и сразу после нее.

Граничные значения:

0–15 Не нанимать
16–17 Наем, только сокращенный рабочий день (part time)
18–64 Наем на полный рабочий день (full time)
65–99 Не нанимать

        If (applicantAge >= 0 && applicantAge <16)
        hireStatus="NO";
        If (applicantAge >= 16 && applicantAge <18)
        hireStatus="PART";
        If (applicantAge >= 18 && applicantAge <55)
        hireStatus="FULL";
        If (applicantAge >= 55 && applicantAge <=99)
        hireStatus="NO";

        {-1, 0, 1}, {15, 16, 17}, {17, 18,
        19}, {64, 65, 66}, и {98, 99, 100}
        { -36, 1001, FRED, %$#@}

- Определим границы классов эквивалентности: 1й класс эквавалентности: 0-15, 2й класс: 16-17, 3й класс: 18-64, 4й класс: 65-99.
- Определим к какому классу эквивалентности относится каждая из границ: 1й класс эквавалентности: 0, 2й - 16, 3й: 18, 4й: 65.
- Для каждой границы выделим 3 значения - 2 околограничные, 1 - граница. Для границы 0 околограничные: -1, и 1, для 16: 15 и 17, для 18: 17 и 19, для 65: 64 и 66.
- Исключить дубликаты и добавить негативные проверки (отрицательные, большие значения, спецсимволы, кириллица, латиница)

## Нелинейные классы эквивалентности: техники:

## Попарное тестирование (pairwise testing) - Pairwise

Техника формирования наборов тестовых данных, где каждое тестируемое значение каждого из проверяемых параметров хотя бы раз сочетается с каждым из тестируемых значений всех остальных проверяемых параметров.
**Проверяются НЕлинейные значения**.

Применяется на проектах при тестировании функциональности, в которых много различных параметров и их значений. Пример: фильтры в магазине/соц сети и проч.

Суть проблемы:
Если мы попытаемся проверить все сочетания всех значений всех параметров для сложного случая тестирования, мы получим количество тест-кейсов, превышающее все разумные пределы.

_Большинство дефектов возникает при комбинации двух параметров._

**Чекбокс** - эл-т, имеющий 2 состояния: вкл и выкл.

Полный перебор:
1 чекбокс = 2 значения ON|OFF
2 чекбокса = 4
3 чекбокса = 8
4 чекбокса = 16
5 чекбоксов = 32
10 чекбоксов = 1024
15 чекбоксов = 32 768
20 чекбоксов = 1 048 576

Результат использования **Pairwise** – 10 тестов вместо 1 048 576

Важно при применении Pairwise:

- хорошо масштабируется при увеличении _параметров_
- плохо масштабируется при увеличении количества _значений_. Здесь удобнее разделить значения на 2 класса: _валидный класс_ - все корректные знач-я; _НЕвалидный класс_ - все НЕкорректные знач-я;

Программы для Pairwise

- Pairwise Online Tool
- PICT
- Allpairs
- VPTag

## Тестирование на основе состояний и переходов (State-Transition Testing)

Фиксируют требований, описывают дизайн приложения, помогают выбрать необходимые для проверки кейсы. Описываются конкретные состояния приложения и как они могут меняться.

**Точка входа** — черная точка на диаграмме.
**Переход (transition) (стрелка)** — переход из одного состояния приложения в другое, происходящий по событию.
**Состояние (state) (круг)** — состояние приложения, в котором оно ожидает одного или нескольких событий.
**Событие (event) (надпись над стрелкой)** — то, что сделал пользователь/импульс извне.
**Действие (action)** — реакция приложения на событие.
**Точка выхода** — показана на диаграмме как мишень.
**Условия перехода (transition conditions)** — условия, в соответствии с которыми система будет выполнять то или иное действие.
**Роли пользователей (actors)** - влияющих на систему в зависимости от прав доступа/обстоятельств.

**Плюсы** диаграмм состояний и переходов:

- позволяют визуализировать состояния продукта;
- демонстрируют варианты переходов, которые можно пропустить;
- помогают отследить дефект, сужая его локацию до конкретного перехода;
- показывают внутреннюю механику продукта.

**Минусы** диаграмм состояний и переходов:

- можно пропустить неочевидные переходы;
- при слишком сложной структуре продукта диаграммы могут стать громоздкими, запутанными;
- являются только основой к применению других методов;
- бесполезны при плохом знании продукта.

## Таблицы принятия решений (decision table)

Техника тестирования **черного ящика**, применяется для систем со сложной логикой. Помогает быстрее разобраться в бизнес-логике приложения, упорядочить ее, протестировать все возможные комбинации условий.

Сущности, из которых состоят таблицы:
**Условия (conditions)** — короткое описание входных условий/данных в виде вопроса.
**Действия (actions)** — четкое описание ожидаемого результата, действия системы.
**Значения (values)** — значения, допустимые для входных данных, указанных в условии.
**Правила (rules)** — комбинации входных данных, отраженых в таблице.

Цель применения:

- упорядочить, задокументировать сложную логику приложения;
- протестировать все комбинации условий и состояний.

Пример. Рассылка писем
Требование: для поддержания системы лояльности провести информационную рассылку постоянным клиентам.
Содержание писем зависит от следующих условий:

- Клиенты типа А, В получают стандартное письмо.
- Клиенты типа С получают специальное письмо.
- Клиентам, совершившим пять и более покупок или купившим на сумму более 500 долларов, в письме сообщается о дополнительной скидке 20% на следующий заказ.

План действий:

1. Разбить требование на условия.
2. Посчитать количество возможных правил (комбинаций).
3. Составить таблицу принятия решений.
4. Исключить лишние комбинации, если они есть.
5. Создать тесты.

Количество возможных комбинаций:
X = Y1*Y2*...Yn, где Х — вычисляемое количество комбинаций;
Y1...Yn — количество вариантов каждого условия;
N — количество условий.

- Y1 = 4 (четыре значения для условия «Тип клиента» — «A, B, C, D»);
- Y2 = 2 и Y3 = 2 (по два значения для условий «Пять и более покупок» и «Сумма больше 500 долларов» — «YES/NO»);
- N = 3 (требование содержит три условия);
- X = 4*2*2;
- Х = 16 правил (комбинаций условий).

D – все остальные типы клиентов (если существуют).
? – не описано в требованиях (если более пяти покупок + сумма
больше 500 долларов, а также как поступить с клиентами D).

**Плюсы** таблиц принятия решений:

- помогают быстро составлять тестовые сценарии;
- позволяют выявить неполноту требований;
- их можно использовать при отсутствии требований;
- можно быстро проверить покрытие требований тест-кейсами;
- позволяют предугадывать возможные ошибки.

**Минусы** таблиц принятия решений:
– при большом количестве условий таблицы могут быть громоздкими — их сложно составлять, использовать;
– сложность в корректном определении условий, действий и значений при первоначальном проектировании.

## Исследовательское тестирование (exploratory testing)

Неформальный метод проектирования тестов, при котором _тестировщик НЕ использует тест-кейсы, а тестирует приложение по сценарию, который часто создается прямо во время проверки_.
Полученный сценарий - тест, выявивший дефекты - документируется - на него составляется тест-кейс.
Используется если тест-кейсы отсутствуют и для проверки похожих сценариев.
Вспомогательный подход к тестированию по тест-кейсам. Помогает исключить "эффект пестицида"(ТК не выявляют новых дефектов).

Эффективное применение исследовательского тестирования:

- быстрая обратная связь о качестве новой функциональности;
- быстрое изучение тестируемого продукта;
- контроль работы других тестировщиков;
- недостаток времени для составления тестовых сценариев;
- отсутствие требований;
- небольшой проект, для которого не требуется структурированный подход к тестированию;
- внезапные изменения в проекте;
- дополнительные проверки.

**Плюсы** исследовательского тестирования:

- не нужно тратить время на предварительное описание всех сценариев;
- не нужна поддержка тестовых сценариев;
- не происходит привыкание к тестовым сценариям, и их прохождение не происходит «не глядя»;
- не теряется цельное видение продукта;
- критические дефекты находятся быстрее;
- повышается скорость тестирования;
- можно сразу начинать тестировать продукт, даже если требований нет вообще;
- исследовательское тестирование интереснее и креативнее (тесты ограничиваются только фантазией и глубиной знаний о продукте).

**Минусы** исследовательского тестирования:

- сложно планировать время на проведение тестирования без задокументированных заранее сценариев;
- вероятность пропустить ключевые проверки, так как отсутствует ранжирование сценариев по степени важности;
- сложность оценки полноты покрытия требований тестами;
- требуется высокая квалификация тестировщиков и хорошее знание тестируемого приложения;
- сложно использовать для регрессионного тестирования;
- невозможно автоматизировать такое тестирование.

Дополнительные материалы:

1. Тест-дизайн. Что это такое? Тест дизайн в тестировании ПО. Test design [https://www.youtube.com/watch?v=x8QI3vNxg-8&ab_channel=BogdanOvsiyuk]
2. Процесс тестирования. Часть 2: Анализ тестирования и тест дизайн [https://crashtest.by/test-analysis-and-test-design/]
3. Кто такие тест-дизайнеры и зачем они нужны [https://quality-lab.ru/blog/roles-and-responsibilities-of-test-designer/]
