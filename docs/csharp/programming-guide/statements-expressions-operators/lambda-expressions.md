---
title: "람다 식(C# 프로그래밍 가이드)"
ms.date: 03/03/2017
ms.prod: .net
ms.technology:
- devlang-csharp
ms.topic: article
helpviewer_keywords:
- lambda expressions [C#]
- outer variables [C#]
- statement lambda [C#]
- expression lambda [C#]
- expressions [C#], lambda
ms.assetid: 57e3ba27-9a82-4067-aca7-5ca446b7bf93
caps.latest.revision: 
author: BillWagner
ms.author: wiwagn
ms.openlocfilehash: 14bb60a5009f9a1ae59ed9846ebc868cfdcc05c6
ms.sourcegitcommit: 83dd5ec003e788ccb3e33f3412a7af39ae347646
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/15/2018
---
# <a name="lambda-expressions-c-programming-guide"></a>람다 식(C# 프로그래밍 가이드)
람다 식은 [대리자](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md) 또는 [식 트리](../../../csharp/programming-guide/delegates/using-delegates.md) 형식을 만드는 데 사용할 수 있는 [익명 함수](http://msdn.microsoft.com/library/fb1d3ed8-d5b0-4211-a71f-dd271529294b) 입니다. 람다 식을 사용하여 인수로 전달되거나 함수 호출 값으로 반환되는 로컬 함수를 쓸 수 있습니다. 람다 식은 LINQ 쿼리 식을 작성하는 데 특히 유용합니다.  
  
 람다 식을 만들려면 람다 연산자 [=>](../../../csharp/language-reference/operators/lambda-operator.md)왼쪽에 입력 매개 변수를 지정하고(있는 경우) 다른 쪽에 식이나 문 블록을 삽입합니다. 예를 들어 람다 식 `x => x * x` 는 이름이 `x` 인 매개 변수를 지정하고 `x` 제곱 값을 반환합니다. 다음 예제와 같이 대리자 형식에 이 식을 할당할 수도 있습니다.  
  
```csharp  
delegate int del(int i);  
static void Main(string[] args)  
{  
    del myDelegate = x => x * x;  
    int j = myDelegate(5); //j = 25  
}  
```  
  
 식 트리 형식을 만들려면  
  
```csharp  
using System.Linq.Expressions;  
  
namespace ConsoleApplication1  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            Expression<del> myET = x => x * x;  
        }  
    }  
}  
```  
  
 `=>` 연산자는 대입(`=`)과 우선 순위가 같고 [오른쪽 결합형](../../../csharp/programming-guide/statements-expressions-operators/operators.md)입니다(연산자 문서의 "결합성" 섹션 참조).  
  
 람다 식은 메서드 기반 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 쿼리에서 <xref:System.Linq.Enumerable.Where%2A> 같은 표준 쿼리 연산자 메서드의 인수로 사용됩니다.  
  
 <xref:System.Linq.Enumerable.Where%2A> to Objects 및 <xref:System.Linq.Enumerable> 에서처럼 메서드 기반의 구문을 사용하여 [!INCLUDE[vbteclinq](~/includes/vbteclinq-md.md)] 클래스에서 [!INCLUDE[sqltecxlinq](~/includes/sqltecxlinq-md.md)]메서드를 호출하는 경우 매개 변수는 <xref:System.Func%602?displayProperty=nameWithType>대리자 형식입니다. 람다 식은 이러한 대리자를 만드는 가장 간단한 방법입니다. 예를 들어 [!INCLUDE[vbtecdlinq](~/includes/vbtecdlinq-md.md)]에서처럼 이 메서드를 <xref:System.Linq.Queryable?displayProperty=nameWithType> 클래스에서 호출하는 경우 매개 변수 형식은 <xref:System.Linq.Expressions.Expression?displayProperty=nameWithType><Func\>이고, 여기서 Func는 입력 매개 변수를 16개까지 가질 수 있는 임의의 Func 대리자입니다. 이 경우에도 람다 식을 사용하면 식 트리를 간단하게 만들 수 있습니다. 람다 식은 `Where` 호출과 비슷하게 보일 수 있지만 실제로 람다 식을 통해 생성되는 개체 형식은 다릅니다.  
  
 위의 예제에서 대리자 시그니처는 형식이 암시적으로 지정된 `int`형식의 입력 매개 변수 하나를 포함하고 `int`를 반환합니다. 람다 식에도 입력 매개 변수 하나(`x`)와 컴파일러에서 `int` 형식으로 암시적으로 변환할 수 있는 반환 값이 있기 때문에 람다 식을 이 형식의 대리자로 변환할 수 있습니다. 형식 유추는 다음 단원에서 자세하게 설명합니다. 입력 매개 변수를 5로 사용하여 대리자를 호출하면 25라는 결과가 반환됩니다.  
  
 [is](../../../csharp/language-reference/keywords/is.md) 또는 [as](../../../csharp/language-reference/keywords/as.md) 연산자의 왼쪽에는 람다 식을 사용할 수 없습니다.  
  
 무명 메서드에 적용되는 모든 제한은 람다 식에도 적용됩니다. 자세한 내용은 [무명 메서드](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)를 참조하세요.  
  
## <a name="expression-lambdas"></a>식 람다  
 => 연산자의 오른쪽에 식이 있는 람다 식을 *식 람다*라고 합니다. 식 람다는 [식 트리](http://msdn.microsoft.com/library/fb1d3ed8-d5b0-4211-a71f-dd271529294b)를 만드는 데 광범위하게 사용됩니다. 식 람다는 식의 결과를 반환하며 기본 형식은 다음과 같습니다.  
  
```csharp
(input-parameters) => expression
```

 괄호는 람다 식에 입력 매개 변수가 하나뿐인 경우에만 생략할 수 있고 그렇지 않으면 생략할 수 없습니다. 둘 이상의 입력 매개 변수는 다음과 같이 괄호로 묶고 쉼표로 구분해야 합니다.  
  
```csharp
(x, y) => x == y
```

 컴파일러에서 입력 형식을 유추할 수 없는 경우도 있습니다. 이와 같은 경우에는 다음 예제와 같이 형식을 명시적으로 지정할 수 있습니다.  
  
```csharp
(int x, string s) => s.Length > x
```

 입력 매개 변수가 0개이면 다음과 같이 빈 괄호를 지정합니다.  
  
```csharp
() => SomeMethod()
```

 위의 예제에서 식 람다의 본문은 메서드 호출로 구성될 수 있습니다. 하지만 SQL Server와 같은 .NET Framework 외부에서 평가되는 식 트리를 만드는 경우에는 람다 식에 메서드 호출을 사용하지 않아야 합니다. 이러한 메서드는 .NET 공용 언어 런타임의 컨텍스트 안에서만 의미가 있습니다.  
  
## <a name="statement-lambdas"></a>문 람다  
 문 람다는 다음과 같이 중괄호 안에 문을 지정한다는 점을 제외하면 식 람다와 비슷합니다.  
  
(input-parameters) => { statement; }

 문 람다의 본문에 지정할 수 있는 문의 개수에는 제한이 없지만 일반적으로 2-3개 정도만 지정합니다.  
  
[!code-csharp[StatementLamba#1](../../../../samples\snippets\csharp\programming-guide\lambda-expressions/statements.cs#1)]

[!code-csharp[StatementLamba#2](../../../../samples\snippets\csharp\programming-guide\lambda-expressions/statements.cs#2)]

 무명 메서드와 마찬가지로 문 람다는 식 트리를 만드는 데 사용할 수 없습니다.  
  
## <a name="async-lambdas"></a>비동기 람다  
 [async](../../../csharp/language-reference/keywords/async.md) 및 [await](../../../csharp/language-reference/keywords/await.md) 키워드를 사용하여 비동기 처리를 통합하는 람다 식과 문을 쉽게 만들 수 있습니다. 예를 들어 다음 Windows Forms 예제에는 비동기 메서드 `ExampleMethodAsync`를 호출하고 기다리는 이벤트 처리기가 포함되어 있습니다.  
  
```csharp
public partial class Form1 : Form  
{  
    public Form1()  
    {  
        InitializeComponent();  
    }  
  
    private async void button1_Click(object sender, EventArgs e)  
    {  
        // ExampleMethodAsync returns a Task.  
        await ExampleMethodAsync();  
        textBox1.Text += "\r\nControl returned to Click event handler.\n";  
    }  
  
    async Task ExampleMethodAsync()  
    {  
        // The following line simulates a task-returning asynchronous process.  
        await Task.Delay(1000);  
    }  
}  
```

 비동기 람다를 사용하여 동일한 이벤트 처리기를 추가할 수 있습니다. 이 처리기를 추가하려면 다음 예제에 표시된 것처럼 람다 매개 변수 목록에 `async` 한정자를 추가합니다.  
  
```csharp  
public partial class Form1 : Form  
{  
    public Form1()  
    {  
        InitializeComponent();  
        button1.Click += async (sender, e) =>  
        {  
            // ExampleMethodAsync returns a Task.  
            await ExampleMethodAsync();  
            textBox1.Text += "\nControl returned to Click event handler.\n";  
        };  
    }  
  
    async Task ExampleMethodAsync()  
    {  
        // The following line simulates a task-returning asynchronous process.  
        await Task.Delay(1000);  
    }  
}  
```  

 비동기 메서드를 만들고 사용하는 방법에 대한 자세한 내용은 [Async 및 Await를 사용한 비동기 프로그래밍](../../../csharp/programming-guide/concepts/async/index.md)을 참조하세요.  
  
## <a name="lambdas-with-the-standard-query-operators"></a>표준 쿼리 연산자와 람다 식  
 대부분의 표준 쿼리 연산자에는 형식이 제네릭 대리자의 <xref:System.Func%602> 패밀리 중 하나인 입력 매개 변수를 사용합니다. 이러한 대리자는 형식 매개 변수를 사용하여 입력 매개 변수의 수와 형식 및 대리자의 반환 형식을 정의합니다. `Func` 대리자는 소스 데이터 집합에 있는 각 요소에 적용할 사용자 정의 식을 캡슐화하는 데 매우 유용합니다. 다음 대리자 형식을 예로 들 수 있습니다.  
  
```csharp  
public delegate TResult Func<TArg0, TResult>(TArg0 arg0)  
```  
  
 이 경우 대리자를 `Func<int,bool> myFunc` 로 인스턴스화할 수 있습니다. 여기서 `int` 는 입력 매개 변수이고, `bool` 은 반환 값입니다. 반환 값은 항상 마지막 형식 매개 변수에 지정됩니다. `Func<int, string, bool>` 은 두 입력 매개 변수 `int` 및 `string`과 반환 형식 `bool`을 사용하여 대리자를 정의합니다. 다음 `Func` 대리자를 호출하면 입력 매개 변수가 5인지 여부를 나타내는 true 또는 false가 반환됩니다.  
  
```csharp  
Func<int, bool> myFunc = x => x == 5;  
bool result = myFunc(4); // returns false of course  
```  
  
 System.Linq.Queryable에 정의되어 있는 표준 쿼리 연산자의 경우와 같이 인수 형식이 `Expression<Func>`인 경우에도 람다 식을 사용할 수 있습니다. `Expression<Func>` 인수를 지정하면 식 트리에 람다 식이 컴파일됩니다.  
  
 다음 코드에서는 표준 쿼리 연산자인 <xref:System.Linq.Enumerable.Count%2A> 메서드를 보여 줍니다.  
  
```csharp  
int[] numbers = { 5, 4, 1, 3, 9, 8, 6, 7, 2, 0 };  
int oddNumbers = numbers.Count(n => n % 2 == 1);  
```  
  
 컴파일러에서 입력 매개 변수의 형식을 유추하거나 사용자가 형식을 명시적으로 지정할 수 있습니다. 이 람다 식은 2로 나누었을 때 나머지가 1인 정수(`n`)의 수를 계산합니다.  
  
 다음 코드 줄은 숫자 시퀀스에서 조건을 만족하지 않는 첫 번째 숫자가 "9"이기 때문에 `numbers` 배열에서 "9" 왼쪽에 있는 모든 요소가 포함된 시퀀스를 생성합니다.  
  
```csharp  
var firstNumbersLessThan6 = numbers.TakeWhile(n => n < 6);  
```  
  
 이 예제에서는 괄호로 묶어 입력 매개 변수를 여러 개 지정하는 방법을 보여 줍니다. 이 메서드는 값이 해당 위치보다 작은 숫자를 발견할 때까지 숫자 배열의 모든 요소를 반환합니다. 여기서 람다 연산자(`=>`)를 크거나 같음 연산자(`>=`)와 혼동하면 안 됩니다.  
  
```csharp  
var firstSmallNumbers = numbers.TakeWhile((n, index) => n >= index);  
```  
  
## <a name="type-inference-in-lambdas"></a>람다 식에서의 형식 유추  
 컴파일러에서는 람다 식 본문, 매개 변수의 대리자 형식 및 C# 언어 사양에 설명되어 있는 기타 요소를 기준으로 형식을 유추할 수 있기 때문에 대부분의 경우에는 람다 식을 작성할 때 입력 매개 변수의 형식을 지정하지 않아도 됩니다. 대부분의 표준 쿼리 연산자에서 첫 번째 입력 형식은 소스 시퀀스 요소의 형식입니다. 따라서 `IEnumerable<Customer>`를 쿼리할 경우 입력 변수가 `Customer` 개체로 유추됩니다. 이는 이 개체의 메서드와 속성에 액세스할 수 있음을 의미합니다.  
  
```csharp  
customers.Where(c => c.City == "London");  
```  
  
 람다 식에는 다음과 같은 일반적인 규칙이 적용됩니다.  
  
-   람다 식과 대리자 형식에 포함된 매개 변수 수가 같아야 합니다.  
  
-   람다 식의 각 입력 매개 변수는 해당되는 대리자 매개 변수로 암시적으로 변환될 수 있어야 합니다.  
  
-   람다 식의 반환 값(있는 경우)은 대리자의 반환 형식으로 암시적으로 변환될 수 있어야 합니다.  
  
 공용 형식 시스템에는 "람다 식"이라는 개념이 기본적으로 포함되어 있지 않기 때문에 람다 식 자체에는 형식이 없습니다. 그러나 람다 식의 "형식"을 비공식적으로 언급해야 할 경우도 있는데 이 경우 형식은 대리자 형식 또는 람다 식이 변환되는 <xref:System.Linq.Expressions.Expression> 형식을 의미합니다.  
  
## <a name="variable-scope-in-lambda-expressions"></a>람다 식의 변수 범위  
 람다 식은 람다 함수를 정의하는 메서드 범위 내에 있거나 람다 식을 포함하는 형식 범위 내에 있는 *외부 변수*([무명 메서드](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md) 참조)를 참조할 수 있습니다. 이러한 방식으로 캡처되는 변수는 변수가 범위를 벗어나 가비지 수집되는 경우에도 람다 식에 사용할 수 있도록 저장됩니다. 외부 변수는 명확하게 할당해야만 람다 식에 사용할 수 있습니다. 다음 예제에서는 이러한 규칙을 보여 줍니다.  
  
```csharp  
delegate bool D();  
delegate bool D2(int i);  
  
class Test  
{  
    D del;  
    D2 del2;  
    public void TestMethod(int input)  
    {  
        int j = 0;  
        // Initialize the delegates with lambda expressions.  
        // Note access to 2 outer variables.  
        // del will be invoked within this method.  
        del = () => { j = 10;  return j > input; };  
  
        // del2 will be invoked after TestMethod goes out of scope.  
        del2 = (x) => {return x == j; };  
  
        // Demonstrate value of j:  
        // Output: j = 0   
        // The delegate has not been invoked yet.  
        Console.WriteLine("j = {0}", j);        // Invoke the delegate.  
        bool boolResult = del();  
  
        // Output: j = 10 b = True  
        Console.WriteLine("j = {0}. b = {1}", j, boolResult);  
    }  
  
    static void Main()  
    {  
        Test test = new Test();  
        test.TestMethod(5);  
  
        // Prove that del2 still has a copy of  
        // local variable j from TestMethod.  
        bool result = test.del2(10);  
  
        // Output: True  
        Console.WriteLine(result);  
  
        Console.ReadKey();  
    }  
}  
```  
  
 람다 식의 변수 범위에는 다음과 같은 규칙이 적용됩니다.  
  
-   캡처된 변수는 해당 변수를 참조하는 대리자가 가비지 수집 대상이 될 때까지 가비지 수집되지 않습니다.  
  
-   람다 식에 사용된 변수는 외부 메서드에 표시되지 않습니다.  
  
-   람다 식은 바깥쪽 메서드에서 `in`, `ref` 또는 `out` 매개 변수를 직접 캡처할 수 없습니다.  
  
-   람다 식의 return 문에 의해서는 바깥쪽 메서드가 반환되지 않습니다.  
  
-   점프문의 대상이 블록 외부에 있는 경우 람다 식에 람다 함수 내에 있는 `goto` 문, `break` 문 또는 `continue` 문을 포함할 수 없습니다. 대상이 블록 내에 있는 경우 람다 함수 블록 외부에 점프문을 사용해도 오류가 발생합니다.  
  
## <a name="c-language-specification"></a>C# 언어 사양  
 [!INCLUDE[CSharplangspec](~/includes/csharplangspec-md.md)]  
  
## <a name="featured-book-chapter"></a>중요 설명서 장  
 [C# 3.0 Cookbook, Third Edition: More than 250 solutions for C# 3.0 programmers](https://msdn.microsoft.com/library/orm-9780596516109-03-09.aspx) 의 [Delegates, Events, and Lambda Expressions](https://msdn.microsoft.com/library/orm-9780596516109-03.aspx)  
  
## <a name="see-also"></a>참고 항목  
 [C# 프로그래밍 가이드](../../../csharp/programming-guide/index.md)  
 [LINQ(Language-Integrated Query)](../../../csharp/programming-guide/concepts/linq/index.md)  
 [무명 메서드](../../../csharp/programming-guide/statements-expressions-operators/anonymous-methods.md)  
 [is](../../../csharp/language-reference/keywords/is.md)  
 [식 트리](../../../csharp/programming-guide/concepts/expression-trees/index.md)  
 [Visual Studio 2008 C# 샘플(LINQ 샘플 쿼리 파일 및 XQuery 프로그램 참조)](http://code.msdn.microsoft.com/Visual-Studio-2008-C-d295cdba)  
 [재귀 람다 식](https://blogs.msdn.microsoft.com/madst/2007/05/11/recursive-lambda-expressions/)
