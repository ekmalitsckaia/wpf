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
Для определения привязки используется выражение типа:
```

