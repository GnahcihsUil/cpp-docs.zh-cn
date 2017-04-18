---
title: "enable_shared_from_this 类 | Microsoft 文档"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-cpp
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- enable_shared_from_this
- std::enable_shared_from_this
- memory/std::enable_shared_from_this
dev_langs:
- C++
helpviewer_keywords:
- enable_shared_from_this class
- enable_shared_from_this
ms.assetid: 9237603d-22e2-421f-b070-838ac006baf5
caps.latest.revision: 22
author: corob-msft
ms.author: corob
manager: ghogen
translation.priority.mt:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: f293f074f2b8e2334dc70fbebba8e6f4c17efecc
ms.openlocfilehash: 7f32ee8a40da16ac919f0c3d8be05573f7b78c3a
ms.lasthandoff: 02/24/2017

---
# <a name="enablesharedfromthis-class"></a>enable_shared_from_this 类
帮助生成一个 `shared_ptr`。  
  
## <a name="syntax"></a>语法  
```    
class enable_shared_from_this {
public:
    shared_ptr<Ty>
        shared_from_this();
    shared_ptr<const Ty> shared_from_this() const;
protected:
    enable_shared_from_this();
    enable_shared_from_this(const enable_shared_from_this&);
    enable_shared_from_this& operator=(const enable_shared_from_this&);
    ~enable_shared_from_this();
}; 
``` 
#### <a name="parameters"></a>参数  
 `Ty`  
 由共享指针控制的类型。  
  
## <a name="remarks"></a>备注  
 从 `enable_shared_from_this` 派生的对象可以在成员函数中使用 `shared_from_this` 方法来创建实例的 [shared_ptr](../standard-library/shared-ptr-class.md) 所有者，这些所有者与现有 `shared_ptr` 所有者共享所有权。 否则，如果使用 `this` 创建一个新的 `shared_ptr`，则其与现有的 `shared_ptr` 所有者不同，从而会导致无效引用或导致此对象被删除多次。  
  
 保护构造函数、析构函数和赋值运算符，以帮助预防意外的误用。 模板参数类型 `Ty` 必须是派生类类型。  
  
 有关使用示例，请参阅 [enable_shared_from_this::shared_from_this](#enable_shared_from_this__shared_from_this)。  
  
## <a name="requirements"></a>要求  
 **标头：**\<memory>  
  
 **命名空间：** std  
  
##  <a name="a-nameenablesharedfromthissharedfromthisa--enablesharedfromthissharedfromthis"></a><a name="enable_shared_from_this__shared_from_this"></a>  enable_shared_from_this::shared_from_this  
 生成与现有 `shared_ptr` 所有者共享实例所有权的 `shared_ptr`。  
  
```  
shared_ptr<T> shared_from_this();
shared_ptr<const T> shared_from_this() const;
```  
  
### <a name="remarks"></a>备注  
 从 `enable_shared_from_this` 基类派生对象时，`shared_from_this` 模板成员函数返回与现有 `shared_ptr` 所有者共享此实例所有权的 [shared_ptr 类](../standard-library/shared-ptr-class.md)对象。 否则，如果通过 `this` 创建一个新的 `shared_ptr`，则其与现有的 `shared_ptr` 所有者不同，从而会导致无效引用或导致此对象被删除多次。 如果在尚未由 `shared_ptr` 对象所有的实例上调用 `shared_from_this`，则不会定义行为。  
  
### <a name="example"></a>示例  
  
```cpp  
// std_memory_shared_from_this.cpp   
// compile with: /EHsc   
#include <memory>  
#include <iostream>  
  
using namespace std;  
  
struct base : public std::enable_shared_from_this<base>  
{  
    int val;    
    shared_ptr<base> share_more()  
    {  
        return shared_from_this();  
    }  
};  
  
int main()  
{  
    auto sp1 = make_shared<base>();  
    auto sp2 = sp1->share_more();  
  
    sp1->val = 3;  
    cout << "sp2->val == " << sp2->val << endl;    
    return 0;  
}   
```  
  
```Output  
sp2->val == 3  
```  
  
## <a name="see-also"></a>另请参阅  
 [enable_shared_from_this::shared_from_this](#enable_shared_from_this__shared_from_this)   
 [shared_ptr 类](../standard-library/shared-ptr-class.md)