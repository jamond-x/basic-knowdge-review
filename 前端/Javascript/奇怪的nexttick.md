```vue
setTimeout(() => {
      console.log(5555)
    }, 0)
    void nextTick(() => {
      console.log(3333)
    })
    setTimeout(() => {
      console.log(4444)
    }, 0)
    queueMicrotask(() => {
      console.log(2222)
    })
    console.log(1111)

1111
2222
3333
5555
4444
```

