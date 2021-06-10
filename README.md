# ТЕКСТОВЫЙ РЕДАКТОР НА .NET

## ОПИСАНИЕ

Класс текстового редактора включающий в себя панель инструментов. Панель инструментов содержит все базовые необходимые кнопки с изображениями. Изображения находятся в вспомогательном классе в виде байтовых массивов.

В классе реализованы базовое управление текстом уровня WordPad.
Поддерживаются горячие клавиши:

- Ctrl-C (копирование)
- Ctrl-V (вставка)
- Ctrl-B, Ctrl-I, Ctrl-U (управление стилем: жирный, наклонный и подчеркнутый шрифт)
- Ctrl-L, Ctrl-E, Ctrl-R (управление выравниванием: левый край, центр, правый край)

## ПУБЛИЧНЫЕ МЕТОДЫ И СВОЙСТВА

Член класса | Тип | Описание
----------- | --- | --------
RichTextBox txtBox | Свойство | Прямой доступ к объекту RichTextBox.
bool textWasChanged | Свойство | Признак изменения теста в редакторе пользователем. Должен сбрасываться вручную в false, например после сохранения текста. Автоматически устанавливается в true, если текст был изменен, включая форматирование.
ToolBoxPosition ToolBoxPos | Свойство | Задает положение панели инструментов: вверху (OnTop) или внизу (OnBottom).
ContentChanged OnContentChanged | Событие | Вызывается, когда пользователь меняет текст (дублирует событие TextChanged компонента RichTextBox).
ToolStrip tsMenu | Объект | Прямой доступ к панели инструментов (ToolStrip) для добавления собственных кнопок.
Action userAction1<br/>Action userAction2<br/>Action userAction3 | Метод | Пользовательские методы. Могут быть использованы, если необходимо быстро добавить пользовательские функции без выполнения наследования класса. Удобно при использовании нескольких редакторов текста на одной форме.
TextEditor(Control parent, ImageList images = null) | Конструктор | Задает родительский контрол для текстового редактора, в котором он будет вызван с параметром Dock=Fill. Позволяет либо задать внешний список изображений для кнопок, либо использовать внутренний.

## ПРИМЕР ИСПОЛЬЗОВАНИЯ

```C#
public TextEditor myTextEditor;

public Form1()
{
    InitializeComponent();

    // создать текстовый редактор, и разместить его на всю форму
    myTextEditor = new TextEditor(this);
    // расположить панель инструментов внизу, по умолчанию вверху
    myTextEditor.ToolBoxPos = TextEditor.ToolBoxPosition.OnBottom;
    // создать обработчик событий отслеживающий изменения текста (опционально)
    myTextEditor.OnContentChanged += myTextEditor_OnContentChanged;
    // через прямой доступ к объекту RichTextBox добавить свой обработчик нажатия клавиш
    // например Ctrl-S (опционально)
    myTextEditor.txtBox.KeyDown += myTextEditor_KeyDown;
    // можно добавить пользовательский код к текстовому редактору (что бы не делать наследование
    // класса с добавлением методов)
    myTextEditor.userAction1 = delegate
    {
        // например, сменить картинку на кнопке сохранения
        btnSaved.ImageKey = "saved";
        // установить признак изменного теста
        myTextEditor.textWasChanged = false;
    };
}
```

![Sample of interface1](https://github.com/ezik117/TextEditor/blob/main/README_files/screenshot1.png)