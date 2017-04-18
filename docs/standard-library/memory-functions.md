---
title: "&lt;memory&gt; 函数 | Microsoft Docs"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- std::addressof
- memory/std::addressof
- std::align
- memory/std::align
- std::allocate_shared
- memory/std::allocate_shared
- std::const_pointer_cast
- memory/std::const_pointer_cast
- std::declare_no_pointers
- memory/std::declare_no_pointers
- std::declare_reachable
- memory/std::declare_reachable
- std::default_delete
- memory/std::default_delete
- std::dynamic_pointer_cast
- memory/std::dynamic_pointer_cast
- std::get_deleter_function
- memory/std::get_deleter_function
- std::get_pointer_safety
- memory/std::get_pointer_safety
- std::get_temporary_buffer
- memory/std::get_temporary_buffer
- std::make_shared
- memory/std::make_shared
- std::make_unique
- memory/std::make_unique
- std::owner_less
- memory/std::owner_less
- std::return_temporary_buffer
- memory/std::return_temporary_buffer
- std::static_pointer_cast
- memory/std::static_pointer_cast
- std::swap
- memory/std::swap
- std::undeclare_no_pointers
- memory/std::undeclare_no_pointers
- std::undeclare_reachable
- memory/std::undeclare_reachable
- std::uninitialized_copy
- memory/std::uninitialized_copy
- std::uninitialized_copy_n
- memory/std::uninitialized_copy_n
- std::uninitialized_fill
- memory/std::uninitialized_fill
- std::uninitialized_fill_n
- memory/std::uninitialized_fill_n
ms.assetid: 3e1898c2-44b7-4626-87ce-84962e4c6f1a
caps.latest.revision: 12
author: corob-msft
ms.author: corob
manager: ghogen
translationtype: Machine Translation
ms.sourcegitcommit: a937c9d083a7e4331af63323a19fb207142604a0
ms.openlocfilehash: bab363d16555ca66ce0b57aad4ac8f3d9aaad21b
ms.lasthandoff: 02/24/2017

---
# <a name="ltmemorygt-functions"></a>&lt;memory&gt; 函数
||||  
|-|-|-|  
|[addressof](#addressof)|[align](#align)|[allocate_shared](#allocate_shared)|  
|[const_pointer_cast](#const_pointer_cast)|[declare_no_pointers](#declare_no_pointers)|[declare_reachable](#declare_reachable)|  
|[default_delete](#default_delete)|[dynamic_pointer_cast](#dynamic_pointer_cast)|[get_deleter 函数](#get_deleter_function)|  
|[get_pointer_safety](#get_pointer_safety)|[get_temporary_buffer](#get_temporary_buffer)|[make_shared](#make_shared)|  
|[make_unique](#make_unique)|[owner_less](#owner_less)|[return_temporary_buffer](#return_temporary_buffer)|  
|[static_pointer_cast](#static_pointer_cast)|[swap（C++ 标准库）](#swap)|[undeclare_no_pointers](#undeclare_no_pointers)|  
|[undeclare_reachable](#undeclare_reachable)|[uninitialized_copy](#uninitialized_copy)|[uninitialized_copy_n](#uninitialized_copy_n)|  
|[uninitialized_fill](#uninitialized_fill)|[uninitialized_fill_n](#uninitialized_fill_n)|  
  
##  <a name="a-nameaddressofa--addressof"></a><a name="addressof"></a>addressof  
 获取对象的实际地址。  
  
```  
template <class T>  
T* addressof(T& Val);
```  
  
### <a name="parameters"></a>参数  
 `Val`  
 要获取其实际地址的对象或函数。  
  
### <a name="return-value"></a>返回值  
 由 `Val` 引用的对象或函数的实际地址，即使存在重载的 `operator&()`，情况也不例外。  
  
### <a name="remarks"></a>备注  
  
##  <a name="a-namealigna--align"></a><a name="align"></a>align  
 将给定大小的存储（通过给定对齐规范对齐）放入给定存储的第一个可能地址。  
  
```  
void* align(
    size_t Alignment, // input  
    size_t Size,   // input  
    void*& Ptr        // input/output  
    size_t& Space     // input/output);
```  
  
### <a name="parameters"></a>参数  
 `Alignment`  
 要尝试的对齐边界。  
  
 `Size`  
 对齐存储的大小（以字节为单位）。  
  
 `Ptr`  
 要使用的可用连续存储池的起始地址。 此参数还用作输出参数，如果对齐成功，将包含新的起始地址。  
  
 如果 `align()` 不成功，则不修改此参数。  
  
 `Space`  
 供 `align()` 用于创建对齐存储的总空间。 此参数还是输出参数，并包含存储缓冲区中在减去对齐存储和任何关联系统开销后剩余的调整空间。  
  
 如果 `align()` 不成功，则不修改此参数。  
  
### <a name="return-value"></a>返回值  
 如果请求的对齐缓冲区无法放入可用空间，则为 null 指针；否则为 `Ptr` 的新值。  
  
### <a name="remarks"></a>备注  
 通过修改的 `Ptr` 和 `Space` 参数，可以使用不同的 `align()` 值和 `Alignment` 值，对同一缓冲区重复调用 `Size`。 下面的代码片段演示 `align()` 的一种用法。  
  
```cpp  
#include <type_traits> // std::alignment_of()  
#include <memory>  
//...  
char buffer[256]; // for simplicity  
size_t alignment = std::alignment_of<int>::value;  
void * ptr = buffer;  
std::size_t space = sizeof(buffer); // Be sure this results in the true size of your buffer  
  
while (alignment, sizeof(MyObj), ptr, space)) {  
    // You now have storage the size of MyObj, starting at ptr, aligned on   
    // int boundary. Use it here if you like, or save off the starting address  
    // contained in ptr for later use.  
    // ...  
    // Last, move starting pointer and decrease available space before  
    // the while loop restarts.  
    ptr = reinterpret_cast<char*>(ptr) + sizeof(MyObj);  
    space -= sizeof(MyObj);  
}  
// At this point, align() has returned a null pointer, signaling it is not  
// possible to allow more aligned storage in this buffer.   
```  
  
##  <a name="a-nameallocateshareda--allocateshared"></a><a name="allocate_shared"></a>allocate_shared  
 创建指向对象的 `shared_ptr`，这些对象通过指定分配器针对给定类型分配和构造。 返回 `shared_ptr`。  
  
```  
template <class Type, class Allocator, class... Types>  
shared_ptr<Type>  
allocate_shared(Allocator Alloc, Types&&... Args);
```  
  
### <a name="parameters"></a>参数  
 `Alloc`  
 用于创建对象的分配器。  
  
 `Args`  
 成为对象的零个或更多自变量。  
  
### <a name="remarks"></a>备注  
 此函数创建对象 `shared_ptr``<Type>`，此对象为指向 `Type(``Args``...)` 的指针，通过 `Alloc` 分配和构造。  
  
##  <a name="a-nameconstpointercasta--constpointercast"></a><a name="const_pointer_cast"></a>const_pointer_cast  
 常量强制转换为 shared_ptr。  
  
```  
template <class Ty, class Other>  
shared_ptr<Ty>  
const_pointer_cast(const shared_ptr<Other>& sp);
```  
  
### <a name="parameters"></a>参数  
 `Ty`  
 由返回的共享指针控制的类型。  
  
 `Other`  
 由自变量共享指针控制的类型。  
  
 `Other`  
 自变量共享指针。  
  
### <a name="remarks"></a>备注  
 如果 `const_cast<Ty*>(sp.get())` 返回一个 null 指针，则模板函数将返回空 shared_ptr 对象；否则它将返回 [shared_ptr 类](../standard-library/shared-ptr-class.md)`<Ty>`对象，该对象具有由 `sp` 拥有的资源。 表达式 `const_cast<Ty*>(sp.get())` 必须有效。  
  
### <a name="example"></a>示例  
  
```cpp  
// std__memory__const_pointer_cast.cpp   
// compile with: /EHsc   
#include <memory>   
#include <iostream>   
  
int main()   
    {   
    std::shared_ptr<int> sp0(new int);   
    std::shared_ptr<const int> sp1 =   
        std::const_pointer_cast<const int>(sp0);   
  
 *sp0 = 3;   
    std::cout << "sp1 == " << *sp1 << std::endl;   
  
    return (0);   
    }  
  
```  
  
```Output  
sp1 == 3  
```  
  
##  <a name="a-namedeclarenopointersa--declarenopointers"></a><a name="declare_no_pointers"></a>declare_no_pointers  
 通知垃圾回收器：通过基地址指针和块大小而定义的内存块中的字符不包含可跟踪的指针。  
  
```  
void declare_no_pointers(
    char* ptr,   
    size_t _Size);
```  
  
### <a name="parameters"></a>参数  
  
|参数|说明|  
|---------------|-----------------|  
|` ptr`|第一个字符的地址，该字符不再包含可跟踪的指针。|  
|`_Size`|块的大小，该块以不包含可跟踪的指针的 ` ptr` 开始。|  
  
### <a name="remarks"></a>备注  
 该函数通知任何 `garbage collector`：地址 `[`` ptr``,` ` ptr` `+` `_Size``)` 的范围内不再包含可跟踪的指针。 （不得取消引用指向已分配存储的任何指针，除非使其 `reachable`。）  
  
##  <a name="a-namedeclarereachablea--declarereachable"></a><a name="declare_reachable"></a>declare_reachable  
 通知垃圾回收器：所指示的地址属于分配的存储并可到达。  
  
```  
void declare_reachable(void* ptr);
```  
  
### <a name="parameters"></a>参数  
 ` ptr`  
 指向可访问、已分配且有效的存储区域的指针。  
  
### <a name="remarks"></a>备注  
 如果 ` ptr` 不为 null，则该函数将通知任何垃圾回收器以后可访问 ` ptr`（指向有效的已分配存储）。  
  
##  <a name="a-namedefaultdeletea--defaultdelete"></a><a name="default_delete"></a>default_delete  
 删除使用 `operator new` 分配的对象。 适合与 `unique_ptr` 一起使用。  
```  
struct default_delete {
   constexpr default_delete() noexcept = default;
   template <class Other, class = typename enable_if<is_convertible<Other*, T*>::value, void>::type>>  
   default_delete(const default_delete<Other>&) noexcept;
   void operator()(T* Ptr) const noexcept;     };  
```
### <a name="parameters"></a>参数  
 `Ptr`  
 指向要删除的对象的指针。  
  
 其他  
 要删除的数组中的元素类型。  
  
### <a name="remarks"></a>备注  
 此模板类描述 `deleter`，它删除使用 `operator new` 分配的标量对象，适合与 `unique_ptr` 模板类一起使用。 它还具有显式专用化 `default_delete<Type[]>`。  
  
##  <a name="a-namedynamicpointercasta--dynamicpointercast"></a><a name="dynamic_pointer_cast"></a>dynamic_pointer_cast  
 动态强制转换为 shared_ptr。  
  
```  
template <class Ty, class Other>  
shared_ptr<Ty>  
dynamic_pointer_cast(const shared_ptr`<`Other>& sp);
```  
  
### <a name="parameters"></a>参数  
 `Ty`  
 由返回的共享指针控制的类型。  
  
 `Other`  
 由自变量共享指针控制的类型。  
  
 `sp`  
 自变量共享指针。  
  
### <a name="remarks"></a>备注  
 如果 `dynamic_cast<Ty*>(sp.get())` 返回一个 null 指针，则模板函数将返回空 shared_ptr 对象；否则它将返回 [shared_ptr 类](../standard-library/shared-ptr-class.md)`<Ty>`对象，该对象具有由 `sp` 拥有的资源。 表达式 `dynamic_cast<Ty*>(sp.get())` 必须有效。  
  
### <a name="example"></a>示例  
  
```cpp  
// std__memory__dynamic_pointer_cast.cpp   
// compile with: /EHsc   
#include <memory>   
#include <iostream>   
  
struct base   
    {   
    virtual ~base()   
        {   
        }   
  
    int val;   
    };   
  
struct derived   
    : public base   
    {   
    };   
  
int main()   
    {   
    std::shared_ptr<base> sp0(new derived);   
    std::shared_ptr<derived> sp1 =   
        std::dynamic_pointer_cast<derived>(sp0);   
  
    sp0->val = 3;   
    std::cout << "sp1->val == " << sp1->val << std::endl;   
  
    return (0);   
    }  
  
```  
  
```Output  
sp1->val == 3  
```  
  
##  <a name="a-namegetdeleterfunctiona--getdeleter-function"></a><a name="get_deleter_function"></a>get_deleter 函数  
 从 shared_ptr 获取删除器。  
  
```  
template <class D, class Ty>  
D *get_deleter(const shared_ptr<Ty>& sp);
```  
  
### <a name="parameters"></a>参数  
 `D`  
 删除器的类型。  
  
 `Ty`  
 由共享指针控制的类型。  
  
 `Other`  
 共享的指针。  
  
### <a name="remarks"></a>备注  
 该模板函数返回一个指向 `D` 类型的删除器的指针，该删除器属于 [shared_ptr 类](../standard-library/shared-ptr-class.md)对象 `sp`。 如果 `sp` 没有删除器，或如果其删除器的类型不是 `D`，则该函数将返回 0。  
  
### <a name="example"></a>示例  
  
```cpp  
// std__memory__get_deleter.cpp   
// compile with: /EHsc   
#include <memory>   
#include <iostream>   
  
struct base   
    {   
    int val;   
    };   
  
struct deleter   
    {   
    void operator()(base *p)   
        {   
        delete p;   
        }   
    };   
  
int main()   
    {   
    std::shared_ptr<base> sp0(new base);   
  
    sp0->val = 3;   
    std::cout << "get_deleter(sp0) != 0 == " << std::boolalpha   
        << (std::get_deleter<deleter>(sp0) != 0) << std::endl;   
  
    std::shared_ptr<base> sp1(new base, deleter());   
  
    sp0->val = 3;   
    std::cout << "get_deleter(sp1) != 0 == " << std::boolalpha   
        << (std::get_deleter<deleter>(sp1) != 0) << std::endl;   
  
    return (0);   
    }  
  
```  
  
```Output  
get_deleter(sp0) != 0 == false  
get_deleter(sp1) != 0 == true  
```  
  
##  <a name="a-namegetpointersafetya--getpointersafety"></a><a name="get_pointer_safety"></a>get_pointer_safety  
 返回任意垃圾回收器所采用的指针安全类型。  
  
```  
pointer_safety get_pointer_safety();
```  
  
### <a name="remarks"></a>备注  
 该函数返回任何自动 `garbage collector` 所采用的指针安全类型。  
  
##  <a name="a-namegettemporarybuffera--gettemporarybuffer"></a><a name="get_temporary_buffer"></a>get_temporary_buffer  
 为不超过指定元素数量的元素序列分配临时存储。  
  
```  
template <class Type>  
pair<Type *, ptrdiff_t> get_temporary_buffer(ptrdiff_t count);
```  
  
### <a name="parameters"></a>参数  
 ` count`  
 所请求的、要为其分配内存的元素的最大数目。  
  
### <a name="return-value"></a>返回值  
 一个 `pair`，其第一个组件是一个指向已分配内存的指针，其第二个组件提供缓冲区的大小，指示它可以存储的元素的最大数目。  
  
### <a name="remarks"></a>备注  
 该函数发出内存请求，该请求可能不会成功。 如果没有分配缓冲区，则该函数将返回一个 pair，其第二个组件等于零，第一个组件等于空指针。  
  
 此函数仅用于临时内存。  
  
### <a name="example"></a>示例  
  
```cpp  
// memory_get_temp_buf.cpp  
// compile with: /EHsc  
#include <memory>  
#include <iostream>  
  
using namespace std;  
  
int main( )  
{  
   // Create an array of ints  
   int intArray [ ] = { 10, 20, 30, 40, 100, 200, 300, 1000, 2000 };  
   int count = sizeof ( intArray ) / sizeof ( int );  
   cout << "The number of integers in the array is: "   
      << count << "." << endl;  
  
   pair<int *, ptrdiff_t> resultPair;  
   resultPair = get_temporary_buffer<int>( count );  
  
   cout << "The number of elements that the allocated memory\n"  
        << "could store is given by: resultPair.second = "   
        << resultPair.second << "." << endl;  
}  
```  
  
```Output  
The number of integers in the array is: 9.  
The number of elements that the allocated memory  
could store is given by: resultPair.second = 9.  
```  
  
##  <a name="a-namemakeshareda--makeshared"></a><a name="make_shared"></a>make_shared  
 创建并返回指向分配对象的 `shared_ptr`，这些对象是通过使用默认分配器从零个或多个参数构造的。 分配并构造指定类型的对象和`shared_ptr`来管理对象的共享所有权，并返回`shared_ptr`。  
  
```  
template <class Type, class... Types>  
shared_ptr<Type>  
make_shared(
    Types&&... _Args);
```  
  
### <a name="parameters"></a>参数  
  
|参数|描述|  
|---------------|-----------------|  
|`_Args`|零个或多个构造函数参数。 函数根据所提供的自变量来推断要调用的构造函数重载。|  
  
### <a name="remarks"></a>备注  
 使用`make_shared`作为创建对象的简单、更高效的方法，以及一个`shared_ptr`来同时管理对对象的共享访问。 在语义上，这两个语句是等效的：  
  
```cpp  
auto sp = std::shared_ptr<Example>(new Example(argument));
auto msp = std::make_shared<Example>(argument);
```  
  
 但是，第一条语句进行了两个分配，如果在`shared_ptr`对象的分配成功后，`Example`的分配失败，则未命名的`Example`对象将被泄漏。 使用`make_shared`的语句更简单，因为只涉及到一个函数调用。 这样会更有效，因为库可能会对对象和智能指针进行一个分配。 这样既更快，又产生较少内存碎片，并且除了另一个以外，这个资源分配不可能出现异常。 通过使引用对象和更新智能指针中的引用计数的代码具有的更好的地址来提高性能。  
  
 如果不需要共享访问对象，请考虑使用 [make_unique](../standard-library/memory-functions.md#make_unique)。 如果需要为对象指定自定义的分配器，请使用 [allocate_shared](../standard-library/memory-functions.md#allocate_shared)。 如果您的对象需要自定义删除器，您不能使用`make_shared`，因为无法将删除器作为参数传递。  
  
 以下示例演示如何通过调用特定构造函数重载来创建指向类型的共享指针。  
  
### <a name="example"></a>示例  
  
```cpp  
// stl_make_shared.cpp  
// Compile by using: cl /W4 /EHsc stl_make_shared.cpp  
#include <iostream>  
#include <string>  
#include <memory>  
#include <vector>  
  
class Song {  
public:  
   std::wstring title_;  
   std::wstring artist_;  
  
   Song(std::wstring title, std::wstring artist) : title_(title), artist_(artist) {}  
   Song(std::wstring title) : title_(title), artist_(L"Unknown") {}  
};  
  
void CreateSharedPointers() {  
   // Okay, but less efficient to have separate allocations for  
   // Song object and shared_ptr control block.    
   auto song = new Song(L"Ode to Joy", L"Beethoven");  
   std::shared_ptr<Song> sp0(song);  
  
   // Use make_shared function when possible. Memory for control block  
   // and Song object are allocated in the same call:    
   auto sp1 = std::make_shared<Song>(L"Yesterday", L"The Beatles");  
   auto sp2 = std::make_shared<Song>(L"Blackbird", L"The Beatles");  
  
   // make_shared infers which constructor to use based on the arguments.  
   auto sp3 = std::make_shared<Song>(L"Greensleeves");  
  
   // The playlist vector makes copies of the shared_ptr pointers.  
   std::vector<std::shared_ptr<Song>> playlist;  
   playlist.push_back(sp0);  
   playlist.push_back(sp1);  
   playlist.push_back(sp2);  
   playlist.push_back(sp3);  
   playlist.push_back(sp1);  
   playlist.push_back(sp2);  
   for (auto&& sp : playlist) {  
      std::wcout << L"Playing " << sp->title_ <<   
         L" by " << sp->artist_ << L", use count: " <<   
         sp.use_count() << std::endl;  
   }  
}  
  
int main() {  
   CreateSharedPointers();  
}  
```  
  
  此示例产生以下输出：  
  
```Output  
Playing Ode to Joy by Beethoven, use count: 2  
Playing Yesterday by The Beatles, use count: 3  
Playing Blackbird by The Beatles, use count: 3  
Playing Greensleeves by Unknown, use count: 2  
Playing Yesterday by The Beatles, use count: 3  
Playing Blackbird by The Beatles, use count: 3  
```  
  
##  <a name="a-namemakeuniquea--makeunique"></a><a name="make_unique"></a>make_unique  
 创建 [unique_ptr](../standard-library/unique-ptr-class.md) 并将其返回到指定类型的对象，该对象通过指定的自变量进行构建。  
  
```scr  
// make_unique<T>template <class T,   
    class... Types>  
unique_ptr<T> make_unique(Types&&... Args)  
 {  
    return (unique_ptr<T>(new T(forward<Types>(Args)...)));

 }  
// make_unique<T[]>  
template <class T>  
make_unique(size_t Size)   
 {   
    return (unique_ptr<T>(new Elem[Size]()));

 }  
 
// make_unique<T[N]> disallowed  
template <class T,   
    class... Types>  
typename enable_if<extent<T>::value != 0,   
    void>::type make_unique(Types&&...) = delete;  
```  
  
### <a name="parameters"></a>参数  
 `T`  
 `unique_ptr` 将指向的对象的类型。  
  
 `Types`  
 `Args` 指定的构造函数自变量的类型。  
  
 `Args`  
 要传递到 `T` 类型对象的构造函数的自变量。  
  
 `Elem`  
 类型 `T` 的元素的数组。  
  
 `Size`  
 新数组中要为其分配空间的元素的数目。  
  
### <a name="remarks"></a>备注  
 第一个重载用于单个对象，第二个重载针对数组进行调用，第三个重载防止用户指定类型参数中的数组大小 (make_unique\<T[N]>)；当前标准不支持此构造。 当使用 `make_unique` 将 `unique_ptr` 创建到数组时，必须分别初始化数组元素。 如果你正在考虑此重载，也许使用 [std::vector](../standard-library/vector-class.md) 会是更好的选择。  
  
 由于谨慎实现 `make_unique` 以获得异常安全，因此建议您使用 `make_unique` 而不是直接调用 `unique_ptr` 构造函数。  
  
### <a name="example"></a>示例  
  下面的示例说明如何使用 `make_unique`。 有关更多示例，请参阅[如何：创建和使用 unique_ptr 实例](../cpp/how-to-create-and-use-unique-ptr-instances.md)。  
  
 [!code-cpp[stl_smart_pointers#214](../cpp/codesnippet/CPP/memory-functions_1.cpp)]  
  
  如果您收到与 `unique_ptr` 有关的错误 C2280，则几乎可以肯定是因为您尝试调用其副本构造函数（此函数是一个已删除的函数）。  
  
##  <a name="a-nameownerlessa--ownerless"></a><a name="owner_less"></a>owner_less  
 允许对共享指针和弱指针进行基于所有权的混合比较。 如果成员函数 `owner_before` 将左侧参数排在右侧参数前面，则返回 `true`。  
  
```  
template <class Type>  
struct owner_less; // not defined  
 
template <class Type>  
struct owner_less<shared_ptr<Type>> {  
    bool operator()(
    const shared_ptr<Type>& left,  
    const shared_ptr<Type>& right);

    bool operator()(
    const shared_ptr<Type>& left,  
    const weak_ptr<Type>& right);

    bool operator()(
    const weak_ptr<Type>& left,  
    const shared_ptr<Type>& right);

};  
 
template <class Type>  
struct owner_less<weak_ptr<Type>>  
    bool operator()(
    const weak_ptr<Type>& left,  
    const weak_ptr<Type>& right);

    bool operator()(
    const weak_ptr<Type>& left,  
    const shared_ptr<Ty>& right);

    bool operator()(
    const shared_ptr<Type>& left,  
    const weak_ptr<Type>& right);

};  
```  
  
### <a name="parameters"></a>参数  
 `_left`  
 共享指针或弱指针。  
  
 ` right`  
 共享指针或弱指针。  
  
### <a name="remarks"></a>备注  
 该模板类将其所有成员运算符都定义为返回 ` left``.owner_before(`` right``)`。  
  
##  <a name="a-namereturntemporarybuffera--returntemporarybuffer"></a><a name="return_temporary_buffer"></a>return_temporary_buffer  
 对使用 `get_temporary_buffer` 模板函数分配的临时内存执行解除分配。  
  
```  
template <class Type>  
void return_temporary_buffer(Type* _Pbuf);
```  
  
### <a name="parameters"></a>参数  
 *_Pbuf*  
 指向要取消分配的内存的指针。  
  
### <a name="remarks"></a>备注  
 此函数仅用于临时内存。  
  
### <a name="example"></a>示例  
  
```cpp  
// memory_ret_temp_buf.cpp  
// compile with: /EHsc  
#include <memory>  
#include <iostream>  
  
using namespace std;  
  
int main( )  
{  
   // Create an array of ints  
   int intArray [ ] = { 10, 20, 30, 40, 100, 200, 300 };  
   int count = sizeof ( intArray ) / sizeof ( int );  
   cout << "The number of integers in the array is: "   
         << count << "." << endl;  
  
   pair<int *, ptrdiff_t> resultPair;  
   resultPair = get_temporary_buffer<int>( count );  
  
   cout << "The number of elements that the allocated memory\n"  
         << " could store is given by: resultPair.second = "   
         << resultPair.second << "." << endl;  
  
   int* tempBuffer = resultPair.first;  
  
   // Deallocates memory allocated with get_temporary_buffer  
   return_temporary_buffer ( tempBuffer );  
}  
```  
  
```Output  
The number of integers in the array is: 7.  
The number of elements that the allocated memory  
 could store is given by: resultPair.second = 7.  
```  
  
##  <a name="a-namestaticpointercasta--staticpointercast"></a><a name="static_pointer_cast"></a>static_pointer_cast  
 静态强制转换为 shared_ptr。  
  
```  
template <class Ty, class Other>  
shared_ptr<Ty>  
static_pointer_cast(const shared_ptr<Other>& sp);
```  
  
### <a name="parameters"></a>参数  
 `Ty`  
 由返回的共享指针控制的类型。  
  
 `Other`  
 由自变量共享指针控制的类型。  
  
 `Other`  
 自变量共享指针。  
  
### <a name="remarks"></a>备注  
 如果 `sp` 为空 `shared_ptr` 对象，则模板函数返回空 shared_ptr 对象；否则它将返回 [shared_ptr 类](../standard-library/shared-ptr-class.md)`<Ty>`对象，该对象具有由 `sp` 拥有的资源。 表达式 `static_cast<Ty*>(sp.get())` 必须有效。  
  
### <a name="example"></a>示例  
  
```cpp  
// std__memory__static_pointer_cast.cpp   
// compile with: /EHsc   
#include <memory>   
#include <iostream>   
  
struct base   
    {   
    int val;   
    };   
  
struct derived   
    : public base   
    {   
    };   
  
int main()   
    {   
    std::shared_ptr<base> sp0(new derived);   
    std::shared_ptr<derived> sp1 =   
        std::static_pointer_cast<derived>(sp0);   
  
    sp0->val = 3;   
    std::cout << "sp1->val == " << sp1->val << std::endl;   
  
    return (0);   
    }  
  
```  
  
```Output  
sp1->val == 3  
```  
  
##  <a name="a-nameswapa--swap-c-standard-library"></a><a name="swap"></a>swap（C++ 标准库）  
 交换两个 shared_ptr 或 weak_ptr 对象。  
  
```  
template <class Ty, class Other>  
void swap(shared_ptr<Ty>& left, shared_ptr<Other>& right);

template <class Ty, class Other>  
void swap(weak_ptr<Ty>& left, weak_ptr<Other>& right);
```  
  
### <a name="parameters"></a>参数  
 `Ty`  
 由左侧共享/弱指针控制的类型。  
  
 `Other`  
 由右侧共享/弱指针控制的类型。  
  
 `left`  
 左侧共享/弱指针。  
  
 `right`  
 右侧共享/弱指针。  
  
### <a name="remarks"></a>备注  
 模板函数调用 `left.swap(right)`。  
  
### <a name="example"></a>示例  
  
```cpp  
// std__memory__swap.cpp   
// compile with: /EHsc   
#include <memory>   
#include <iostream>   
  
struct deleter
{
    void operator()(int *p)
    {
        delete p;
    }
};

int main()
{
    std::shared_ptr<int> sp1(new int(5));
    std::shared_ptr<int> sp2(new int(10));
    std::cout << "*sp1 == " << *sp1 << std::endl;

    sp1.swap(sp2);
    std::cout << "*sp1 == " << *sp1 << std::endl;

    swap(sp1, sp2);
    std::cout << "*sp1 == " << *sp1 << std::endl;
    std::cout << std::endl;

    std::weak_ptr<int> wp1(sp1);
    std::weak_ptr<int> wp2(sp2);
    std::cout << "*wp1 == " << *wp1.lock() << std::endl;

    wp1.swap(wp2);
    std::cout << "*wp1 == " << *wp1.lock() << std::endl;

    swap(wp1, wp2);
    std::cout << "*wp1 == " << *wp1.lock() << std::endl;

    return (0);
}

```  
  
```Output  
*sp1 == 5  
*sp1 == 10  
*sp1 == 5  
  
*wp1 == 5  
*wp1 == 10  
*wp1 == 5  
```  
  
##  <a name="a-nameundeclarenopointersa--undeclarenopointers"></a><a name="undeclare_no_pointers"></a>undeclare_no_pointers  
 通知垃圾回收器：通过基地址指针和块大小而定义的内存块中的字符现在可包含可跟踪的指针。  
  
```  
void undeclare_no_pointers(
    char* ptr,   
    size_t _Size);
```  
  
### <a name="remarks"></a>备注  
 该函数通知任何 `garbage collector`：地址 `[`` ptr``,` ` ptr` `+` `_Size``)` 的范围内现在可能包含 `traceable pointers`。  
  
##  <a name="a-nameundeclarereachablea--undeclarereachable"></a><a name="undeclare_reachable"></a>undeclare_reachable  
 通知 `garbage_collector`：指定的内存位置无法达到。  
  
```  
template <class Type>  
Type *undeclare_reachable(Type* ptr);
```  
  
### <a name="parameters"></a>参数  
  
|参数|描述|  
|---------------|-----------------|  
|` ptr`|指向要声明为不可访问的内存地址的指针。|  
  
### <a name="remarks"></a>备注  
 如果 ` ptr` 不为 `null`，则该函数将通知任何 `garbage collector` ` ptr` 以后不 `reachable`。 它将返回等同于 ` ptr` 的 `safely derived` 指针。  
  
##  <a name="a-nameuninitializedcopya--uninitializedcopy"></a><a name="uninitialized_copy"></a>uninitialized_copy  
 将指定源范围中的对象复制到未初始化的目标范围。  
  
```  
template <class InputIterator, class ForwardIterator>  
ForwardIterator uninitialized_copy(InputIterator first, InputIterator last, ForwardIterator dest);
```  
  
### <a name="parameters"></a>参数  
 ` first`  
 确定源范围中第一个元素的地址的输入迭代器。  
  
 ` last`  
 确定源范围中最后一个元素的地址的输入迭代器。  
  
 ` dest`  
 确定目标范围中第一个元素的地址的前向迭代器。  
  
### <a name="return-value"></a>返回值  
 确定超出目标范围的第一个位置的地址的前向迭代器，除非源范围为空，此时迭代器将确定 * first* 的地址。  
  
### <a name="remarks"></a>备注  
 该算法可将内存分配与对象构造分离开。  
  
 该模板函数有效执行以下操作：  
  
```  
while (first!= last)  
    new ((void*)&* dest ++)  
    iterator_traits<InputIterator>::value_type (* first ++);

return first;  
```  
  
 除非代码引发异常。 在这种情况下，所有构造的对象将销毁，并重新引发异常。  
  
### <a name="example"></a>示例  
  
```cpp  
// memory_uninit_copy.cpp  
// compile with: /EHsc /W3  
#include <memory>  
#include <iostream>  
  
using namespace std;  
  
class Integer
{
public:
    Integer(int x) : val(x) {}
    int get() { return val; }
private:
    int val;
};

int main()
{
    int Array[] = { 10, 20, 30, 40 };
    const int N = sizeof(Array) / sizeof(int);

    int i;
    cout << "The initialized Array contains " << N << " elements: ";
    for (i = 0; i < N; i++)
    {
        cout << " " << Array[i];
    }
    cout << endl;

    Integer* ArrayPtr = (Integer*)malloc(N * sizeof(int));
    Integer* LArrayPtr = uninitialized_copy(
        Array, Array + N, ArrayPtr);  // C4996  

    cout << "Address of position after the last element in the array is: "
        << &Array[0] + N << endl;
    cout << "The iterator returned by uninitialized_copy addresses: "
        << (void*)LArrayPtr << endl;
    cout << "The address just beyond the last copied element is: "
        << (void*)(ArrayPtr + N) << endl;

    if ((&Array[0] + N) == (void*)LArrayPtr)
        cout << "The return value is an iterator "
        << "pointing just beyond the original array." << endl;
    else
        cout << "The return value is an iterator "
        << "not pointing just beyond the original array." << endl;

    if ((void*)LArrayPtr == (void*)(ArrayPtr + N))
        cout << "The return value is an iterator "
        << "pointing just beyond the copied array." << endl;
    else
        cout << "The return value is an iterator "
        << "not pointing just beyond the copied array." << endl;

    free(ArrayPtr);

    cout << "Note that the exact addresses returned will vary\n"
        << "with the memory allocation in individual computers."
        << endl;
}
```  
  
##  <a name="a-nameuninitializedcopyna--uninitializedcopyn"></a><a name="uninitialized_copy_n"></a>uninitialized_copy_n  
 创建来自输入迭代器的指定数量的元素的副本。 副本放置在向前迭代器中。  
  
```  
template <class InputIterator, class Size, class ForwardIterator>  
ForwardIterator uninitialized_copy_n(
    InputIterator first,   
    Size count,  
    ForwardIterator dest);
```  
  
### <a name="parameters"></a>参数  
 ` first`  
 引用要复制的对象的输入迭代器。  
  
 ` count`  
 指定复制对象的次数的带符号或无符号整数类型。  
  
 ` dest`  
 引用新副本所在位置的向前迭代器。  
  
### <a name="return-value"></a>返回值  
 发现超出目标的第一个位置的向前迭代器。 如果源范围为空，迭代器将发现 ` first`*。*  
  
### <a name="remarks"></a>备注  
 模板函数有效执行以下操作：  
  
 `for (; 0 < count; -- count)`  
  
 `new ((void *)&*` ` dest` `++)`  
  
 `iterator_traits<InputIterator>::value_type(*` ` first` `++);`  
  
 `return dest;`  
  
 除非代码引发异常。 在这种情况下，所有构造的对象将销毁，并重新引发异常。  
  
##  <a name="a-nameuninitializedfilla--uninitializedfill"></a><a name="uninitialized_fill"></a>uninitialized_fill  
 将具有指定值的对象复制到未初始化的目标范围。  
  
```  
template <class ForwardIterator, class Type>  
void uninitialized_fill(ForwardIterator first, ForwardIterator last, const Type& val);
```  
  
### <a name="parameters"></a>参数  
 ` first`  
 一个向前迭代器，用于在要启动的目标范围中发现第一个元素。  
  
 ` last`  
 一个向前迭代器，用于在要启动的目标范围中发现最后一个元素。  
  
 ` val`  
 用于初始化目标范围的值。  
  
### <a name="remarks"></a>备注  
 该算法可将内存分配与对象构造分离开。  
  
 该模板函数有效执行以下操作：  
  
```  
while (first != last)  
    new ((void*)&* first ++)  
    iterator_traits<ForwardIterator>::value_type (_Val);
```  
  
 除非代码引发异常。 在这种情况下，所有构造的对象将销毁，并重新引发异常。  
  
### <a name="example"></a>示例  
  
```cpp  
// memory_uninit_fill.cpp  
// compile with: /EHsc  
#include <memory>  
#include <iostream>  
  
using namespace std;  
  
   class Integer {         // No default constructor  
   public:  
      Integer( int x ) : val( x ) {}  
      int get( ) { return val; }  
   private:  
      int val;  
   };  
  
int main( )  
{  
   const int N = 10;  
   Integer val ( 25 );  
   Integer* Array = ( Integer* ) malloc( N * sizeof( int ) );  
   uninitialized_fill( Array, Array + N, val );  
   int i;  
   cout << "The initialized Array contains: ";  
      for ( i = 0 ; i < N; i++ )  
      {  
         cout << Array [ i ].get( ) << " ";  
      }  
   cout << endl;  
}  
```  
  
```Output  
The initialized Array contains: 25 25 25 25 25 25 25 25 25 25   
```  
  
##  <a name="a-nameuninitializedfillna--uninitializedfilln"></a><a name="uninitialized_fill_n"></a>uninitialized_fill_n  
 将具有指定值的对象复制到未初始化的目标范围内的指定数量的元素。  
  
```  
template <class FwdIt, class Size, class Type>  
void uninitialized_fill_n(ForwardIterator first, Size count, const Type& val);
```  
  
### <a name="parameters"></a>参数  
 ` first`  
 在要初始化的目标范围中发现第一个元素的向前迭代器。  
  
 ` count`  
 要初始化的元素的个数。  
  
 ` val`  
 用于初始化目标范围的值。  
  
### <a name="remarks"></a>备注  
 该算法可将内存分配与对象构造分离开。  
  
 该模板函数有效执行以下操作：  
  
```cpp  
while (0 <count--)  
    new ((void*)&* first ++)  
    iterator_traits<ForwardIterator>::value_type(val);
```  
  
 除非代码引发异常。 在这种情况下，所有构造的对象将销毁，并重新引发异常。  
  
### <a name="example"></a>示例  
  
```cpp  
// memory_uninit_fill_n.cpp  
// compile with: /EHsc /W3  
#include <memory>  
#include <iostream>  
  
using namespace std;  
  
class Integer {   // No default constructor  
public:  
   Integer( int x ) : val( x ) {}  
   int get( ) { return val; }  
private:  
   int val;  
};  
  
int main() {  
   const int N = 10;  
   Integer val ( 60 );  
   Integer* Array = ( Integer* ) malloc( N * sizeof( int ) );  
   uninitialized_fill_n( Array, N, val );  // C4996  
   int i;  
   cout << "The uninitialized Array contains: ";  
   for ( i = 0 ; i < N; i++ )  
      cout << Array [ i ].get( ) <<  " ";  
}  
```  
  
## <a name="see-also"></a>另请参阅  
 [\<memory>](../standard-library/memory.md)
