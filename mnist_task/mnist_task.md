Task 4.4 - Классификация рукописных чисел полносвязной сетью

Полносвязная сеть из двух скрытых линейных слоев, между ними используется функция активации сигмоида.
В качестве результирующей loss-функции используется кросс-энтропия.
Количество нейронов на скрытом слое - 100, число выходных - 10, по количеству классов.

[//]: # (Image References)
[image1]: ./img/loss.png "Loss"

[//]: # (Image References)
[image2]: ./img/acc.png "Accuracy"

[//]: # (Image References)
[image3]: ./img/sgd.png "SGD"

[//]: # (Image References)
[image4]: ./img/sgd_moment.png "SGD with Momentum"

[//]: # (Image References)
[image5]: ./img/sgd_nesterov.png "Nesterov Momentum"

[//]: # (Image References)
[image6]: ./img/rprop.png "Rprop"

[//]: # (Image References)
[image7]: ./img/rmsprop.png "RMSprop"

[//]: # (Image References)
[image8]: ./img/adam.png "Adam"


1. График Loss-функции для train и validation 
Был построен график loss-функции для набора данных train и validation.

![alt text][image1]

Судя по графику, loss падает одинаково и примерно к 200 эпохе выходит на плато.
Loss на validation убывает плавно, без выбросов, так что переобучения не замечено.

2. Улучшение метрик на валидации в зависимости от количества эпох (40 -> 200) 
Построен график accuracy на validation, на котором видно, что в данном диапазоне (с 40 до 200)
эпох значение метрики растет.
![alt text][image2]

3. Время вычисления cpu/gpu
Величина batch_size -- 100.
Время вычисления 100 эпох на:
 - **GPU**: 0.0001250686707496643  (сек)
 - **CPU**: 0.00020344500136375428 (сек)
Вычисления на GPU почти в 2 раза быстрее (2х).

4. Время вычисления при torch.backends.cudnn.deterministic = True/False
Параметры используются те же, что и в предыдущем шаге.
Время вычисления при: 
*torch.backends.cudnn.deterministic* = **True**: 0.00013575996232032775,
*torch.backends.cudnn.deterministic* = **False**: 0.00013668710923194885.
Замедление работы на Tesla не наблюдается, при значении True даже немного быстрее.

5. Методы градиентного спуска (один эксперимент 3 раза на разных random seed)
Для уверенности в результатах один эксперимент проводился 3 раза на разных random seed.
Были построены графики по средним значениям accuracy для каждого метода оптимизации.
Обучение проходило на 300 эпохах. Во всех алгоритмах использовался learning rate = 1e-3, momentum = 0.9.

 - SGD

![alt text][image3]

 - SGD with Momentum 

![alt text][image4]

 - SGD Nesterov Accelerated Gradient

![alt text][image5]

 - Rprop

![alt text][image6]

 - RMSprop

![alt text][image7]

 - Adam

![alt text][image8]

Исходя из полученных графиков, наилучшее схождение имеется у алгоритмов оптимизации SGD с моментом/импульсом и Нестерова (используется то же значение для скорости обучения и момента, тч результат закономерно схож). Градиентный спуск в принципе показывает стабильность и плавный выход на плато. При этом у алгоритма Adam быстрее достигается значение метрики, превышающее 0.91.
