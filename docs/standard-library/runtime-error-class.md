---
title: "runtime_error 类 | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-cpp
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- std.runtime_error
- runtime_error
- stdexcept/std::runtime_error
- std::runtime_error
dev_langs:
- C++
helpviewer_keywords:
- runtime_error class
ms.assetid: 4d0227bf-847b-45a2-a320-2351ebf98368
caps.latest.revision: 20
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
ms.sourcegitcommit: 3168772cbb7e8127523bc2fc2da5cc9b4f59beb8
ms.openlocfilehash: 10185339d7f9f90c4651f68451ce3012439f4ac2
ms.lasthandoff: 02/24/2017

---
# <a name="runtimeerror-class"></a>runtime_error 类
此类用作引发报告仅在执行程序时大概可检测的错误的所有异常的基类。  
  
## <a name="syntax"></a>语法  
  
```  
class runtime_error : public exception {  
public:  
    explicit runtime_error(const string& message);

    explicit runtime_error(const char *message);

};  
```  
  
## <a name="remarks"></a>备注  
 [exception 类](../standard-library/exception-class.md)返回的值是 **message**`.`[data](../standard-library/basic-string-class.md#basic_string__data) 的副本。  
  
## <a name="example"></a>示例  
  
```cpp  
// runtime_error.cpp  
// compile with: /EHsc /GR  
#include <iostream>  
  
using namespace std;  
  
int main( )  
{  
// runtime_error  
   try   
   {  
      locale loc( "test" );  
   }  
   catch ( exception &e )   
   {  
      cerr << "Caught " << e.what( ) << endl;  
      cerr << "Type " << typeid( e ).name( ) << endl;  
   };  
}  
\* Output:   
Caught bad locale name  
Type class std::runtime_error  
*\  
```  
  
## <a name="requirements"></a>要求  
 **标头：**\<stdexcept>  
  
 **命名空间：** std  
  
## <a name="see-also"></a>另请参阅  
[exception 类](../standard-library/exception-class.md)

    
 [C++ 标准库中的线程安全](../standard-library/thread-safety-in-the-cpp-standard-library.md)

