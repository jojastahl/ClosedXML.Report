---
title: Простой шаблон
---

# Простой шаблон

Вы можете использовать _выражения_ с фигурными скобками {% raw %}`{{}}`{% endraw %} в любой ячейке любого листа _шаблона_ и Excel найдёт эти значения во время выполнения. Как? Чтобы обеспечить работу этого механизма ClosedXML.Report добавляет в книгу шаблона невидимый лист, куда переносит значения всех полей набора данных из текущей записи. Затем ячейки со значениями именуются. 

Формулы Excel, в которые добавлены _переменные_, должны быть экранированы `&`. В качестве примера: {% raw %}`&=CONCATENATE({{Addr1}}," ", {{Addr2}})`{% endraw %}. Обратите внимание, что экранированные формулы должны соответствовать международному, нелокализованному синтаксису, который включает в себя английские названия функций, запятую в качестве разделителя значений и т.д. Например, в русской версии Excel вы можете использовать формулу `=СУММ(A1:B2; E1:F2)` для обычных ячеек, но escape-формула должна быть `&=SUM(A1:B2, E1:F2)`.


Ячейки с формулами полей могут быть отформатированы любым известным способом, включая условное форматирование.

Простой пример:

![simpletemplate](../../images/simple-template-01.png)

```c#
...
        var template = new XLTemplate(@".\Templates\template.xlsx");
        var cust = db.Customers.GetById(10);

        template.AddVariable(cust);
        // OR
        template.AddVariable("Company", cust.Company);
        template.AddVariable("Addr1", cust.Addr1);
        template.AddVariable("Addr2", cust.Addr2);
...

public class Customer
{
	public double CustNo { get; set; }
	public string Company { get; set; }
	public string Addr1 { get; set; }
	public string Addr2 { get; set; }
	public string City { get; set; }
	public string State { get; set; }
	public string Zip { get; set; }
	public string Country { get; set; }
	public string Phone { get; set; }
	public string Fax { get; set; }
	public double? TaxRate { get; set; }
	public string Contact { get; set; }
}

```