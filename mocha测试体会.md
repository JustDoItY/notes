# mocha 测试库的使用

## 错误promise异步测试

- 当出现异常，或者出现被promise直接reject掉。done函数（需要传入），就会发出错误，mocha可以捕捉。把这次测试归为失败。
- promise的reject会在then的第二个函数内处理，当遇到unhand的错误时，catch会进行处理，在then的函数内部出现运行错误，也会跳转到catch进行处理，相当于trycatch。如果不指定then的第二个函数，就会跳转到catch处理，catch中出现错误，就会出现unhand的错误，直接报错。
- 如果跳转到catch中，使用done处理，就会找不到done的情况，除非在it和describe中都引入done

## 正确promise异步测试

- 当处理promise等异步处理的时候，使用async函数去处理，会获得想要的结果。一个例子

      describe('测试全部resolve', () => {
        it("返回['success1', 'success2']", async () => {
          await promiseAll([
            delay(100, 'success1'),
            delay(50, 'success2'),
          ]).then((res) => {
            assert.deepEqual(res, ['success2', 'success1']);
          }, (err) => {
            assert.fail();
          })
        })
        });
