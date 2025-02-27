# 基础信息

|      |      |
|------|------|
| 编码语言 | .java |
| 代码路径 | auto-suggest-java-demo/src/main/java/org/example/leansoftx/Trie.java |
| 包名 | org.example.leansoftx |
| 依赖项 | ['java.util'] |
| 概述说明 | Trie类实现字典树数据结构，支持插入、补全、获取单词、打印树结构、拼写建议等，递归打印树，编辑距离计算字符串间距离。 |

# 说明

这段代码实现了一个名为Trie的字典树数据结构的类。Trie类包含了插入单词、自动补全建议、获取所有单词、打印字典树结构、获取拼写建议等功能。

其中，插入单词的功能用于将单词逐个字符地插入到字典树中。自动补全建议的功能用于查询字典树中以给定前缀开头的所有单词，并返回这些单词作为建议。获取所有单词的功能用于返回字典树中存储的所有单词。打印字典树结构的功能使用了递归方式，用于按层次打印字典树的结构。获取拼写建议的功能用于查询字典树中与给定单词相似的拼写建议，并返回这些建议。

此外，代码还实现了一个计算两个字符串之间的编辑距离的函数。编辑距离是指通过插入、删除和替换操作将一个字符串转换为另一个字符串所需的最小操作次数。

通过这些功能，Trie类提供了方便的字典树操作和字符串相关计算的方法，可以用于处理文本数据和实现拼写检查等应用。

# 类列表 Class Summary

| 名称   | 类型  | 说明 |
|-------|------|-------------|
| Trie | class | 这段代码实现了一个字典树数据结构的类Trie。它包括了插入单词、自动补全建议、获取所有单词、打印字典树结构、获取拼写建议等功能。其中，打印字典树结构函数使用了递归方式。还实现了一个计算两个字符串之间的编辑距离函数。 |



## 类 Trie

|      |      |
|------|------|
| 访问范围 | public |
| 类型 | class |
| 名称 | Trie |
| 说明 | 这段代码实现了一个字典树数据结构的类Trie。它包括了插入单词、自动补全建议、获取所有单词、打印字典树结构、获取拼写建议等功能。其中，打印字典树结构函数使用了递归方式。还实现了一个计算两个字符串之间的编辑距离函数。 |


### UML类图

classDiagram
class Trie {
    -root: TrieNode
    +Trie()
    +insert(String word): boolean
    +autoSuggest(String prefix): List<String>
    +getAllWordsWithPrefix(TrieNode node, String prefix): List<String>
    +getAllWords(): List<String>
    +printTrieStructure()
    -_printTrieNodes(TrieNode root, String format, boolean isLastChild)
    +getSpellingSuggestions(String word): List<String>
    +levenshteinDistance(String s, String t): int
}
class TrieNode {
    -value: char
    -isEndOfWord: boolean
    -children: Map<Character, TrieNode>
    +TrieNode()
    +TrieNode(char value)
    +hasChild(char c): boolean
}
Trie <|.. TrieNode
TrieNode "*"..1 TrieNode : children


### 内部方法调用关系图

graph TD;
root-->insert
insert-->[]=new TrieNode
[]=new TrieNode-->children.put
insert-->getCurrentNode
getCurrentNode-->hasChild
hasChild-->return
getCurrentNode-->children.get
children.get-->[]=isEndOfWord=true
isEndOfWord=true-->return
insert-->isEndOfWord
isEndOfWord-->return
root-->autoSuggest
autoSuggest-->getCurrentNode
getCurrentNode-->hasChild
hasChild-->ArrayList
hasChild-->return
getCurrentNode-->children.get
children.get-->getAllWordsWithPrefix
getAllWordsWithPrefix-->return
root-->getAllWordsWithPrefix
getAllWordsWithPrefix-->return
root-->printTrieStructure
printTrieStructure-->_printTrieNodes
printTrieStructure-->println
_printTrieNodes-->checkNull
checkNull-->return
_printTrieNodes-->println
println-->children.sort
println-->println
children.sort-->return
println-->children.get
children.get-->_printTrieNodes
println-->children.size
children.size-->==1
println-->=_printTrieNodes
println-->format+
println-->format +=
println-->children.get.getValue
children.get.getValue-->_printTrieNodes
println-->_printTrieNodes
println-->==children.size-1
_printTrieNodes-->return
root-->getSpellingSuggestions
getSpellingSuggestions-->charAt
charAt-->ArrayList
charAt-->getAllWordsWithPrefix
getAllWordsWithPrefix-->words
getAllWordsWithPrefix-->String.valueOf
words-->levenshteinDistance
levenshteinDistance--><=2
<=2-->add
levenshteinDistance-->return
root-->levenshteinDistance
levenshteinDistance-->char
levenshteinDistance-->char
charAt-->return

### 字段列表 Field List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| root | TrieNode | 包含一个私有的TrieNode根节点。 |

### 方法列表 Method List

| 名称  | 类型  | 说明 |
|-------|-------|------|
| _printTrieNodes | void | 该代码段是一个打印字典树节点的方法，使用递归实现。通过对每个节点进行格式化输出，将节点的值打印出来，并对节点的子节点进行排序后再递归调用该方法。 |
| levenshteinDistance | int | 本文提供了一个计算两个字符串之间的最小编辑距离的算法。算法使用Levenshtein距离来度量两个字符串之间的差异。通过动态规划的方法，计算出两个字符串之间的最小编辑距离后返回。 |
| getSpellingSuggestions | List<String> | 根据输入的单词提供拼写建议。通过获取首字母获取单词列表，然后使用Levenshtein距离计算单词间的差异，若小于等于2则添加到建议列表。返回建议列表。 |
| insert | boolean | 插入方法：遍历输入的字符串，将每个字符作为键添加到字典树中的子节点中，如果节点不存在则创建新节点。
如果最后一个节点已经是一个单词的末尾，返回false，否则将最后一个节点设为单词结尾，并返回true。 |
| getAllWordsWithPrefix | List<String> | 提供一个方法，用于从Trie树中获取以指定前缀开头的所有单词列表。 |
| printTrieStructure | void | 打印Trie结构，以根节点开始打印，使用空格作为缩进标识符。 |
| getAllWords | List<String> | 该方法返回以指定前缀开头的所有单词列表。使用的是树结构，根节点为root，初始前缀为空。 |
| autoSuggest | List<String> | 根据给定的前缀，在字典树中自动补全匹配的词列表。通过遍历前缀字符，如果没有子节点则返回空列表，否则返回与前缀匹配的所有词。 |




