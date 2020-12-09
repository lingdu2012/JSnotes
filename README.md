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

