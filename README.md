# Questions
###1.Какие компоненты андроид системы вы знаете?
Основные компоненты андроид системы которые должны быть зарегестрированы в файле AndroidManifest:
Activity
Servicy
BroadcastReceivers
ContentProviders
###2.Какой из этих компонентов не обязательно регистрировать в файлу AndroidManifest и почему?
В системе Android необязательным компонентом для регистрации в манифесте является Service. В отличии от Activity и BroadcastReceivers, Servicy могут быть запущены и работать в фоновом режиме без непосредственного взаимодействия с пользователем. 
###3.Что такое Activity?
Это компонент приложения, который представляет собой экран, с которым пользователи могут взаимодействовать для выполнения каких-либо действий, например набрать номер телефона, сделать фото, отправить письмо или просмотреть карту. Каждой Activity присваивается окно для прорисовки соответствующего пользовательского интерфейса.
###4.Опишите жизненный цикл Activity
<h3 align="center"><strong>Welcom Fragment</strong></h3>
<p align="center">
  <img src="https://www.sysbunny.com/blog/wp-content/uploads/2021/04/Android-Activity-Lifecycle-768x917.jpg)https://www.sysbunny.com/blog/wp-content/uploads/2021/04/Android-Activity-Lifecycle-768x917.jpg" alt="Preview"/>
</p>
