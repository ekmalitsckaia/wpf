**Привязка**

**Введение в привязку данных**
____________________________________
В WPF привязка (binding) является мощным инструментом программирования, без которого не обходится ни одно серьезное приложение.
Привязка подразумевает взаимодействие двух объектов: источника и приемника. Объект-приемник создает привязку к определенному свойству объекта-источника. В случае модификации объекта-источника, объект-приемник также будет модифицирован. Например, простейшая форма с использованием привязки:
________________________________________
``` C#
<Window x:Class="BindingApp.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:BindingApp"
        mc:Ignorable="d"
        Title="MainWindow" Height="250" Width="300">
    <StackPanel>
        <TextBox x:Name="myTextBox" Height="30" />
        <TextBlock x:Name="myTextBlock" Text="{Binding ElementName=myTextBox,Path=Text}" Height="30" />
    </StackPanel>
</Window>
```
![sdad](https://metanit.com/sharp/wpf/pics/11.1.png)

Для определения привязки используется выражение типа:
``` C#
{Binding ElementName=Имя_объекта-источника, Path=Свойство_объекта-источника}
```
То есть в данном случае у нас элемент TextBox является источником, а TextBlock - приемником привязки. Свойство Text элемента TextBlock привязывается к свойству Text элемента TextBox. В итоге при осуществлении ввода в текстовое поле синхронно будут происходить изменения в текстовом блоке.
_________________________________________
**Работа с привязкой в C#**
Ключевым объектом при создании привязки является объект **System.Windows.Data.Binding.** Используя этот объект мы можем получить уже имеющуюся привязку для элемента:
```C#
Binding binding = BindingOperations.GetBinding(myTextBlock, TextBlock.TextProperty);
```
В данном случае получаем привязку для свойства зависимостей TextProperty элемента myTextBlock.

Также можно полностью установить привязку в коде C#:
```C#
public MainWindow()
{
    InitializeComponent();
 
 
    Binding binding = new Binding();
 
    binding.ElementName = "myTextBox"; // элемент-источник
    binding.Path = new PropertyPath("Text"); // свойство элемента-источника
    myTextBlock.SetBinding(TextBlock.TextProperty, binding); // установка привязки для элемента-приемника
}
```
Если в дальнейшем нам станет не нужна привязка, то мы можем воспользоваться классом **BindingOperations** и его методами **ClearBinding()**(удаляет одну привязку) и **ClearAllBindings()** (удаляет все привязки для данного элемента)
```C#
	
BindingOperations.ClearBinding(myTextBlock, TextBlock.TextProperty);
```
или
```C#
BindingOperations.ClearAllBindings(myTextBlock);
```
Некоторые свойства класса **Binding**:

- **lementName**: имя элемента, к которому создается привязка

- **IsAsync**: если установлено в True, то использует асинхронный режим получения данных из объекта. По умолчанию равно False

- **Mode**: режим привязки

- **Path**: ссылка на свойство объекта, к которому идет привязка

- **TargetNullValue**: устанавливает значение по умолчанию, если привязанное свойство источника привязки имеет значение null

- **RelativeSource**: создает привязку относительно текущего объекта

- **Source**: указывает на объект-источник, если он не является элементом управления.

- **XPath**: используется вместо свойства path для указания пути к xml-данным
