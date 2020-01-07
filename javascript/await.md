# async与await

```
var a = 0;
async function test(){
 let result= await 10 + a;
 console.log(result);
}

test();
a=a+1;

```

输入：11

```
var a = 0;
async function test(){
 let result = a + await 10; // 此时a=0
 console.log(result);
}

test();
a = a + 1;

```

输入：10

async 代表异步，await 代表等待返回结果，原理是 promise。

```
function getConstant() {
return 1
}

async function getAsyncConstant() {
return 1
}

async function getPromise() {
return new Promise((resolved, rejected)=> {
resolved(1)
});
}

async function test() {
a = 2
c = 1
await getConstant();
d = 3
await getPromise();
d = 4
await getAsyncConstant();
return 2
}

```

babel 转换

```
function getConstant() {
return 1;
}

function getAsyncConstant() {
return Promise.resolve().then(function () {
return 1;
});
}

function getPromise() {
return Promise.resolve().then(function () {
return new Promise((resolved, rejected) => {
resolved(1);
});
});
}

function test() {
return Promise.resolve().then(function () {
a = 2;
c = 1;
return getConstant();
}).then(function () {
d = 3;
return getPromise();
}).then(function () {
d = 4;
return getAsyncConstant();
}).then(function () {
return 2;
});
}

```
