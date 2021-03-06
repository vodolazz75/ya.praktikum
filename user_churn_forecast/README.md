# Прогноз вероятности оттока пользователей для фитнес-центра   

Сеть фитнес-центров «Культурист-датасаентист» разрабатывает стратегию взаимодействия с пользователями на основе аналитических данных.Чтобы бороться с оттоком, отдел по работе с клиентами «Культуриста-датасаентиста» перевёл в электронный вид множество анкет пользователей. Наша задача — провести анализ и подготовить план действий по удержанию клиентов.   
А именно:      
 - научиться прогнозировать вероятность оттока (на уровне следующего месяца) для каждого клиента     
 - сформировать типичные портреты пользователей: выделить несколько наиболее ярких групп и охарактеризовать их основные свойства     
 - проанализировать основные признаки, наиболее сильно влияющие на отток     
 - сформулировать основные выводы и разработать рекомендации по повышению качества работы с клиентами:     
     - выделить целевые группы клиентов     
     - предложить меры по снижению оттока      
     - определить другие особенности взаимодействия с клиентами    
    
Сеть фитнес-центров «Культурист-датасаентист» разрабатывает стратегию взаимодействия с пользователями на основе аналитических данных.Чтобы бороться с оттоком, отдел по работе с клиентами «Культуриста-датасаентиста» перевёл в электронный вид множество анкет пользователей. Перед нами стояла задача — провести анализ и подготовить план действий по удержанию клиентов.      

В данных 4000 записей, пропуски и категориальные переменные отсутствуют. Названия столбцов были приведены к единому регистру. В текущем месяце в отток попал 1061 клиент. Более 26% посетителей фитнес-центра перестали пользоваться его услугами. Если не улучшить стратегию поведения в будущем, через месяц фитнес-центр потеряет уже более половины клиентов, обслуживающихся на данный момент.     

Суммарная выручка от сопутствующих услуг фитнес-центра на одного клиента в среднем составляет 147 рублей, медианное значение 136 рублей. Максимальный показатель суммарной выручки 553 рубля. Если посмотреть на суммарную выручку с разбивкой клиентов на группы - тех, кто ушел и тех, кто остался, видно, что ушли более прижимистые пользователи. В среднем выручка фитнес-центра от оставшегося клиента составляет 158 рублей против 115 рублей от ушедшего. Оставшиеся пользователи могут потратить максимально 553 рубля против 425 рублей тех, кто больше не вернется.      
Средняя частота посещений фитнес-центра одним посетителем за весь период действия абонемента составляет 1,8 раз в неделю. Самые увлеченные посетители занимаются спортом 6 раз в неделю. Тот же показатель частоты посещений фитнес-центра, но только за прошлый месяц, чуть меньше - 1,7 раз в неделю. А максимальное значение посещений, наоборот, чуть выше - 6,1 раз в неделю.      
Разница в средней частоте посещения фитнес-центра между теми, кто остался и теми, кто ушел в отток, очевидна: 2 раза в неделю против 1,5 раз в неделю за весь период действия абонемента и 2 раза в неделю против 1 раза в неделю за прошлый месяц. Но более убедительная разница у показателей максимального количества посещений: 6 раз в неделю у оставшихся любителей спорта против 3,5 раз в неделю у ушедших.      

Большинство посетителей живут или работают рядом с фитнес-центром и у них есть телефон. По всем бинарным признакам отток составляет существенную часть от оставшихся клиентов. Удаленность от фитнес-центра негативно влияет на желание посетителей туда ходить.      
Чем длительнее период действия абонемента - тем меньше отток посетителей. Клиенты, у которых годовой абонемент, ценят свои финансовые вложения и регулярно ходят в фитнес-центр. С приближением срока окончания абонемента, посетители перестают экономить и большинство из них бросает занятия спортом.       
Почти стороцентная корреляция наблюдается у признаков-близнецов: `month_to_end_contract` - `contract_period`, и `avg_class_frequency_current_month` - `avg_class_frequency_total`. Большинство признаков никак не связано между собой. На отток посетителей влияют длительность абонемента, возраст, время с его первого обращения и число посещений фитнес-центра в неделю: чем ниже эти показатели, тем выше отток.      

Мы построили модель прогнозирования оттока посетителей и обучили ее двумя способами: логистической регрессией и случайным лесом. Для обеих моделей на валидационной выборке были рассчитаны метрики `Accuracy`, `Precision` и `Recall`.   
Метрики для модели логистической регрессии:   
  - Accuracy: 0.90   
  - Precision: 0.83   
  - Recall: 0.80       

Обе модели показали высокую точность предсказаний. Однако модель логистической регресии дает чуть более точные значения по всем метрикам по сравнению с моделью случайного леса, поскольку для прогнозирования данных небольшого размера подходит наиболее точно.      
  
На дендрограмме матрице расстояний было предложено оптимальное число кластеров - 4 кластера. Для обучения модели кластеризации на основании алгоритма K-Means было взято число кластеров n= 5: от кластера 0 до кластера 4.      
В кластере 1, с самым высоким средним значением длительности абонемента 8 месяцев, самый низкий показатель оттока пользователей - 11%. Кластер 1 - самый надежный кластер. Это объясняется тем, что здесь собрались более взрослые клиенты фитнес-центра с наиболее длительным сроком абонемента, то есть, с наибольшими инвестициями. Поэтому логично, что никто не разбрасывается финансами и не перестает ходить в зал. Кластер 2, который объединяет самых активных пользователей фитнес-центра, тоже довольно надежный кластер - доля оттока 22%. А кластеры 0 и 4, с самыми высокими показателями оттока пользователей 38% и 40%, наоборот отличаются более молодыми пользователями с наименьшими показателями длительности абонемента - 3 месяца.     

Средние показатели распределения по полу и возрасту посетителей среди кластеров примерно одинаковые.      
Кластеры 0 и 4 с наиболее молодыми пользователями характеризуется самой короткой длительностью абонемента и самым коротким сроком принятия решений `lifetime`. Как оказалось, молодежь быстрее всех принимает решения, в т.ч. и о записи в фитнес-центр, правда потом с той же скоростью меняет их. Кластеры 1 и 2 объединяют пользователей, которые ходят в фитнес-центр чаще остальных - в среднем 2 раза в неделю.      

В результате проведенного анализа обнаружены основные признаки, наиболее сильно влияющие на отток:   
  - удаленность проживания или места работы пользователя от фитнес-центра   
  - длительность приобретаемого пользователем абонемента    
  - наличие у него телефона       
  - является ли пользователь сотрудником компании-партнера клуба    
  - скорость принятия решения о покупке абонемента.   

Для повышения качества работы с клиентами сети фитнес-центров "Культурист-датасаетнист" можно рекомендовать:   
  - оптимизировать линейку предлагаемых абонементов по длительности: отказаться от абонементов с коротким сроком действия   
  - сосредоточиться на пользователях, проживающих или работающих вблизи фитнес-центров   
  - разработать систему бонусов для потенциальных клиентов старше 30 лет   
  - разработать программу лояльности для действующих пользователей, кто посещает фитнес центр два и более раза в неделю.   
