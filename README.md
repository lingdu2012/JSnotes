# JSnotes
> javascript相关代码片段笔记
### 对象的深拷贝（clone）
> 注意typeof 与 intanceof 的区别
> typeof 只能返回6个字符串，即 string、Boolean、number、function、object、undefined，不能对数组或对象进行判断
> instanceof 返回true或false
```javascript
function cloneObj(obj){
	let o=null;
	if(typeof(obj)=='object'){
		if(obj instanceof Array){
		    o=[];
		    for( let value of obj){
				o.push(value);
		    }
		}else{
			o={}
			for(let key in obj){
				o[key]=cloneObj(obj[key]);
			}
		}
	}else{
		o=obj;
	}
	return o;
}

let a={ab:'hello',b:[1,2],c:{m:'nihao',n:100}};
console.log(a);

let b=cloneObj(a);
console.log(b);
```
### 冒泡排序
> 比较相邻两个数的大小，如果前一个比后一个大，则两者交换位置；
> 第一轮结束后，最后一个数是最大的；
> 以此类推，进行N轮比较，每轮最后一个数不再参与比较。
```javascript
function arraySort(arr){
	let len=arr.length;
	for(let m=0;m<len-1;m++){
	   for(let n=1;n<len-1-m;n++){
	       if(arr[n]>arr[n+1]){
				let val=arr[n];
				arr[n]=arr[n+1];
				arr[n+1]=val;
		   }
	   }
	}
	return arr;
}

let testArr=[1,3,2,8,5,6];

console.log(arraySort(testArr));
```
### 不使用新数组去除数组中相邻重复的数字
> 注意两个用来计数的i和count的使用
```javascript
function arrayClear(arr){ 
	let count = 1;
	let i=1;
	while(i  < arr.length){
		if(arr[i] == arr[i-1]){
		  count++;
		  if(count==2) {
			 arr.splice(i-1,1);
			 i--;
		  }
		 
		}else{
		    i++;
			count=1;
		}
		
	}
	
	return arr;
}

let arr2=[1,1,2,3,3,5,6,6];
console.log(arrayClear(arr2));
```
> 利用ES6新数据结构快速去重
```javascript
//去重数组
let arr4=[1,1,2,3,3,5,6,6];
let newArr=[...new Set(arr4)];
console.log(newArr);
//去重字符串
let str="absbsdo";
let newStr=[...new Set(str)].join("");
console.log(newStr);
```

### 在数组中找出两数之和等于目标数字的组合
> 找出数组中下标的组合，尽量少重复使用同一个元素
```javascript
function findNums(arr,sum){
	let index=[];
	let len=arr.length;
	for(let i=0;i<len;i++){
		for(let j=i+1;j<len;j++){
			if(arr[i]+arr[j]==sum){
				index.push([i,j]);
			}
		}
	}
	return index;
}
let arr3=[2,7,4,6,3];

console.log(findNums(arr3,9));
```
### 简单计数器
> 利用闭包函数
```javascript
var add = (function () {
    var counter = 0;
    return function () {
		return counter += 1;
	}
})();
console.log(add());
console.log(add());
console.log(add());
```

### 找出字符串中的最长字串
> 连续的无重复子串
```javascript
function findChildStr(str){
	let arr=[...str];
	let child=[];
	let maxChild=[];
	let maxLen=0;
	for(let i=0;i<arr.length;i++){
		if(child.findIndex(y => y==arr[i])>-1){
			if(child.length > maxLen){
				maxLen=child.length;
				maxChild=child;
			}
			child=[];
			child.push(arr[i]);
		}else{
			child.push(arr[i]);
		}
	}
	console.log(maxChild);
	return maxChild.join("");
}
let longStr='abcabcbb';
console.log(findChildStr(longStr));
```

### 通过一个方法两种方式进行求和
> arguments对象对于可以传递可变数量的参数的函数很有用
```javascript
function sum(){
    let num = arguments[0];
    if(arguments.length==1){
        return function(sec){
            return num+sec;
        }
    }else{
        let num = 0;
        for(let i = 0;i<arguments.length;i++){
            num = num + arguments[i];
        }
    return num;
    }
}
console.log(sum(2)(3));
console.log(sum(2,3));
```
### 改变上下文指向
> bind，call，apply都是为了改变函数体内部 this 的指向。少量参数用call，大量参数用apply
> JavaScript的上下文分为定义时上下文，运行时上下文，其上下文是可以改变
> bind调用完成后不执行，call，apply是马上执行。相互之间是互通的，bind不兼容（IE5，6，7，8）
```javascript
function log(){
  console.log.apply(console, arguments);
};
console.log("输出");
log(1);    //1
log(1,2);    //1 2

function log(){
  var args = Array.prototype.slice.call(arguments);
  var date = new Date(); 
  var tim = date.getTime(); 
  args.unshift(tim);
  console.log.apply(console, args);
};
```