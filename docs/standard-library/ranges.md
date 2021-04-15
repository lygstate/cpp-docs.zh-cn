---
title: <ranges>
description: 标准模板库 (STL) 范围库概述
ms.date: 04/14/2021
f1_keywords:
- <ranges>
helpviewer_keywords:
- ranges
ms.openlocfilehash: d805039a8c3920bdd5dedcb5d40acb3b651a7033
ms.sourcegitcommit: aaab04df80e2d00389c13b075cfac59afc7f4681
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/14/2021
ms.locfileid: "107467611"
---
# `<ranges>`

从较高层面来说，范围是可以循环访问的内容。 范围抽象迭代器的方式可简化和加大使用标准模板库 (STL) 的能力。

STL 算法通常采用迭代器，该迭代器指向应在其上运行的集合的部分。 考虑今天的排序方式 `vector` 。 若要调用 `std::sort()` ，请传递两个迭代器，该迭代器标记的开头和结尾 `vector` 。 这可提供灵活性，但将迭代器传递到算法是一种额外的干扰，因为在大多数情况下，只需对整个操作进行排序即可。

使用范围，只需调用，就 `std::ranges::sort(myVector);` 像是 `std::sort(myVector.begin(), myVector.end());` 在范围库中调用的一样，算法会将范围用作参数 (即使你需要) 也是如此。 中可用的范围算法的示例包括、、、、、、、、、、、、和 `<algorithm>` `copy` `copy_n` `copy_if` `all_of` `any_of` `none_of` `find` `find_if` `find_if_not` `count` `count_if` `for_each` `for_each_n` `equal` `mismatch` 。

更易于编写且可读性更强的代码非常好，但是范围的优点比此更多。 它们还使您能够更轻松地编写 STL 算法，从而更容易筛选和转换部分数据的集合。

## <a name="a-ranges-example"></a>范围示例

在范围之前，若要仅转换满足特定条件的集合中的元素，则需要引入中间步骤来保存操作之间的结果。 例如，假设您想要仅从另一向量中可被3整除的元素生成一个方形向量。 您可以编写如下所示的内容：

```cpp
std::vector<int> input = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
std::vector<int> intermediate, output;

std::copy_if(input.begin(), input.end(), std::back_inserter(intermediate), [](const int i) { return i%3 == 0; });
std::transform(intermediate.begin(), intermediate.end(), std::back_inserter(output), [](const int i) {return i*i; });
```

对于范围，可以完成相同的操作，而无需 `intermediate` 矢量：

```cpp
// requires /std:c++latest
std::vector<int> input = { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };

auto output = input | std::views::filter([](const int n) {return n % 3 == 0; }) | std::views::transform([](const int n) {return n * n; });
```  

除了更易于阅读，它还可以避免矢量及其内容所需的内存分配 `intermediate` ，同时还允许您编写两个操作。

在上面的代码中，可除以三的每个元素都与一个操作来与该元素相结合。 " `|` " 符号将操作链接在一起，并从左向右读取。

结果 `output` 就是一种称为 "视图" 的范围，接下来将对此进行讨论。

> [!NOTE]
> 范围示例需要 [`/std:c++latest`](../build/reference/std-specify-language-standard-version.md) 编译器选项。

## <a name="views"></a>视图

视图是一种范围，其中包含所有视图操作 (默认构造、移动构造/赋值、复制构造/赋值 (（如果存在) 、析构、开始和结束) ，而不考虑视图中的元素数）。

视图中的元素的显示方式取决于您为视图指定的算法或操作。 在上面的示例中，视图采用范围并仅返回可被三整除的元素的视图。 基础范围保持不变。

视图是可组合的。 在上面的示例中，可被三整除的矢量元素的视图与用来表示这些元素的视图组合在一起。

对视图的元素进行惰式计算。 也就是说，在请求元素之前，将不会计算应用于在视图中生成元素的转换。 例如，如果您在调试程序中运行以下代码，并在行和上放置了一个 `auto divisible_by_three = ...` 断点 `auto square =  ...` ，则您将看到在中的 `divisible_by_three` 每个元素 `input` 都被 divisibility 三个测试的情况下，您将看到 lambda 断点。 `square`Lambda 断点将被命中，因为可除以三的元素是平方。

```cpp
// requires /std:c++latest
#include <ranges>
#include <vector>
#include <iostream>

int main()
{
    std::vector<int> input =  { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10 };
    auto divisible_by_three = [](const int n) {return n % 3 == 0; };
    auto square = [](const int n) {return n * n; };

    auto x = input | std::views::filter(divisible_by_three)
                   | std::views::transform(square);

    for (int i : x)
    {
        std::cout << i << '\n';
    }
    return 0;
}
```

## <a name="view-adaptors"></a>查看适配器

视图适配器生成一个范围的视图。 正在查看的范围保持不变。 视图不拥有任何元素。 它允许您使用您指定的自定义行为来循环访问基础范围。

在上面的示例中，第一个视图提供可被 `input` 三整除的的元素。 另一个视图采用由三个元素整除的元素，并提供元素的正方形。

`<ranges>`该库提供多种类型的视图适配器。 除了 "筛选器" 和 "转换" 视图以外，还可以使用某些视图来执行或跳过范围中的前 N 个元素，颠倒范围的顺序，联接范围，跳过范围中的元素，直到满足条件，转换范围的元素，等等。

## <a name="range-adaptors"></a>范围内的适配器

范围适配器从现有范围生成新范围并转换其元素的访问方式。 例如，范围适配器可能会采用一个范围并生成一个新的范围，以按相反的顺序提供原始范围内的元素。 前面所述的视图是一种通用的范围适配器。

范围适配器生成延迟计算的范围。 也就是说，不会产生任何费用，即转换范围中的每个元素（仅限你访问的元素）以及访问这些元素的时间。

范围内的适配器有多种形式。 例如，你可以使用范围适配器基于谓词 () 来筛选另一个范围 `view::filter` ，转换范围中的元素 (`view::transform`) 、拆分范围 (`view::split()`) 等。

范围内的适配器可以链接或组合--这是范围的强大功能和灵活性最明显的地方。

## <a name="range-algorithms"></a>范围算法

已创建采用范围参数的范围算法。 例如 `std::ranges::sort(myVector);`

范围算法与命名空间中的相应迭代器对算法几乎相同 `std` ，不同之处在于它们具有概念强制约束，并接受范围参数或更常见的迭代器-sentinel 参数对。 它们可以直接在一个容器上工作，并且可以轻松地链接在一起。

## <a name="types-of-ranges"></a>范围类型

使用范围时可以执行的操作取决于范围的基础迭代器类型。 范围概念是对概念的优化 `range` 。 在 c + + 20 中，假设概念 X 精炼概念 Y 意味着满足 Y 的所有内容也能满足 X 的所有条件，尽管这不一定是如此。 例如，汽车、客车和卡车均为优化车辆。

范围概念反映迭代器类别的层次结构。 此表列出了各种范围概念，以及可应用到的容器类型：

| 范围概念 | 说明 | 支持的容器 |
|--|--|--|
| `std::ranges::input_range` | 最少可循环访问一次 |
| `std::forward_list`<br>`std::unordered_map`<br>`std::unordered_multimap`<br>`std::unordered_set`<br>`std::unordered_multiset`<br>`basic_istream_view` |
| `std::ranges::forward_range` | 可以多次循环访问)  | `std::forward_list`<br>`std::unordered_map`<br>`std::unordered_multimap`<br>`std::unordered_set`<br>`std::unordered_multiset` |
| `std::ranges::bidirectional_range` | 可以多次循环访问 | `std::list`<br>`std::map`<br>`std::multimap`<br>`std::multiset`<br>`std::set`|
| `std::ranges::random_access_range` | 可以使用运算符)  (在常量时间访问任意元素 `[]`)  | `std::deque` |
| `std::ranges::contiguous_range` | 元素连续存储在内存中 | `std::array`<br>`std::string`<br>`std::vector` |



## <a name="see-also"></a>另请参阅

[头文件引用](../standard-library/cpp-standard-library-header-files.md)