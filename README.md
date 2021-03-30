Cypress 教程

### 1、优势

#### **学习 Cypress 需要知道的几件事**

- 使用 JavaScript
- 用流行的 JS 测试框架 mocha & chai
- 架构不同于 selenium

#### **特性**

- 时间旅行（Time Travel)
- 实时加载
- 结果一致性
- 调试功能
- 自动等待
- 网络控制
- 截图和录频

### 2、安装

cypress 是使用 nodejs 开发的一款工具，所以需要先下载 [nodejs](https://nodejs.org/zh-cn/)。进入官网下载 LTS 长期支持版。下载好之后在命令行输入 node 命令和 npm 命令确认是否正确安装。 npm 是一款包管理工具，类似于 python 中的 pip。

![img](https://ky8tjff7tg.feishu.cn/space/api/box/stream/download/asynccode/?code=YTJjNDkzOWJhMTcyY2I5NTkwMjllNWI3NWM3MjA5NDBfd291TlFkMnY0akx1UHVvc21ZazVkd2ppM1ZsNENabUVfVG9rZW46Ym94Y25ZSWNnNWdqRFdHb081cnpVeklQVjhlXzE2MTcxMDQ1MjQ6MTYxNzEwODEyNF9WNA)



当 nodejs 和 npm 都正确安装好后，就可以通过 npm 安装 cypress 了。

1. 进入项目目录。
2. 通过 npm 初始化工程，得到 package.json 文件。
3. 通过 npm 安装 cypress。

```
cd CypressNotes
npm init -y
npm install cypress
```

 

需要注意的是，npm 有时候安装比较慢。如果出现网速慢无法安装成功，可以先通过 npm 安装 cnpm, 再通过 cnpm 安装 cypress。 cnpm 是国内镜像版，下载速度非常快。

```
npm install -g cnpm --registry=https://registry.npm.taobao.org
cnpm install cypress
```



#### **打开 Cypress 工程**

安装好 cypress 以后，可以通过 cypress open 指令打开项目。 cypress 命令是没有直接添加到系统变量当中的，需要进入 node_modules 目录下去手工启动：

```
 ./node_modules/.bin/cypress open
```



系统会打开一个类似于编辑器的 cypress 界面:

![img](https://ky8tjff7tg.feishu.cn/space/api/box/stream/download/asynccode/?code=YWI5NjhlOWFkNTNmMDQwNTYwYjM5NmVjYmJjZTE1YTRfb2pOeGhZQmtLb1hoeUlNZnRVMm4wYlhJcEtzQWFaVUFfVG9rZW46Ym94Y240NXRNRDdhWVVrcklJaHYwaWJqbWFmXzE2MTcxMDQ1MjQ6MTYxNzEwODEyNF9WNA)

所有的测试用例存放在 integration tests 中，cypress 会默认生成一些 examples 示例，如果需要编写其他的测试用例，在 integration 目录下建立 js 文件就可以了。

![img](https://ky8tjff7tg.feishu.cn/space/api/box/stream/download/asynccode/?code=NjFmMGM1ODY1YmEwNTJjOTA0N2YwN2FkM2Q2NmEyNDhfemR3Nzd3N0l4NTBDcHVjVGIyNWNUQmZDck1lZm84aVdfVG9rZW46Ym94Y25NVUR0QlhPelNHSEpKTnQ0eTlqWTNjXzE2MTcxMDQ1MjQ6MTYxNzEwODEyNF9WNA)

运行可以点击单个文件运行，也可以运行所有的。



默认用例看效果，左边可以点击查看运行步骤，右边是屏幕显示：



**cypress 的其他指令可以通过 --help 查看**：

 ./node_modules/.bin/cypress --help

#### **npx 运行**

npx 可以更加快捷的运行 cypress 命令，首先确认 npx 有没有安装，没有安装的话通过 npm install -g npx 安装。 安装完成后可以通过 npx cypress 直接运行 cypress 指令。

还有一种方式是再 package.json 配置 npm 命令。

```
 "scripts": {
     "cy": "node_modules/.bin/cypress"
 },
```



可以通过 npm run cy 运行了。



**Cypress 的代码结构说明**



#### **编写第一个测试用例**

打开 vscode， 在 interation 目录下创建一个 hello.js 文件。 在 cypress 的交互界面点击这个文件就可以运行。

运行结果会报错 No tests found in your file, 因为我们还没有编写任何的测试步骤。

![img](https://ky8tjff7tg.feishu.cn/space/api/box/stream/download/asynccode/?code=YWVmZmNkY2I3OTQyOTllZTgzZDEzZjMzNThhYWUyNDRfU1JCQWtaSzJWZURYc2RGeTVQZU5TZW9KU2kxMlM1NEJfVG9rZW46Ym94Y25HZjVQR2ZpeFR1N2NRNDlESUxyWDdnXzE2MTcxMDQ1MjQ6MTYxNzEwODEyNF9WNA)

在 hello.js 中编写测试代码：

 describe('这是我的第一条用例', () => {

​     it('1等于1', () => {

​         assert(1==1, "1 not equal to 1")

​     });

​     it('1不等于2', () => {

​         assert(1 != 2, "1 not equal to 2")

​     });

 })

- describe 表示测试用例场景
- it 表示详细的测试点
- assert 是断言
- 这里用到了 es6 的箭头函数，也可以写成 function() 的形式

这些语法是 JavaScript 中的测试框架 [Mocha](https://mochajs.org/#bdd) 的用法。 Mocha 除了可以用 describe 这些 bdd 的形式，还可以用 suite 和 test 这样的 tdd 形式，但是在 Cypress 中不直接支持。

断言使用的是 [Chai](https://docs.cypress.io/guides/references/assertions.html#Chai), 同样支持 bdd 和 tdd, 现在暂且用这种断言，后面可以换用其他的形式。

编写代码完成以后，再次点击 cypress 界面中的 hello.js， 就可以出现测试页面了。

![img](https://ky8tjff7tg.feishu.cn/space/api/box/stream/download/asynccode/?code=MWJlOWMzM2IwZDZiMWIxMTAwMWIyNWM5ZmIxYTU3ZTJfUnJkUEpDdFlpWE9zSVhCRXJGOEtwczJ3Q2NITUt4UnNfVG9rZW46Ym94Y254S2dRWUU3NE5GNlQ3YnpMQzRjb0poXzE2MTcxMDQ1MjQ6MTYxNzEwODEyNF9WNA)

再编写一个断言不成功的情况：

 it('1等于3', () => {

​         assert(1==3, "1 not equal to 3")

​     });

则断言失败的部分会用红色标明：

![img](https://ky8tjff7tg.feishu.cn/space/api/box/stream/download/asynccode/?code=M2VhMmYzOGY0YTI2ZjAyMjM0ZjZkOTIwNWU5NzA5MTFfc3VRbjRxQ2Zyd1Y2TUlkMTNXODRqZEx1QURxVUVEMmNfVG9rZW46Ym94Y25BU3M5RlkwSElDeVF5U0hBYTJNVVRmXzE2MTcxMDQ1MjQ6MTYxNzEwODEyNF9WNA)

#### **代码提示**

cypress 封装的方法默认是没有代码提示的。如果需要代码提示，最简单的方式是在文件的开头加一个特殊注释：

 /// <reference types="Cypress" />

这时候就可以看到 cy 下面的 api 了哦：



在 vscode 里面，如果你不想每次都在文件开头加注释，可以新建一个 jsconfig.json 文件，加上以下配置，效果是一样的。

```
 {
     "include": [
         "/node_modules/cypress",
         "cypress/**/*.js"
     ]
 }
```



你也可以在 vscode 中安装 cypress snippets 插件，安上以后，可以自动完成 it 等语法规则：





### 3、开始

### 4、JavaScript 基础语法

使用 cypress 进行端对端测试，和其他的一些框架有一个显著不同的地方，它使用 javascript 作为编程语言。传统主流的 selenium 框架是支持多语言的，大多数 QA 会的python 和 java 语言都可以编写 selenium 代码，遇到需要编写 js 代码的 cypress，以为又要学习一门编程语言，慢慢就放弃了。



其实学习 cypress 只需要掌握一些基础语法就够了。



#### 4.1、变量

在 js 里用 let 这个关键字定义变量，当一行代码结束后，可以用分号 ;  隔开。

```
let name = 'yuz' // ; or not 
```

浏览器当中都内置了 js 的解释器，上面的代码可以直接在浏览器中运行。按 F12 打开浏览器的开发者工具，点击 console 标签页，就可以输入 js 代码了。

![img](https://ky8tjff7tg.feishu.cn/space/api/box/stream/download/asynccode/?code=OWZjNDFkYjg5YWMxZjZhN2UwMjI1NzhlZGJiZjM2ZjZfd0JDdTJmSlBkdVd5UmJ5UWJtSm5zWlFpV2tRV2k4SGNfVG9rZW46Ym94Y24zYmdiQTk3dXhvQ3lYemtJYURCbUloXzE2MTcxMDQ1MjQ6MTYxNzEwODEyNF9WNA)

除了浏览器环境，也可以通过 node.js 环境运行代码。我们可以把上面的代码保存到 demo.js 文件中，然后在命令行工具中输入 node 指令运行代码。

```
node /path/to/demo.js
```

#### **4.2、条件分支**

js 的条件分支主要需要注意条件表达式要用括号包裹。

```
 let age = 17
 
 if (age > 18) {
     canSmoke = true
 }
 else {
     canSmoke = false
 }
 
 console.log("can i smoke? " + canSmoke)
```

在 js 的条件分支代码中，如果代码逻辑比较简单，经常使用三元运算符简化代码，它的使用方式是通过 ？表示。上面的代码可以改成三元运算符形式：

```
let age = 17
let canSmoke = (age > 18) ? true : false // false
```



#### **4.3、函数 （Function)**

定义函数时使用 function 关键字，然后是函数名，括号里填入参数，参数之间用逗号隔开，最后是花括号之间的代码（即“函数体”），函数的返回值使用 return 关键字。

```
 function add (a, b) {
     return a + b
 }
 
 let res = add(3, 4)
```



#### **4.4、箭头函数 (Arrow function)**

箭头函数在 js 使用中非常普遍，他能简化普通函数的写法。上面的普通函数改成箭头函数

```
add = (a, b) => {
    return a + b
}
add(3, 4)
```



#### 4.5、回调函数（Callback）

在 js 代码编写中，经常需要用到回调函数。它允许我们采用异步方式编程，当执行完一个任务以后，再通过回调触发另外的任务。

```
function print(string, callback) {
    let wait =  Math.random() * 5000;
    setTimeout(() => {
        console.log(string);
        callback();
    }, wait);
 }
```

在上面的例子中，print 函数允许程序随机等待 5 秒内的时间，再打印字符串，最终触发回调函数。在调用该函数时，可以通过箭头函数指定一个回调函数，比如打印"finished"。

```
print("hello", () => console.log("finished") )
```



回调函数如果不嵌套调用，是一个非常好的工具。但是一旦嵌套调用，会陷入“回调地狱” 。陷入回调地狱的代码加入 try catch 异常捕获之后，层次非常不清晰，严重影响阅读。

```
print("first", () => {
    print("second", () => {
        print("last", () => console.log("finished"))
    })
})
```



#### 4.6、Promise

Promise 是在异步编程中替代回调函数的编程方式。我们可以在函数中创建一个 Promise 对象，这个对象需要传递一个函数作为参数，通常可以写成箭头函数的形式。



箭头函数有两个特定参数 resolve 和 reject，resolve 负责把程序的正常结果返回出去， reject 负责程序出现异常时，把异常情况返回出去。

```
function print (string) {
    let promise = new Promise( (resolve, reject) => {
        let wait =  Math.random() * 5000;
        setTimeout(() => {}, wait);
        resolve(string);
        reject(new Error());
    })
    return promise;
}

let promise = print("some thing");
promise.then( result => console.log('first'), err => {} )
       .then( result => console.log('second'), err => {} )
       .then( result => console.log('last'), err => {} )
```



#### 4.7、Async / Await

Promise 比普通回调函数的方式更容易编写，但是也涉及到 resolve，reject 和 then 等很多概念，如果 then 很多，代码也不好看。Async/Await 是以更舒适的方式使用 promise 的一种特殊语法，同时它也非常易于理解和使用。我们只需要在普通函数前面加上 async 关键字，那么这个函数的返回值将是一个 promise 对象。

```
async function print() {
    return 8;
}
print() // Promise {<fulfilled>: 8}
```



虽然函数在定义的时候确定了返回值是 8，但是当调用 print 函数时，得到的是一个 Promise, 而不是 8 。如果需要获取到其中返回值，可以通过 then 方法：

```
let promise = print()
promise.then( (result) => console.log(result) )
```

如果觉得 then 写法不喜欢，可以换成 await 获取返回值：

```
let promise = print()
console.log(await promise)
// or
let result = await print()
```

之前的回调函数例子可以改写成 async / await 的形式：

```
async function print (string) {
    let wait =  Math.random() * 5000;
    setTimeout(() => {}, wait);
    return string;
}

console.log(await print("first"))
console.log(await print("second"))
console.log(await print("last"))
```



#### 4.8、**[mocha](https://ky8tjff7tg.feishu.cn/docs/doccnJM8b21fS7giN31vn5Ntz4f)** **&** **[chai](https://www.chaijs.com/)**

当编写完一些 js 代码之后，你需要对这些代码进行测试，保证代码能按预期执行，并得到预期结果。而 mocha 是一个非常出色的 js 单元测试框架，chai 专门处理断言。需要使用这两个框架时，先通过 npm 安装：

```
 npm install mocha chai
```



接着就可以写用例了，用例最好写到以 test 命名的目录中，每一个 js 文件就是一个规范（spec），它表示被测试的函数应该是怎样的。在这个规范文件中，包含了对功能的描述（describe）和测试用例（it）以及断言情况（assert）。编写好测试代码后，进入文件目录，在命令行通过 npx mocha 运行。

```
// test/mocha.spec.js
const assert = require('assert');

// the function to be tested
function pow(a, b) {return a ** b};

// tests
describe("pow", () => {
    it('pow of 2 and 3', () => {
        let actual = pow(2, 3);
        assert.equal(actual, 8);
    })
    
    it('pow of string and 3', () => {
        let actual = pow("a", 3);
        assert.equal(actual, 8);
    })
})
```



正如你所看到的，一个规范包含三个部分： 

1、describe

表示我们正在描述的功能是什么。在我们的例子中我们正在描述函数 pow。描述的作用是组织测试用例（it)，在一个描述中，通常会包含多个 it 用例。

2、it

需要执行的用例，第二个参数是用于测试 pow 函数的代码，通常来说是一个函数。

3、assert

断言，表示测试的结果是否符合预期。



cypress 框架 对 mocha 进行了集成，编写测试代码用的正是 mocha 的表示方法，所以学好 mocha, cypress 就学会了一半。下面这个例子就是 cypress 执行浏览器测试的代码，可以看出，和 mocha 没有区别，只是在 cypress 中，不能直接使用 assert 这种显性断言方式。

```
describe("go to the home page", () => {
    it('title contains', () => {
        cy.visit("http://www.testingpai.com")
        cy.title().should('include', '测试派')
    });
})
```



#### 4.9、总结

要进行浏览器端的自动化测试，掌握核心的 js 用法是必不可少的，本文提到的 8 个知识点，都会频繁用到。

- 通过 let 关键字命名变量。
- 通过 if 和三元表达式控制条件。
- 普通的 function 形式函数定义。
- 箭头函数也经常使用，有点类似匿名函数。
- 回调函数在 js 当中非常常见，但是会遇到回调地狱的问题。
- Promise 是解决回调地狱的有效手段，promise 和 then 的用法会经常碰到。
- Async / Await 是另一种更优雅的使用 promise 的方式，更推荐使用。







```
// test.js
 var should = require('chai').should()
 
 describe('Test name variable', () => {
     let name = 'yuz'
     
     it("name should be string", () => {
         name.should.be.a("string")
     })
 
     it("name should be equal to yuz", () => {
         name.should.equal('yuz')
     })
 })
```

 

### 5、mocha

Mocha 一个最简单的例子是这样的。

```
// test/mocha.spec.js
const assert = require('assert');

// the function to be tested
function pow(a, b) {return a ** b};

// tests
describe("pow", () => {
    it('pow of 2 and 3', () => {
        let actual = pow(2, 3);
        assert.equal(actual, 8);
    })
    
    it('pow of string and 3', () => {
        let actual = pow("a", 3);
        assert.equal(actual, 8);
    })
})
```



实际上，mocha 官方不推荐用箭头函数(匿名函数)来表示测试过程，而是使用普通的 function 函数表达式，因为箭头函数不能通过 this 访问 mocha 的上下文。



使用箭头函数在不用 this 获取 mocha 上下文时不会有问题，但是一旦需要 this 访问上下文，箭头函数会报错。

```
// 错误写法
const assert = require('assert');

describe('my suite', () => {
    it('my test', () => {
        // should set the timeout of this test to 1000 ms; 
        // instead will fail
        this.timeout(1000)
        assert.ok(true);
    });
});
```

此时必须使用 function 函数表达式：

```
// 正确写法
const assert = require('assert');

describe('my suite', function() {
    it('my test', function() {
        this.timeout(1000)
        assert.ok(true);
    });
});
```



#### 5.1、hook

Mocha 提供了 before、after、beforeEach、afterEach 执行前置条件和后置清理工作。

1. before 在这个描述的开始执行一次
2. after 在这个描述的结束执行一次
3. beforeEach 在每个用例之前都执行一次
4. afterEach 在每个用例之后都执行一次  

```
const assert = require('assert');

describe('hooks', function() {
    before(function() {
      // runs once before the first test in this block
      console.log("before")
    });
  
    after(function() {
      // runs once after the last test in this block
      console.log("after")
    });
  
    beforeEach(function() {
      // runs before each test in this block
      console.log("before each")
    });
  
    afterEach(function() {
      // runs after each test in this block
      console.log("after each")
    });
  
    // test cases
    it('pow of 2 and 3', () => {
        assert(true)
    });
    
    it('pow of string and 3', () => {
        assert(true)
    });
    
 });
```



Hook 也可以加说明，解释需要做什么事情：

```
beforeEach('some description', function() {
  // beforeEach:some description
});
```



#### 5.2、运行指定用例

在 it 用例后添加 only 函数就可以指定用例，标记了 only 的用例会运行，没有标记的不会运行。

```
describe('#indexOf()', function() {
    it.only('should return -1 unless present', function() {
      // this test will be run
    });

    it.only('should return the index when present', function() {
      // this test will also be run
    });

    it('should return -1 if called with a non-Array context', function() {
      // this test will not be run
    });
});
```

不仅可以在 it 用例上使用 only，而且可以在嵌套的 describe 中使用：

```
describe('Array', function() {
  describe.only('#indexOf()', function() {
    it('should return -1 unless present', function() {
      // this test will be run
    });

    it('should return the index when present', function() {
      // this test will also be run
    });
  });

  describe.only('#concat()', function() {
    it('should return a new Array', function() {
      // this test will also be run
    });
  });

  describe('#slice()', function() {
    it('should return a new Array', function() {
      // this test will not be run
    });
  });
});
```



#### 5.3、跳过用例

在 mocha 中，可以通过 only 指定需要执行的用例，也可以通过 skip 跳过用例，用法和 only 基本一致，你可以通过 it.skip 跳过一个用例，也可以通过 describe.skip 跳过整个描述。



除此之外，你还可以根据环境变量的值判断，当满足条件时，再跳过用例。

```
it('should only test in the correct environment', function() {
  if (Cypress.env('host') === 'local') {
    // make assertions
  } else {
    this.skip();
  }
});
```



你甚至可以在 describe 或者 before 函数中，跳过整个块中的所有用例：

```
before(function() {
  if (Cypress.env('host') === 'local') {
    // setup code
  } else {
    this.skip();
  }
});
```



#### 

#### 5.4、重复执行

在一些脆弱的测试中，一次执行可能并不能成功执行用例。在web测试过程中，因为网络环境和其他因素影响，会造成用例执行不稳定，此时你需要对失败用例重复执行。在 mocha 当中，你可以通过 this.retry 在 describe 和 it 中设置失败执行次数，你也可以在 before函数中设置，但是在 beforeEach 是不可以的。

```
describe('retries', function() {
  // Retry all tests in this suite up to 4 times
  this.retries(4);

  beforeEach(function() {
    browser.get('http://www.yahoo.com');
  });

  it('should succeed on the 3rd try', function() {
    // Specify this test to only retry up to 2 times
    this.retries(2);
    expect($('.foo').isDisplayed()).to.eventually.be.true;
  });
});
```



#### 5.5 动态生成用例

你已经有了 3 组测试数据，这 3 组数据的测试步骤都是一样的，那就没有必要重复去编写 3 个测试函数，没错，用数据驱动，根据 3 组数据动态生成 3 个用例。

```
const assert = require('chai').assert;

function add(args) {
  return args.reduce((prev, curr) => prev + curr, 0);
}

describe('add()', function() {
  const tests = [
    {args: [1, 2], expected: 3},
    {args: [1, 2, 3], expected: 6},
    {args: [1, 2, 3, 4], expected: 10}
  ];

  tests.forEach(({args, expected}) => {
    it(`correctly adds ${args.length} args`, function() {
      const res = add(args);
      assert.equal(res, expected);
    });
  });
});
```





### 5、页面导航

#### 5.1、导航函数

```
describe("导航", () => {
    
    it('导航操作', () => {
        cy.visit("http://testingpai.com")
        cy.visit("http://testingpai.com/login")
        cy.title().should('include', '登录')
        cy.go("back")
        cy.title().should('include', '测试派')
        cy.go("forward")
        cy.title().should('include', '登录')
        cy.go(-1)
        cy.title().should('include', '测试派')
        cy.go(1)
        cy.title().should('include', '登录')
        cy.reload()
        cy.title().should('include', '登录')
    })

})
```



能不能在中间打印值呢？可以，但是得到的是一个 Chainer 对象。

```
it.only('cy 操作中赋值', () => {
    cy.visit("http://testingpai.com")
    // 可以赋值，但是得到的是一个 Chainer 对象，无法获取值。
    let title = cy.title()
    title.should('include', '测试派')
    console.log(title) // Chainer
});
```

#### 5.2、同源策略

能不能在导航中访问其他域名？不能，cypress 为了安全采取了同源策略，在一个用例中不能同时访问多个域名。

```
// no 
it('访问其他域名', () => {
    cy.visit("http://testingpai.com")
    cy.visit('https://readhub.cn/')
});
```



虽然不能在同一个用例中访问不同源的地址，但是在不同的用例中是可以存在不同域名的地址的。

```
it.only('分用例访问不同域名', () => {
    cy.visit("http://testingpai.com")
});

it.only('分用例访问不同域名2', () => {
    cy.visit("https://readhub.cn/")
});
```

#### 5.3、特色功能：发送post请求

页面访问时，cypress 的特色是它不仅可以发 get 请求，而且支持 post 请求，只要页面返回的是 html，就可以解析其中的数据。我们可以通过 mockoon 工具创建一个 post 请求的 api，然后通过 visit 方法访问接口。

```
it.only('发送 post 请求', () => {
    cy.visit({
        url: "http://127.0.0.1:3001/demo",
        method: 'POST',
        body: {},
        header: {},
    })
    cy.get('#title').should('have.text', 'hello world')
});
```

#### 5.4、baseUrl

项目路径配置可以在 cypress.json 文件中配置域名，然后访问地址时可以使用相对路径访问。当域名发生变化时，只需要修改一个地方。

```
{
    "baseUrl": "http://testingpai.com"
}
```



### 6、元素定位

#### 6.1、辅助工具

在 cypress 的 ui 界面里，有快捷的辅助定位工具。打开网页后，点击靶心图标去定位元素，然后点击打印该元素，我们就可以在控制台查看是不是我们想要的元素，如果确定元素，直接复制代码到编辑器就可以了。

![img](https://ky8tjff7tg.feishu.cn/space/api/box/stream/download/asynccode/?code=MTI3NTJlODFlZDU3MzBjMjg2NTNlNDZhMzFiMTcyNGRfYWk3emRwb29XZUdmM3VZdnNVZnBsd2owMlZMdWtWc0FfVG9rZW46Ym94Y24yRUh0TUxRelFJcGttVUpGQUY5ZHRlXzE2MTcxMDQ1MjQ6MTYxNzEwODEyNF9WNA)



#### 6.2、定位函数

Cypress 使用 css 选择器定位元素，主要使用的元素定位方式有：

- cy.get, 通过 css 选择器定位元素
- cy.contains, 通过text定位
- cy.within, 在某个节点内定位



用得最多得 get 和 contains

```
describe("元素定位", () => {
    it('get 定位元素', () => {
        cy.visit('http://testingpai.com')
        cy.contains('登录').click()
        cy.get('#nameOrEmail').focus().type('wagyu2016@163.com')
        cy.get('#loginPassword').focus().type('admin123456')
        cy.get('#loginBtn').click()
        cy.get('.user-nav > a.nav__item').should('be.visible')
    });
})
```

Form 表单这样的需要对多个子元素操作的，用 within 划定作用域。

```
it.only('within', () => {
    cy.visit('http://testingpai.com/login')
    cy.get('#verifyForm').within( $form => {
        cy.get('input:first').focus().type('wagyu2016@163.com')
        cy.get('input[type="password"]').focus().type('admin123456')
        cy.contains('登录').click()
    })
});
```

#### 6.3、索引

复杂元素可以先划定作用域，再通过索引获取，使用索引的方式：

- first()
- last()
- eq(0)

```
it.only('within', () => {
    cy.visit('http://testingpai.com/login')
    cy.get('#verifyForm').within( $form => {
        cy.get('input').first().focus().type('wagyu2016@163.com')
        cy.get('input').eq(1).focus().type('admin123456')
        cy.contains('登录').click()
    })
});
```

#### 6.4、同级

对于同级元素，可以使用以下 api 相互定位：

- prev('#prev')
- next('input')
- sibling('.s')



#### 6.5、环境变量保存敏感信息

敏感信息通过 env 环境变量保存到 cypress.env.json 文件当中，并使用 .gitignore 在版本控制系统中过滤。当然你也可以直接在系统中设置环境变量。

```
{
    "user01": {
        "email": "wagyu2016@163.com",
        "password": "admin123456"
    }
}
```



然后通过 Cypress.env 调用：

```
it.only('within and env file', () => {
    cy.visit('http://testingpai.com/login')
    cy.get('#verifyForm').within( $form => {
        cy.get('input').first().focus().type(Cypress.env('user01').email )
        cy.get('input').eq(1).focus().type(Cypress.env('user01').password)
        cy.contains('登录').click()
    })
});
```



保存 Cookie 后面使用？ 



### 7、鼠标操作

- dbclick
- rightclick

### 8、选择操作

- check
- 强制选择 {'force': true}
- 选择单个 check('value')
- 选择多个 check(['value1', 'value2'])

```
describe("", () => { 
 
    it("点击", () => { 
        // 访问 url 
        cy.visit('https://example.cypress.io/commands/actions') 
        cy.get('.action-checkboxes [type="checkbox"]').not("[disabled]").check() 
        cy.get('.action-multiple-checkboxes [type="checkbox"]').check() 
 
        cy.get('.action-checkboxes [type="checkbox"]').check({"force": true}) 
         
        // 取消所有选择 
        cy.get('.action-checkboxes [type="checkbox"]').uncheck({"force": true}) 
        cy.get('.action-multiple-checkboxes [type="checkbox"]').uncheck() 
 
        // 选择某个 
        cy.get('.action-checkboxes [type="checkbox"]').check('checkbox3') 
        cy.get('.action-multiple-checkboxes [type="checkbox"]').check(['checkbox2', 'checkbox3']) 
 
        // 单选 
        cy.get('.action-radios [type="radio"]').check('radio2') 
 
    }) 
})
```



- Select

```
describe("", () => { 
 
    it("点击", () => { 
        // 访问 url 
        cy.visit('https://example.cypress.io/commands/actions') 
         
        // 单选 
        // cy.get('.action-select').select('bananas') 
         
        // 多选， 可以用 text, 也可以用 value 
        cy.get('.action-select-multiple').select(['fr-bananas', 'fr-apples']) 
 
    }) 
})
```



### 9、滚动

#### 9.1、窗口滚动

- cy.scrollTo('bottom')
- cy.scrollTo(0, 250)
- cy.scrollTo('0%', '25%')

```
 it('scrollTo', () => {
     cy.visit('https://example.cypress.io/commands/querying')
     cy.wait(2000)
     cy.scrollTo('bottom')
     cy.wait(2000)
     cy.scrollTo('top')
     cy.wait(2000)
     cy.scrollTo('center')
     cy.wait(2000)
     cy.scrollTo(0,250)
     cy.wait(2000)
     cy.scrollTo('0%', '25%')
 }
```

#### 9.2、可滚动元素

- cy.get().scrollTo('bottom')
- cy.get().scrollTo(0, 250)
- cy.get().scrollTo('0%', '25%')

```
cy.visit('https://example.cypress.io/commands/actions') 
cy.get('#scrollable-horizontal').scrollIntoView() 
cy.wait(2000) 
 
cy.get('#scrollable-horizontal').scrollTo(0, 250, { easing: 'linear' }) 
cy.wait(2000) 
 
cy.get('#scrollable-horizontal').scrollTo('0%', '25%', { duration: 2000 })
```



### Iframe

```
describe('iframe', () => {
    const getIframeDocument = () => {
        return cy
        .get('#iframeResult')
        .its('0.contentDocument').should('exist')
    }

    const getIframeBody = () => {
        return getIframeDocument()
        .its('body').should('not.be.undefined')
        // wraps "body" DOM element to allow
        // chaining more Cypress commands, like ".find(...)"
        .then(cy.wrap)
    }

    it('works (simply)', () => {
        cy.visit('https://www.runoob.com/try/try.php',{
            qs:{filename: "tryhtml5_draganddrop"}
        })
        // use find(), not get()
        getIframeBody().find('#drag1').should('have.attr', 'height', '69')
    })
})
```





### 10、文件上传

上传文件需要安装插件 cypress-file-upload。首先把需要上传的数据放到 fixture 目录中，点击上传直接通过 attachFile 完成上传。如果是拖拽上传，需要指定可选参数 subjectType 为 drag-n-drop。

```
import 'cypress-file-upload'

it('', () => {
    cy.visit('https://ant.design/components/upload-cn/#components-upload-demo-drag');
    cy.get('.ant-upload-drag-container')
    .attachFile('example.json', { subjectType: 'drag-n-drop' })
});
```

如果你有较多的第三方插件不想在每个文件分别导入，可以在 support 的 index.js 文件下面引入新插件

```
 import 'cypress-file-upload'
 import './commands' // 这个是之前的
```







### 11、测试报告

安装插件

```
npm install mochawesome --save 
npm install mochawesome-merge --save 
npm install mochawesome-report-generator --save
```

cypress.json 配置

```
{ 
    "reporter": "mochawesome", 
    "reporterOptions": { 
        "overwrite": false, 
        "html": false, 
        "json": true 
    } 
}
```

运行程序

```
const cypress = require('cypress') 
const { merge } = require('mochawesome-merge') 
const generator = require('mochawesome-report-generator') 

async function runTests() { 
    const { totalFailed } = await cypress.run()  
    const jsonReport = await merge()  
    console.log(jsonReport) 
    await generator.create(jsonReport) 
    process.exit(totalFailed)  
} 

runTests()
```



### 12、命令行运行

```
// run all
npx cypress run
// run node
npx cypress run --spec "cypress\intergration\demo.spec.js" 
// headed or headless
npx cypress run --headed 
// browser
npx cypress run --browser=chrome 
```





### 环境变量配置

敏感信息通过 env 环境变量保存到 cypress.env.json 文件当中，并使用 .gitignore 在版本控制系统中过滤。当然你也可以直接在系统中设置环境变量。

```
{
    "user01": {
        "email": "wagyu2016@163.com",
        "password": "admin123456"
    }
}
```

然后通过 Cypress.env 调用：

```
it.only('within and env file', () => {
    cy.visit('http://testingpai.com/login')
    cy.get('#verifyForm').within( $form => {
        cy.get('input').first().focus().type(Cypress.env('user01').email )
        cy.get('input').eq(1).focus().type(Cypress.env('user01').password)
        cy.contains('登录').click()
    })
});
```



### 





录屏

请求

alias

环境变量

并行