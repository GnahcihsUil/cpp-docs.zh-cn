---
title: "&lt;filesystem&gt; 函数 | Microsoft 文档"
ms.custom: 
ms.date: 11/04/2016
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-cpp
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- FILESYSTEM/std::experimental::filesystem::absolute
- std::experimental::filesystem::absolute
- FILESYSTEM/std::experimental::filesystem::canonical
- std::experimental::filesystem::canonical
- FILESYSTEM/std::experimental::filesystem::copy
- std::experimental::filesystem::copy
- FILESYSTEM/std::experimental::filesystem::copy_file
- std::experimental::filesystem::copy_file
- FILESYSTEM/std::experimental::filesystem::copy_symlink
- std::experimental::filesystem::copy_symlink
- FILESYSTEM/std::experimental::filesystem::create_directories
- std::experimental::filesystem::create_directories
- FILESYSTEM/std::experimental::filesystem::create_directory
- std::experimental::filesystem::create_directory
- FILESYSTEM/std::experimental::filesystem::create_directory_symlink
- std::experimental::filesystem::create_directory_symlink
- FILESYSTEM/std::experimental::filesystem::create_hard_link
- std::experimental::filesystem::create_hard_link
- FILESYSTEM/std::experimental::filesystem::create_symlink
- std::experimental::filesystem::create_symlink
- FILESYSTEM/std::experimental::filesystem::current_path
- std::experimental::filesystem::current_path
- FILESYSTEM/std::experimental::filesystem::equivalent
- std::experimental::filesystem::equivalent
- FILESYSTEM/std::experimental::filesystem::exists
- std::experimental::filesystem::exists
- FILESYSTEM/std::experimental::filesystem::file_size
- std::experimental::filesystem::file_size
- FILESYSTEM/std::experimental::filesystem::hard_link_count
- std::experimental::filesystem::hard_link_count
- FILESYSTEM/std::experimental::filesystem::hash_value
- std::experimental::filesystem::hash_value
- FILESYSTEM/std::experimental::filesystem::is_block_file
- std::experimental::filesystem::is_block_file
- FILESYSTEM/std::experimental::filesystem::is_character_file
- std::experimental::filesystem::is_character_file
- FILESYSTEM/std::experimental::filesystem::is_directory
- std::experimental::filesystem::is_directory
- FILESYSTEM/std::experimental::filesystem::is_empty
- std::experimental::filesystem::is_empty
- FILESYSTEM/std::experimental::filesystem::is_fifo
- std::experimental::filesystem::is_fifo
- FILESYSTEM/std::experimental::filesystem::is_other
- std::experimental::filesystem::is_other
- FILESYSTEM/std::experimental::filesystem::is_regular_file
- std::experimental::filesystem::is_regular_file
- FILESYSTEM/std::experimental::filesystem::is_socket
- std::experimental::filesystem::is_socket
- FILESYSTEM/std::experimental::filesystem::is_symlink
- std::experimental::filesystem::is_symlink
- FILESYSTEM/std::experimental::filesystem::last_write_time
- std::experimental::filesystem::last_write_time
- FILESYSTEM/std::experimental::filesystem::permissions
- std::experimental::filesystem::permissions
- FILESYSTEM/std::experimental::filesystem::read_symlink
- std::experimental::filesystem::read_symlink
- FILESYSTEM/std::experimental::filesystem::remove
- std::experimental::filesystem::remove
- FILESYSTEM/std::experimental::filesystem::remove_all
- std::experimental::filesystem::remove_all
- FILESYSTEM/std::experimental::filesystem::rename
- std::experimental::filesystem::rename
- FILESYSTEM/std::experimental::filesystem::resize_file
- std::experimental::filesystem::resize_file
- FILESYSTEM/std::experimental::filesystem::space
- std::experimental::filesystem::space
- FILESYSTEM/std::experimental::filesystem::status
- std::experimental::filesystem::status
- FILESYSTEM/std::experimental::filesystem::status_known
- std::experimental::filesystem::status_known
- FILESYSTEM/std::experimental::filesystem::swap
- std::experimental::filesystem::swap
- FILESYSTEM/std::experimental::filesystem::symlink_status
- std::experimental::filesystem::symlink_status
- FILESYSTEM/std::experimental::filesystem::system_complete
- std::experimental::filesystem::system_complete
- FILESYSTEM/std::experimental::filesystem::temp_directory_path
- std::experimental::filesystem::temp_directory_path
- FILESYSTEM/std::experimental::filesystem::u8path
- std::experimental::filesystem::u8path
dev_langs:
- C++
ms.assetid: be3cb821-4728-4d47-ab78-858fa8aa5045
caps.latest.revision: 13
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
ms.sourcegitcommit: 31a7a65ed759ec552e11f2eccc5d425c2b2b765d
ms.openlocfilehash: 253af6748b2d46ee1421604ed6f16fd97bf5a459
ms.lasthandoff: 02/24/2017

---
# <a name="ltfilesystemgt-functions"></a>&lt;filesystem&gt; 函数
[\<filesystem>](../standard-library/filesystem.md) 标头中的这些自由格式函数对路径、文件、符号链接、目录和卷执行修改和查询操作。 有关详细信息和代码示例，请参阅[文件系统导航 (C++)](../standard-library/file-system-navigation.md)。  
||||  
|-|-|-|  
|[absolute](#absolute)|[begin](#begin)|[canonical](#canonical)|
|[copy](#copy)|[copy_file](#copy_file)|[copy_symlink](#copy_symlink)|
|[create_directories](#create_directories)|[create_directory](#create_directory)|[create_directory_symlink](#create_directory_symlink)|
|[create_hard_link](#create_hard_link)|[create_symlink](#create_symlink)|[current_path](#current_path)|
|[end](#end)|[equivalent](#equivalent)|[exists](#exists)|
|[file_size](#file_size)|[hard_link_count](#hard_link_count)|[hash_value](#hash_value)|
|[is_block_file](#is_block_file)|[is_character_file](#is_character_file)|[is_directory](#is_directory)|
|[is_empty](#is_empty)|[is_fifo](#is_fifo)|[is_other](#is_other)|
|[is_regular_file](#is_regular_file)|[is_socket](#is_socket)|[is_symlink](#is_symlink)|
|[last_write_time](#last_write_time)|[permissions](#permissions)|[read_symlink](#read_symlink)|
|[remove](#remove)|[remove_all](#remove_all)|[rename](#rename)|
|[resize_file](#resize_file)|[space](#space)|[status](#status)|
|[status_known](#status_known)|[swap](#swap)|[symlink_status](#symlink_status)|
|[system_complete](#system_complete)|[temp_directory_path](#temp_directory_path)|[u8path](#u8path)|  


## <a name="a-namea--a-nameabsolutea-absolute"></a><a name=""></a>  <a name="absolute"></a> absolute  
  
```  
path absolute(const path& pval, const path& base = current_path());
```  
  
 该函数返回与 `pval` 对应的绝对路径名（相对于路径名 `base`）：  
  
1.  如果 pval.has_root_name() && pval.has_root_directory()，则该函数返回 pval。  
  
2.  如果 pval.has_root_name() && !pval.has_root_directory()，则该函数返回 pval.root_name() / absolute(base).root_directory() / absolute(base).relative_path() / pval.relative_path()。  
  
3.  如果 !pval.has_root_name() && pval.has_root_directory()，则该函数返回 absolute(base).root_name() / pval。  
  
4.  如果 !pval.has_root_name() && !pval.has_root_directory()，则该函数返回 absolute(base) / pval。  
  
## <a name="a-namebegina--begin"></a><a name="begin"></a>  begin  
  
```  
const directory_iterator& begin(const directory_iterator& iter) noexcept;  
const recursive_directory_iterator& 
    begin(const recursive_directory_iterator& iter) noexcept;  
```  
  
 两个函数均返回 `iter`。  
  
## <a name="a-namecanonicala--canonical"></a><a name="canonical"></a>  canonical  
  
```  
path canonical(const path& pval, const path& base = current_path());
path canonical(const path& pval, error_code& ec);
path canonical(const path& pval, const path& base, error_code& ec);
```  
  
 这些函数均形成绝对路径名 pabs = absolute(pval, base)（或 pab = 不使用任何基本参数的重载的 absolute(pval)），然后按顺序执行以下步骤，将其简化为规范格式：  
  
1.  is_symlink(X) 为 true 的每个路径组件 X 都替换为 read_symlink(X)。  
  
2.  删除每个路径组件 . （圆点是由以前的路径组件建立的当前目录）。  
  
3.  删除每对路径组件 X/.. （双园点是由以前的路径组件建立的父目录）。  
  
 然后，该函数返回 pabs。  
  
## <a name="a-namecopya--copy"></a><a name="copy"></a>  copy  
  
```  
void copy(const path& from, const path& to);
void copy(const path& from, const path& to, error_code& ec) noexcept;  
void copy(const path& from, const path& to, copy_options opts);
void copy(const path& from, const path& to, copy_options opts, error_code& ec) noexcept;  
```  
  
 这些函数都可能在 `opts` 参数的控制下将 `from` 处的一个或多个文件复制或链接到 `to`，对于没有 `opts` 参数的重载，该参数被视为 copy_options::none。 `opts` 应最多包含一个以下项：  
  
-   skip_existing、overwrite_existing 或 update_existing  
  
-   copy_symlinks 或 skip_symlinks  
  
-   directories_only、create_symlinks 或 create_hard_links  
  
 函数首先确定 file_status 值 f（表示 `from`）和 t（表示 `to`）：  
  
-   如果 opts & (copy_options::create_symlinks &#124; copy_options::skip_symlinks)，则通过调用 symlink_status  
  
-   否则，通过调用状态  
  
-   否则报告错误。  
  
 如果 !exists(f) &#124;&#124; equivalent(f, t) &#124;&#124; is_other(f) &#124;&#124; is_other(t) &#124;&#124; is_directory(f)&& is_regular_file(t)，则这些函数随后报告错误（不执行任何其他操作）。  
  
 否则，如果 is_symlink(f)，则：  
  
-   如果 options & copy_options::skip_symlinks，则不执行任何操作。  
  
-   否则，如果 !exists(t)&& options & copy_options::copy_symlinks ，则 copy_symlink(from, to, opts)。  
  
-   否则报告错误。  
  
 否则，如果 is_regular_file(f)，则：  
  
-   如果 opts & copy_options::directories_only，则不执行任何操作。  
  
-   否则，如果 opts & copy_options::create_symlinks，则 create_symlink(to, from)。  
  
-   否则，如果 opts & copy_options::create_hard_links，则 create_hard_link(to, from)。  
  
-   否则，如果 is_directory(f)，则 copy_file(from, to / from.filename(), opts)。  
  
-   否则，copy_file(from, to, opts)。  
  
 否则，如果 is_directory(f) && (opts & copy_options::recursive &#124;&#124; !opts)，则：  
  
```cpp  
if (!exists(t))
{  // copy directory contents recursively  
    create_directory(to, from, ec);

    for (directory_iterator next(from), end; ec == error_code() && next != end; ++next)
    {
        copy(next->path(), to / next->path().filename(), opts, ec);
    }

}
```  
  
 否则，不执行任何操作。  
  
## <a name="a-nameopyfilea--copyfile"></a><a name="opy_file"></a>  copy_file  
  
```  
bool copy_file(const path& from, const path& to);
bool copy_file(const path& from, const path& to, error_code& ec) noexcept;  
bool copy_file(const path& from, const path& to, copy_options opts);
bool copy_file(const path& from, const path& to, copy_options opts, error_code& ec) noexcept;  
```  
  
 这些函数都可能在 `opts` 参数的控制下将 `from` 处的文件复制到 `to`，对于没有 `opts` 参数的重载，该参数被视为 copy_options::none。 `opts` 应最多包含 skip_existing、overwrite_existing 或 update_existing 的其中一项。  
  
 如果 exists\(to\) && \!\(opts & \(copy_options::skip_existing &#124; copy_options::overwrite_existing &#124; copy_options::update_existing\)\)，则报告错误，表示该文件已存在。  
  
 否则，如果 \!exists\(to\) &#124;&#124; opts & copy_options::overwrite_existing &#124;&#124; opts & copy_options::update_existing&& last_write_time\(to\) \< last_write_time\(from\) &#124;&#124; \!\(opts & \(copy_options::skip_existing &#124; copy_options::overwrite_existing &#124; copy_options:update_existing\)\)，则尝试将 from 文件的内容和特性复制到 to 文件。 如果复制尝试失败，则报告错误。  
  
 如果尝试复制并成功，则函数返回 true，否则返回 false。  
  
## <a name="a-namecopysymlink-a--copysymlink"></a><a name="copy_symlink "></a>  copy_symlink  
  
```  
void copy_symlink(const path& from, const path& to);
void copy_symlink(const path& from, const path& to, error_code& ec) noexcept;  
```  
  
 如果 is_directory\(from\)，则函数调用 create_directory_symlink\(from, to\)。 否则，它会调用 create_symlink\(from, to\)。  
  
## <a name="a-namecreatedirectoriesa--createdirectories"></a><a name="create_directories"></a>  create_directories  
  
```  
bool create_directories(const path& pval);
bool create_directories(const path& pval, error_code& ec) noexcept;  
```  
  
 对于如 a\/b\/c 这样的路径名，函数根据需要创建目录 a 和 a\/b，以便它可以根据需要创建目录 a\/b\/c。 仅当它实际创建目录 `pval` 时，才返回 true。  
  
## <a name="a-namecreatedirectorya--createdirectory"></a><a name="create_directory"></a>  create_directory  
  
```  
bool create_directory(const path& pval);

bool create_directory(const path& pval, error_code& ec) noexcept;  
bool create_directory(const path& pval, const path& attr);
bool create_directory(const path& pval, const path& attr, error_code& ec) noexcept;  
```  
  
 该函数将根据需要创建目录 `pval`。 仅当它实际创建目录 `pval` 时，才返回 true，在这种情况下，它将从现有的文件 `attr` 复制权限，或对没有 `attr` 参数的重载使用 perms::all。  
  
## <a name="a-namecreatedirectorysymlink-a--createdirectorysymlink"></a><a name="create_directory_symlink "></a>  create_directory_symlink  
  
```  
void create_directory_symlink(const path& to, const path& link);
void create_directory_symlink(const path& to, const path& link, error_code& ec) noexcept;  
```  
  
 该函数将链接创建为指向目录 `to` 的符号链接。  
  
## <a name="a-namecreatehardlinka--createhardlink"></a><a name="create_hard_link"></a>  create_hard_link  
  
```  
void create_hard_link(const path& to,  const path& link);
void create_hard_link(const path& to, const path& link, error_code& ec) noexcept;  
```  
  
 该函数将链接创建为指向目录或文件 `to` 的硬链接。  
  
## <a name="a-namecreatesymlink-a--createsymlink"></a><a name="create_symlink "></a>  create_symlink  
  
```  
void create_symlink(const path& to,  const path& link);

void create_symlink(const path& to, const path& link, error_code& ec) noexcept;  
```  
  
 该函数将 `link` 创建为指向文件 `to` 的符号链接。  
  
## <a name="a-namecurrentpatha--currentpath"></a><a name="current_path"></a>  current_path  
  
```  
path current_path();
path current_path(error_code& ec);
void current_path(const path& pval);
void current_path(const path& pval, error_code& ec) noexcept;  
```  
  
 没有 `pval` 参数的函数将返回当前目录的路径名。 剩余的函数将当前目录设置为 `pval`。  
  
## <a name="a-nameenda--end"></a><a name="end"></a>  end  
  
```  
directory_iterator& end(const directory_iterator& iter) noexcept;  
recursive_directory_iterator& end(const recursive_directory_iterator& iter) noexcept;  
```  
  
 第一个函数返回 directory_iterator\(\)，第二个函数返回 recursive_directory_iterator\(\)  
  
## <a name="a-nameequivalenta--equivalent"></a><a name="equivalent"></a>  equivalent  
  
```  
bool equivalent(const path& left, const path& right);
bool equivalent(const path& left, const path& right, error_code& ec) noexcept;  
```  
  
 仅当 `left` 和`right` 指定相同的文件系统实体时，这些函数才返回 true。  
  
## <a name="a-nameexistsa--exists"></a><a name="exists"></a>  exists  
  
```  
bool exists(file_status stat) noexcept;  
bool exists(const path& pval);
bool exists(const path& pval, error_code& ec) noexcept;  
```  
  
 第一个函数返回 status_known && stat.type\(\) \!\= file_not_found。 第二个和第三个函数返回 exists\(status\(pval\)\)。  
  
## <a name="a-namefilesizea--filesize"></a><a name="file_size"></a>  file_size  
  
```  
uintmax_t file_size(const path& pval);
uintmax_t file_size(const path& pval, error_code& ec) noexcept;  
```  
  
 这些函数返回 `pval` 指定的文件的大小（以字节为单位），如果 exists\(pval\) && is_regular_file\(pval\)，则可以确定文件大小。 否则将报告错误，并返回 uintmax_t\(\-1\)。  
  
## <a name="a-namehardlinkcounta--hardlinkcount"></a><a name="hard_link_count"></a>  hard_link_count  
  
```  
uintmax_t hard_link_count(const path& pval);
uintmax_t hard_link_count(const path& pval, error_code& ec) noexcept;  
```  
  
 这些函数返回 `pval` 的硬链接数，如果出错，则返回 \-1。  
  
## <a name="a-namehashvaluea--hashvalue"></a><a name="hash_value"></a>  hash_value  
  
```  
size_t hash_value(const path& pval) noexcept;  
```  
  
 该函数返回 pval.native\(\) 的哈希值。  
  
## <a name="a-nameisblockfilea--isblockfile"></a><a name="is_block_file"></a>  is_block_file  
  
```  
bool is_block_file(file_status stat) noexcept;  
bool is_block_file(const path& pval);
bool is_block_file(const path& pval, error_code& ec) noexcept;  
```  
  
 第一个函数返回 stat.type\(\) \=\= file_type::block。 其余函数返回 is_block_file\(status\(pval\)\)。  
  
## <a name="a-nameischaracterfilea--ischaracterfile"></a><a name="is_character_file"></a>  is_character_file  
  
```   
bool is_character_file(file_status stat) noexcept;  
bool is_character_file(const path& pval);
bool is_character_file(const path& pval, error_code& ec) noexcept;  
```  
  
 第一个函数返回 stat.type\(\) \=\= file_type::character。 其余函数返回 is_character_file\(status\(pval\)\)。  
  
## <a name="a-nameisdirectory-a--isdirectory"></a><a name="is_directory "></a>  is_directory  
  
```   
bool is_directory(file_status stat) noexcept;  
bool is_directory(const path& pval);
bool is_directory(const path& pval, error_code& ec) noexcept;  
```  
  
 第一个函数返回 stat.type\(\) \=\= file_type::directory。 其余函数返回 is_directory_file\(status\(pval\)\)。  
  
## <a name="a-nameisemptya--isempty"></a><a name="is_empty"></a>  is_empty  
  
```   
bool is_empty(file_status stat) noexcept;  
bool is_empty(const path& pval);
bool is_empty(const path& pval, error_code& ec) noexcept;  
```  
  
 如果 is_directory\(pval\)，则函数返回 directory_iterator\(pval\) \=\= directory_iterator\(\)；否则返回 file_size\(pval\) \=\= 0。  
  
## <a name="a-nameisfifoa--isfifo"></a><a name="is_fifo"></a>  is_fifo  
  
```  
bool is_fifo(file_status stat) noexcept;  
bool is_fifo(const path& pval);
bool is_fifo(const path& pval, error_code& ec) noexcept;  
```  
  
 第一个函数返回 stat.type\(\) \=\= file_type::fifo。 其余函数返回 is_fifo\(status\(pval\)\)。  
  
## <a name="a-nameisothera--isother"></a><a name="is_other"></a>  is_other  
  
```  
bool is_other(file_status stat) noexcept;  
bool is_other(const path& pval);
bool is_other(const path& pval, error_code& ec) noexcept;  
```  
  
 第一个函数返回 stat.type\(\) \=\= file_type::other。 其余函数返回 is_other\(status\(pval\)\)。  
  
## <a name="a-namesregularfilea--isregularfile"></a><a name="s_regular_file"></a>  is_regular_file  
  
```   
bool is_regular_file(file_status stat) noexcept;  
bool is_regular_file(const path& pval);
bool is_regular_file(const path& pval, error_code& ec) noexcept;  
```  
  
 第一个函数返回 stat.type\(\) \=\= file_type::regular。 其余函数返回 is_regular_file\(status\(pval\)\)。  
  
## <a name="a-nameissocketa--issocket"></a><a name="is_socket"></a>  is_socket  
  
```   
bool is_socket(file_status stat) noexcept;  
bool is_socket(const path& pval);
bool is_socket(const path& pval, error_code& ec) noexcept;  
```  
  
 第一个函数返回 stat.type\(\) \=\= file_type::socket。 其余函数返回 is_socket\(status\(pval\)\)。  
  
## <a name="a-nameissymlinka--issymlink"></a><a name="is_symlink"></a>  is_symlink  
  
```   
bool is_symlink(file_status stat) noexcept;  
bool is_symlink(const path& pval);
bool is_symlink(const path& pval, error_code& ec) noexcept;  
```  
  
 第一个函数返回 stat.type\(\) \=\= file_type::symlink。 其余函数返回 is_symlink\(status\(pval\)\)。  
  
## <a name="a-namelastwritetimea--lastwritetime"></a><a name="last_write_time"></a>  last_write_time  
  
```   
file_time_type last_write_time(const path& pval);
file_time_type last_write_time(const path& pval, error_code& ec) noexcept;  
void last_write_time(const path& pval, file_time_type new_time);
void last_write_time(const path& pval, file_time_type new_time, error_code& ec) noexcept;  
```  
  
 前两个函数返回 `pval` 的上次数据修改时间，或如果出错，则返回 file_time_type\(\-1\)。 最后两个函数将 `pval` 的上次数据修改时间设置为 new_time。  
  
## <a name="a-namepermissionsa--permissions"></a><a name="permissions"></a>  permissions  
  
```  
void permissions(const path& pval, perms mask);
void permissions(const path& pval, perms mask, error_code& ec) noexcept;  
```  
  
 这些函数将 `pval` 指定的路径名的权限设置为 mask & perms::mask under control of perms & \(perms::add_perms &#124; perms::remove_perms\)。 mask 最多只应包含 perms::add_perms 和 perms::remove_perms 之一。  
  
 如果 mask & perms::add_perms，则函数将权限设置为 status\(pval\).permissions\(\) &#124; mask & perms::mask。 否则，如果 mask & perms::remove_perms，则函数将权限设置为 status\(pval\).permissions\(\) & ~\(mask & perms::mask\)。 否则，这些函数将权限设置为 mask & perms::mask。  
  
## <a name="a-namereadsymlinka--readsymlink"></a><a name="read_symlink"></a>  read_symlink  
  
```  
path read_symlink(const path& pval);
path read_symlink(const path& pval, error_code& ec);
```  
  
 如果 \!is_symlink\(pval\)，则这些函数报告错误并返回 path\(\)。 否则，函数返回包含符号链接的 `path` 类型的对象。  
  
## <a name="a-nameremovea--remove"></a><a name="remove"></a>  remove  
  
```  
bool remove(const path& pval);
bool remove(const path& pval, error_code& ec) noexcept;  
```  
  
 仅当 exists\(symlink_status\(pval\)\) 并成功删除文件时，这些函数才返回 true。 符号链接自行删除，无需它指定的文件。  
  
## <a name="a-nameremovealla--removeall"></a><a name="remove_all"></a>  remove_all  
  
```  
uintmax_t remove_all(const path& pval);
uintmax_t remove_all(const path& pval, error_code& ec) noexcept;  
```  
  
 如果 `pval` 是一个目录，则这些函数以递归方式删除所有目录项，然后删除该项本身。 否则，这些函数调用 remove。 它们返回已成功删除的所有元素数。  
  
## <a name="a-namerenamea--rename"></a><a name="rename"></a>  rename  
  
```  
void rename(const path& from,  const path& to);
void rename(const path& from,  const path& to, error_code& ec) noexcept;  
```  
  
 这些函数将 `from` 重命名为 `to`。 符号链接自行重命名，无需它指定的文件。  
  
## <a name="a-nameresizefilea--resizefile"></a><a name="resize_file"></a>  resize_file  
  
```  
void resize(const path& pval, uintmax_t size);
void resize(const path& pval, uintmax_t size, error_code& ec) noexcept;  
```  
  
 这些函数调整文件的大小，以便 file_size\(pval\) \=\= size  
  
## <a name="a-namespacea--space"></a><a name="space"></a>  space  
  
```  
space_info space(const path& pval);
space_info space(const path& pval, error_code& ec) noexcept;  
```  
  
 该函数以 `space_info` 类型的结构返回有关 `pval` 指定的卷的信息。 对于无法确定的任意值，该结构包含 uintmax_t\(\-1\)。  
  
## <a name="a-namestatusa--status"></a><a name="status"></a>  status  
  
```  
file_status status(const path& pval);
file_status status(const path& pval, error_code& ec) noexcept;  
```  
  
 这些函数返回与 `pval` 关联的路径名状态、文件类型和权限。 符号链接不自行测试，而是对它指定的文件进行测试。  
  
## <a name="a-namestatusknowna--statusknown"></a><a name="status_known"></a>  status_known  
  
```  
bool status_known(file_status stat) noexcept;  
```  
  
 该函数返回 stat.type\(\) \!\= file_type::none  
  
## <a name="a-nameswapa--swap"></a><a name="swap"></a>  swap  
  
```  
void swap(path& left, path& right) noexcept;  
```  
  
 该函数交换 `left` 和 `right` 的内容。  
  
## <a name="a-namesymlinkstatusa--symlinkstatus"></a><a name="symlink_status"></a>  symlink_status  
  
```  
file_status symlink_status(const path& pval);
file_status symlink_status(const path& pval, erroxr_code& ec) noexcept;  
```  
  
 这些函数返回与 `pval` 关联的路径名符号链接状态、文件类型和权限。 这些函数的行为与 status\(pval\) 一致，只是符号链接自行测试，而无需它指定的文件。  
  
## <a name="a-namesystemcompletea--systemcomplete"></a><a name="system_complete"></a>  system_complete  
  
```  
path system_complete(const path& pval);
path system_complete(const path& pval, error_code& ec);
```  
  
 这些函数返回纳入考虑的绝对路径名，并在必要时返回与其根名称关联的当前目录。 \(对于 Posix，这些函数返回 absolute\(pval\)。\)  
  
## <a name="a-nametempdirectorypatha--tempdirectorypath"></a><a name="temp_directory_path"></a>  temp_directory_path  
  
```  
path temp_directory_path();
path temp_directory_path(error_code& ec);
```  
  
 这些函数返回适合包含临时文件的目录的路径名。  
  
## <a name="a-nameu8patha--u8path"></a><a name="u8path"></a>  u8path  
  
```  
template <class Source>  
path u8path(const Source& source);

template <class InIt>  
path u8path(InIt first, InIt last);
```  
  
 第一个函数的行为与 path(source) 相同，第二个函数的行为与 path(first, last) 相同，只是每种情况中的指定源被视为编码为 UTF-8 的 char 元素序列（无论是何种文件系统）。


