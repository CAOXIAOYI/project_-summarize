# ES6知识点总结

### 1.for..of..循环
	
for-of循环不仅支持数组，还支持大多数类数组对象，例如DOM NodeList对象。for-of循环也支持字符串遍历，它将字符串视为一系列的Unicode字符来进行遍历：


```
		for (var value of myArray) {
		 	 console.log(value);
		}
```


for...of无法获取数组的索引值，可以将数组转换为Map进行操作


```
for(let [index,elem] of new Map( arr.map( ( item, i ) => [ i, item ] ) )){
　　console.log(index);
　　console.log(elem);
}
```


### 2.模板字符串
反撇号字符 ` 代替普通字符串的引号 ' 或 " 外，它们看起来与普通字符串并无二致。

	function authorize(user, action) {
  		if (!user.hasPrivilege(action)) {
    	throw new Error(
     		 `用户 ${user.name} 未被授权执行 ${action} 操作。`);
  		}
	}	
	`g-body unscroll-wrap ${isHomepageVertical ? 'vertical' : ''}`
	还可以做判断

在这个示例中，${user.name}和${action}被称为模板占位符，JavaScript将把user.name和action的值插入到最终生成的字符串中

1. 模板占位符中的代码可以是任意JavaScript表达式，所以函数调用、算数运算等这些都可以作为占位符使用，你甚至可以在一个模板字符串中嵌套另一个，我称之为模板套构（template inception）。
1. 如果这两个值都不是字符串，可以按照常规将其转换为字符串。例如：如果action是一个对象，将会调用它的.toString()方法将其转换为字符串值。
1. 如果你需要在模板字符串中书写反撇号，你必须使用反斜杠将其转义：`\``等价于"`"。
1. 同样地，如果你需要在模板字符串中引入字符$和{。无论你要实现什么样的目标，你都需要用反斜杠转义每一个字符：`\$`和`\{`。
2. 可以书写多行

```
	$("#warning").html(`
	  	<h1>小心！>/h1>
	  	<p>未经授权打冰球可能受罚
	  	将近${maxPenalty}分钟。</p>
	`);
```
### 3.不定参数默认参数
	
##### 不定参数


```
function containsAll(haystack, ...needles) {
  for (var needle of needles) {
    if (haystack.indexOf(needle) === -1) {
      return false;
    }
  }
  return true;
}
containsAll("banana", "b", "nan")

```
传递进来的第一个参数"banana"赋值给参数haystack，needles前的省略号表明它是一个不定参数，所有传递进来的其它参数都被放到一个数组中，赋值给变量needles。needles被赋值为["b", "nan"]，后续的函数执行过程一如往常。

在所有函数参数中，只有最后一个才可以被标记为不定参数。函数被调用时，不定参数前的所有参数都正常填充，任何“额外的”参数都被放进一个数组中并赋值给不定参数。如果没有额外的参数，不定参数就是一个空数组，它永远不会是undefined。

##### 默认参数

```
function animalSentence(animals2="tigers", animals3="bears") {
    return `Lions and ${animals2} and ${animals3}! Oh my!`;
}
animalSentence();                       // Lions and tigers and bears! Oh my!
animalSentence("elephants");            // Lions and elephants and bears! Oh my!
animalSentence("elephants", "whales");  // Lions and elephants and whales! Oh my!
```

### 4.Set与Map
##### 	Set

一个Set是一群值的集合。它是可变的，能够增删元素，不会包含相同的元素。

Set支持的所有操作：

```
	new Set：创建一个新的、空的Set。
	new Set(iterable)：从任何可遍历数据中提取元素，构造出一个新的集合。
	set.size：获取集合的大小，即其中元素的个数。
	set.has(value)：判定集合中是否含有指定元素，返回一个布尔值。
	set.add(value)：添加元素。如果与已有重复，则不产生效果。
	set.delete(value)：删除元素。如果并不存在，则不产生效果。.add()和.delete()都会返回集合自身，所以我们可以用链式语法。
	set[Symbol.iterator]()：返回一个新的遍历整个集合的迭代器。一般这个方法不会被直接调用，因为实际上就是它使集合能够被遍历，也就是说，我们可以直接写for (v of set) {...}等等。
	set.forEach(f)：直接用代码来解释好了，它就像是for (let value of set) { f(value, value, set); }的简写，类似于数组的.forEach()方法。
	set.clear()：清空集合。
	set.keys()、set.values()和set.entries()返回各种迭代器，它们是为了兼容Map而提供的
```

##### Map

一个Map对象由若干键值对组成
Map支持的操作：

```
new Map：返回一个新的、空的Map。
new Map(pairs)：根据所含元素形如[key, value]的数组pairs来创建一个新的Map。这里提供的pairs可以是一个已有的Map 对象，可以是一个由二元数组组成的数组，也可以是逐个生成二元数组的一个生成器，等等。
map.size：返回Map中项目的个数。
map.has(key)：测试一个键名是否存在，类似key in obj。
map.get(key)：返回一个键名对应的值，若键名不存在则返回undefined，类似obj[key]。
map.set(key, value)：添加一对新的键值对，如果键名已存在就覆盖。
map.delete(key)：按键名删除一项，类似delete obj[key]。
map.clear()：清空Map。
map[Symbol.iterator]()：返回遍历所有项的迭代器，每项用一个键和值组成的二元数组表示。
map.forEach(f) 类似for (let [key, value] of map) { f(value, key, map); }。这里诡异的参数顺序，和Set中一样，是对应着Array.prototype.forEach()。
map.keys()：返回遍历所有键的迭代器。
map.values()：返回遍历所有值的迭代器。
map.entries()：返回遍历所有项的迭代器，就像map[Symbol.iterator]()。实际上，它们就是同一个方法，不同名字。
```





	
	




















