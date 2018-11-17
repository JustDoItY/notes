# async和promise的使用

## 1. promise

- promise是处理异步的一种方式，当异步处理完毕，可以根据结果，调用resolve或着reject函数，用then处理resolve和reject的返回值，catch函数可以捕捉异常。
- Promise.race()方法，可以接收一个数组，返回最快的那个正确结果。
- Promise.all()方法，接收一个数组，当所有结果正确返回的时候，才会返回正确结果。

## 2. async函数，await

- async函数是es6中出现的概念，要配合await和promise使用
- async函数和普通函数的区别，async函数返回都是被promise对象，普通函数返回的什么就是什么
- 在async函数内，可以使用await，只有当await后的异步处理执行完，才会继续执行接下来的语句。await直接返回结果,也可以用then处理。
- 使用trycatch捕捉异常
