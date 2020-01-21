Task 6.3 - Классификация рукописных чисел на датасете CIFAR

Исследование работы сети ResNet и сравнение ее с самописной сетью CIFARNet, в которой используюется Batch нормализация, функции активации Relu и гиперболического тангенса, а также слои MaxPooling.

[//]: # (Image References)
[image1]: ./img/acc_100.png "Accuracy"

[//]: # (Image References)
[image2]: ./img/loss_100.png "Loss"

[//]: # (Image References)
[image3]: ./img/acc20_50.png "Acc resnet20"

[//]: # (Image References)
[image4]: ./img/loss20_50.png "Loss resnet20"

[//]: # (Image References)
[image5]: ./img/acc_drop.png "Acc resnet20 drop"

[//]: # (Image References)
[image6]: ./img/loss_drop.png "Loss resnet20 drop"

[//]: # (Image References)
[image7]: ./img/acc_drop_p.png "Acc drop cmp p"

[//]: # (Image References)
[image8]: ./img/loss_drop_p.png "Loss drop cmp p"

[//]: # (Image References)
[image9]: ./img/acc_wd.png "Acc l2"

[//]: # (Image References)
[image10]: ./img/loss_wd.png "Loss l2"


1. Сравните результаты resnet18 и CIFARNet. Какая сеть дает лучший результат?
 
Были построены графики accuarcy и loss-функции на валидации (100 эпох).

![alt text][image1]

![alt text][image2]

resnet18 дает лучший результат по точности и меньше переобучается по сравнению с CIFARNet.

2. Попробуйте, пользуясь нашей лекцией и описанием архитектуры из оригинальной статьи, написать собственную реализацию ResNet20. Удалось ли побить resnet18? 

Реализация [ResNet20](./mod1_plot.ipynb).
Построен график accuracy и loss-функции на валидации (50 эпох).

![alt text][image3]

![alt text][image4]

Точность на валидационном датасете resnet20 выше, чем у resnet18. Переобучение также меньше.

3. Реализуйте ResNet110 (возможно, придется уменьшить размер batch'a). Проверьте утверждение, что ResNet110 не обучается (или обучается в 10% случаев), если отключить BatchNorm.
# TODO

4. Добавьте Dropout2d после каждого BatchNorm2d для ResNet20. Есть ли положительный эффект? Как параметр "p" этого слоя влияет на accuracy и на переобучение?

![alt text][image5]

![alt text][image6]

Точность не стала выше, даже несколько уменьшилась, однако уровень переобучения снизился, *p=0.5*.

Сравнение с разными значениями параметра *p*: 0.2, 0.5, 0.7. 

![alt text][image7]

![alt text][image8]

Параметр *p* влияет на величину accuracy - чем он выше, тем ниже точность, а переобучение, наоборот, снижается.

5. Добавьте L2-регуляризацию. В PyTorch она активируется с помощью параметра weight_decay в оптимизаторе. Значение обычно выбирают из [1e-3, 1e-4, 1e-5]. Значение 1e-2 ставить не стоит, т.к. сеть не сможет учиться,  а 1e-6 скорее всего просто не повлияет на обучение (но лучше это проверить это утверждение самостоятельно). 

![alt text][image9]

![alt text][image10]

Чем меньше значение *weight decay*, тем выше точность, при этом может расти и переобучение. В случае с weight_decay=1e-2 примерно после 40 эпохи величина loss выходит на плато и сеть перестает обучаться.
