```js
function definePromiseAll(promises){
    let store = [...promises]
    let result = []
    return new Promise((rs, rj) => {
        store.forEach((el, index) => {
            Promise.resolve(el).then(res => {
                result.push(res)
                if(result.length === store.length){
                    rs(result)
                }
            })
            .catch(err => {
                rj(err)
            })
        })
    })    
}

const p1 = new Promise(rs => {
    setTimeout(() => {
        rs('p1 成功！')
    },1000)
})

const p2 = new Promise(rs => {
    setTimeout(() => {
        rs('p2 成功！')
    },500)
})

const p3 = new Promise((rs,rj) => {
    setTimeout(() => {
        rj("p3 rejected")
    }, 3500);
})

definePromiseAll([p1, p2, p3])
.then(res => {
    console.log(res);
})
.catch(err => {
    console.log(err);
})
```

