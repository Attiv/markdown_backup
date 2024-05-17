```Plain
state.count.count = state.count.count + amount;
state.count = Object.assign({},state.count)
```

或

%60%60%60%0Astate.count.count%20%3D%20state.count.count%20%2B%20amount%3B%0Astate.count%20%3D%20Object.assign(%7B%7D%2Cstate.count)%0A%60%60%60%0A%0A%E6%88%96%0A%60%60%60%0Aconst%20mutations%20%3D%20%7B%0A%20%20INCREMENT(state%2C%20amount)%20%7B%0A%20%20%20%20if%20(!state.count.count)%20%7B%0A%20%20%20%20%20%20Vue.set(state.count%2C%20'count'%2C%200)%3B%0A%20%20%20%20%7D%0A%20%20%20%20state.count.count%20%3D%20state.count.count%20%2B%20amount%3B%0A%20%20%7D%2C%0A%7D%3B%0A%60%60%60