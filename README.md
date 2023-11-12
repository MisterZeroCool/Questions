# <img src="https://www.gifki.org/data/media/1476/znak-voprosa-animatsionnaya-kartinka-0015.gif" alt="Preview"/> Questions <img src="https://www.gifki.org/data/media/1476/znak-voprosa-animatsionnaya-kartinka-0015.gif" width="30px"> <img src="https://www.gifki.org/data/media/1476/znak-voprosa-animatsionnaya-kartinka-0015.gif" alt="Preview"/>

  <img src="https://www.gifki.org/data/media/1476/znak-voprosa-animatsionnaya-kartinka-0015.gif" alt="Preview"/>

- [Android](#android)
- [Android components](#android-components)
  - [Activity](#activity)
  - [Fragments](#fragments)
  - [Content provider](#content-provider)
  - [Services](#services)
  - [Broadcasts](#broadcasts)
  - [Custom Views](#custom-views)
  - [ViewModel](#viewmodel)
  
# Android<img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExbnluOG4xdGlpeWxwYnFhM3Bjc2Z3dzN5eDhhaThza2N0Ym9wOGUxOCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/zECASgodRMZ5QAbRao/giphy.gif" width="30px">

### Какие компоненты андроид системы вы знаете?
Основные компоненты андроид системы которые должны быть зарегестрированы в файле AndroidManifest:
+ `Activity`
+ `Servicy`
+ `BroadcastReceivers`
+ `ContentProviders`

### Какой из этих компонентов не обязательно регистрировать в файле AndroidManifest и почему?
В системе Android необязательным компонентом для регистрации в манифесте является Service. В отличии от Activity и BroadcastReceivers, Servicy могут быть запущены и работать в фоновом режиме без непосредственного взаимодействия с пользователем. 

### Расскажите про AndroidManifest и для чего он нужен?
Это Xml инструкция которая выполняется до запуска приложения и описывает его основную инфрмацию для системы. Каждое приложение имеет свой файл AndroidManifest.xml который находится в папке проекта manifest. В нем определяется название приложения, api андроида необходимое для работы приложения, методанные о версии, иконке, теме и т.д. Перечисляются общедоступные библиртеки которые связаны с приложением, например Google карты. Объявляются основные компоненты приложения. Например в елементе application мы можем объявлять MainActivity которая будет точкой доступа в приложении и откроется при его запуске, для этого необходимо указать в 
```java
<activity android:name=".presentation.MainActivity">
  <intent-filter>
    <action android:name="android.intent.action.MAIN" />
    <category android:name="android.intent.category.LAUNCHER" />
  </intent-filter>
</activity>
```
В манифесте можно указать разрешения, которые должны запросить други приложени для взаимодействия с нашим приложением. И список permission которые будут запрошены у системы для функционирования приложения, например доступ к интернету, камере, локации, контактам и т.д.

# Android Components<img src="https://media.giphy.com/media/v1.Y2lkPTc5MGI3NjExbnluOG4xdGlpeWxwYnFhM3Bjc2Z3dzN5eDhhaThza2N0Ym9wOGUxOCZlcD12MV9pbnRlcm5hbF9naWZfYnlfaWQmY3Q9Zw/zECASgodRMZ5QAbRao/giphy.gif" width="30px">

## Activity
### 1.Что такое Activity?
Это компонент приложения, который представляет собой экран, с которым пользователи могут взаимодействовать для выполнения каких-либо действий, например набрать номер телефона, сделать фото, отправить письмо или просмотреть карту. Каждой Activity присваивается окно для прорисовки соответствующего пользовательского интерфейса.

 ### 2.Как стартует первая Activity?
 Все начинается с лаунчера. Лаунчер — первое приложение, которое запускается системой. Он отличается от обычного приложения тремя вещами:

1️⃣ Главной Activity лаунчера устанавливается категория HOME, благодаря чему система будет вызывать эту Activity при нажатии на кнопку Home.
```xml
<category android:name="android.intent.category.HOME" />
```


2️⃣ Всем Activity лаунчера нужно выставить флаг excludeFromRecents, чтобы они не мелькали в recents.
```xml
<activity
   android:name=".MainActivity"
   android:excludeFromRecents="true"
```

3️⃣ Activity лаунчера пользователь будет видеть чаще всего. То, что приложением будут пользоваться чаще всего, — сказка для эффективных менеджеров. Но цена такого успеха — когда крашится обычное приложение, пользователи пугаются и удаляют лаунчер.


### 3.Как можно переключаться между Activity?
<b>Первый способ с помощью `Intent`-ов.</b>
<p>Для запуска нового экрана необходимо создать экземпляр класса Intent и указать в первом параметре текущий класс, а во втором - класс для перехода, у нас это AboutActivity. После этого вызывается метод startActivity(), который и запускает новый экран.</p>

```java
button.setOnClickListener {
    val intent = Intent(this@MainActivity, AboutActivity::class.java)
    startActivity(intent)
}
```
<b>Второй способ с помощью `putExtra()`.</b>

Иногда требуется не только вызвать новый экран, но и передать в него данные.В этом случае нужно задействовать специальную область `extraData`, который имеется у класса `Intent`. 

Область `extraData` - это список пар ключ/значение, который передаётся вместе с intent-ом. В качестве ключей используются 
String, а для значений можно использовать любые примитивные типы данных, массивы примитивов, объекты класса Bundle, объекты которые реализуют интерфейсы Serializable и Parcelable.

Для передачи данных в другую активность используется метод `putExtra()`

Принимающая активность должна вызвать какой-нибудь подходящий метод: `getIntExtra()`, `getStringExtra()` и т.д.:

### 4.Опишите жизненный цикл Activity.
Жизненный цикл представляет собой последовательность методов, которые вызываются в определенной последовательности во время создания/уничтожения/приостановки Activity.

<h3 align="center"><strong>Activity Lifecucler</strong></h3>
<p align="center">
  <img src="https://www.sysbunny.com/blog/wp-content/uploads/2021/04/Android-Activity-Lifecycle-768x917.jpg" alt="Preview"">
</p>

+ `onCreate()`
Необходимо обязательно реализовать, поскольку система вызывает его при создании Activity. Важно именно здесь вызвать метод `setContentView()` для определения пользовательского интерфейса. Вызывается первым, во время создания Activity. Вызывается один раз, после чего наше Activity переходит в состояние <b>Created</b>. В данном методе мы инициализируем интерфейс нашего Activity, а также выполняем некоторую базовую логику, которая необходима нам для корректной работы Activity, например, создаём список с какими-либо данными. Также, в качестве аргумента метода `onCreate()` нам передаётся объект <b>Bundle</b>, который содержит в себе информацию, которая была предварительно сохранена, во время пересоздания <b>Activity</b>.

+ `onStart()`
Переводит нашу Activity в состояние <b>Started</b>, после чего Activity становится видно для пользователя. Метод может использоваться для какой-либо логики, которая взаимодействует с UI.

+ `onResume()`
Наше Activity переходит на передний план приложения (foreground) изменяя своё состояние на Resumed. После вызова данного метода, пользователь может взаимодействовать с Activity. В данном состоянии Activity остается до тех пор, пока не потеряет фокус, это может произойти, например, при переходе на другую Activity, либо при входящем телефонном звонке.

+ ` onPause()`
Наше Activity теряет фокус, больше не видно для пользователя и выходит из состояния foreground. При этом Activity не уничтожается и продолжает существовать. В этом методе, например, мы можем приостановить логику связанную с GPS навигацией, чтобы минимизировать расход <b>батареи</b>.

+ `onStop()`
Состояние <b>Activity</b> изменяется на Stopped. Вызывается, когда Activity не видно пользователю, например, при переходе на другой экран или при сворачивании приложения, а также при подготовке к полному уничтожению нашей <b>Activity</b>. системой.

+ `onDestroy()`
Метод вызывается непосредственно перед уничтожением нашей <b>Activity</b>, например, после вызова метода `finish()`, или переходе на предыдущую <b>Activity</b>, путём нажатия кнопки “назад”.
Если активность завершается, `onDestroy()` – это последний метод жизненного цикла, который вызывает <b>Activity</b>. Если `onDestroy()` вызывается в результате изменения конфигурации, система немедленно создает новый экземпляр активности вызывает `onCreate()` в новом экземпляре и новой конфигурации.
Метод `onDestroy()` должен освобождать все ресурсы нашей Activity.


### 5.Что происходит при перевороте экрана Activity? Какие методы вызываются? Как сохранить данные при перевороте?
При повороте экрана система уничтожает и полностью пересоздаёт экземпляр <b>Activity</b>. 

Вызываются коллбэки:  
+ ` onPause()`, `onStop()`, `onSaveInstanceState()`, `onDestroy()`

+ `onCreate()`, `onStart()`, `onRestoreInstanceState()`,  `onResume()`.




Для того, что сохранить какие-либо пользовательские данные и затем восстановить их в нашей <b>Activity</b>, используются следующие методы:

+ `onSaveInstanceState()`
Данный метод вызывается перед тем, как <b>Activity</b> будет уничтожена. Параметром метода является Bundle, в который мы будем складывать необходимые для сохранения данные. Рекомендуется сохранять данным способом информацию, объём которой не превышает 1 мегабайт, в случае превышения лимита мы получим ошибку <b>TransactionTooLargeException</b>.
+ `onRestoreInstanceState()`
Вызывается после метода `onStart()`. В данный метод мы получим наш <b>Bundle</b>, в котором была сохранена информация.

Стоит заметить, что Bundle с сохранёнными данными мы также получаем в методе `onCreate()`, но данную ситуацию нужно отдельно обрабатывать, чтобы не получить <b>NullPointerException</b>.

### 6.Как при пересоздании активити сохранить некоторый объект (кроме onSaveInstanceState)?

  - Методы [onRetainCustomNonConfigurationInstance()](https://developer.android.com/reference/android/support/v4/app/FragmentActivity.html#onretaincustomnonconfigurationinstance) и 
[getLastCustomNonConfigurationInstance()](https://developer.android.com/reference/android/support/v4/app/FragmentActivity.html#getlastcustomnonconfigurationinstance) класса FragmentActivity (или AppCompatActivity)?
- Если активити — просто держатель для фрагментов, лучше в самих фрагментах делать `setRetainInstance(true)` 


### 7.Как получить результат от другой Activity?
Нужно вызвать метод `startActivityForResult()`.

### 8.Какие методы вызываются при переходе между активити?
  - A: `onCreate()`, `onStart()`, `onResume`
    A: *(переход)* onPause
    B: `onCreate()`, `onStart()`, `onResume`
    A: onStop
    B: *(обратный переход)* onPause
    A: `onRestart`, `onStart()`, `onResume`
    B: onStop, onDestroy
   ![иллюстрация процесса](https://lh5.googleusercontent.com/-MMX3o4pdsd0/ToybUtq-EFI/AAAAAAAAAbw/ri5MQ1Jg5sI/s800/20111005_L0024_L_TwoActSchema.jpg) 

### 9.Когда `onDestroy()` вызывается без `onPause()` и `onStop()`?
  - Если активити закрывается через метод `finish()` до начала `onStart()` и `onResume`.
  
  ### 10.Почему `setContentView()` располагают в `onCreate()`?
  - Это тяжёлая операция, и выгоднее производить её только единожды, при создании активити.
  - 
  ### 11.Как очистить бэкстек при создании активити?
  - Использовать флаг `FLAG_ACTIVITY_CLEAR_TOP`. 
  - Использовать `FLAG_ACTIVITY_CLEAR_TASK` и `FLAG_ACTIVITY_NEW_TASK` вместе.
  - 
  ### 12.Разница между `FLAG_ACTIVITY_CLEAR_TASK` и `FLAG_ACTIVITY_CLEAR_TOP`?
  - Первый очистит всё, что есть в таске, второй — только до той же активити, что и запускаемая.
  
  ### 13.Launch modes
  - **Standard** При вызове, активити создаётся заново.
  - **SingleTop** Активити создаётся заново, только если она не вверху активити-стека. 
  - **SingleTask** Стек стирается до момента, пока эта активити не окажется наверху стека.
  - **SingleInstance** Похож на SingleTask, но при создании активити, она уйдёт в новый таск.
  
  ### 14.Когда Activity удаляется из памяти?
  1. Использование метода finish(): этот метод завершает текущую Activity и освобождает память, занимаемую ею. При вызове метода finish() пользователь будет перенаправлен к предыдущей активности в стеке, и текущая Activity будет полностью удалена из памяти.
  2. Использование метода onBackPressed(): этот метод вызывается при нажатии пользователем кнопки «Back». По умолчанию этот метод закрывает текущую Activity и освобождает память, занимаемую ею.
  3. Использование флага Intent.FLAG_ACTIVITY_CLEAR_TOP: этот флаг используется при создании Intent, чтобы удалить все Activity, которые находятся выше в стеке запущенных активностей, и перейти к указанной Activity. Это полезно, когда мы хотим удалить все промежуточные Activity, чтобы вернуться к определенному экрану.
   
   Важно отметить, что Android система автоматически уничтожает Activity, которые не используются и занимают слишком много памяти. Однако в некоторых случаях может быть полезно явно удалить Activity из ОЗУ вручную с помощью вышеуказанных методов.
