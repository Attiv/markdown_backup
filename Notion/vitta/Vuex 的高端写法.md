在 vuex文件里写:

```Plain
import _ from 'lodash'
import { request } from '../common'

const mutations = {
  update (state, o) {
    _.assignIn(state, o)
  }
}

export default {
  namespaced: true,

  state: {
    applied: []
  },

  mutations,

  actions: {
    async reloadApplied ({ commit }) {
      const resp = await request(`mobile/api/my-events`)
      if (resp.success) {
        commit('update', {
          applied: resp.data
        })
      }
    }
  }
}
```

要执行action里面的方法:`this.$store.dispatch('vuex文件/reloadApplied')`

---

（未严重理解是否正确）  
在一个js文件里写:  

```Plain
function bindState (module, field, newField = null) {
  newField = newField || field
  const o = {}
  o[newField] = {
    get () {
      return store.state[module][field]
    },
    set (value) {
      const n = {}
      n[field] = value
      store.commit(`${module}/update`, n)
    }
  }
  return o
}
```

在 vue文件里:

```Plain
computed: {
// ...表示把后面的zhi
    ...bindState('Record', 'filter'),
}
```

%E5%9C%A8%20vuex%E6%96%87%E4%BB%B6%E9%87%8C%E5%86%99%3A%0A%60%60%60%0Aimport%20_%20from%20'lodash'%0Aimport%20%7B%20request%20%7D%20from%20'..%2Fcommon'%0A%0Aconst%20mutations%20%3D%20%7B%0A%20%20update%20(state%2C%20o)%20%7B%0A%20%20%20%20_.assignIn(state%2C%20o)%0A%20%20%7D%0A%7D%0A%0Aexport%20default%20%7B%0A%20%20namespaced%3A%20true%2C%0A%0A%20%20state%3A%20%7B%0A%20%20%20%20applied%3A%20%5B%5D%0A%20%20%7D%2C%0A%0A%20%20mutations%2C%0A%0A%20%20actions%3A%20%7B%0A%20%20%20%20async%20reloadApplied%20(%7B%20commit%20%7D)%20%7B%0A%20%20%20%20%20%20const%20resp%20%3D%20await%20request(%60mobile%2Fapi%2Fmy-events%60)%0A%20%20%20%20%20%20if%20(resp.success)%20%7B%0A%20%20%20%20%20%20%20%20commit('update'%2C%20%7B%0A%20%20%20%20%20%20%20%20%20%20applied%3A%20resp.data%0A%20%20%20%20%20%20%20%20%7D)%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A%0A%60%60%60%0A%0A%E8%A6%81%E6%89%A7%E8%A1%8Caction%E9%87%8C%E9%9D%A2%E7%9A%84%E6%96%B9%E6%B3%95%3A%0A%60this.%24store.dispatch('vuex%E6%96%87%E4%BB%B6%2FreloadApplied')%60%0A%0A----%0A%EF%BC%88%E6%9C%AA%E4%B8%A5%E9%87%8D%E7%90%86%E8%A7%A3%E6%98%AF%E5%90%A6%E6%AD%A3%E7%A1%AE%EF%BC%89%0A%E5%9C%A8%E4%B8%80%E4%B8%AAjs%E6%96%87%E4%BB%B6%E9%87%8C%E5%86%99%3A%0A%60%60%60%0Afunction%20bindState%20(module%2C%20field%2C%20newField%20%3D%20null)%20%7B%0A%20%20newField%20%3D%20newField%20%7C%7C%20field%0A%20%20const%20o%20%3D%20%7B%7D%0A%20%20o%5BnewField%5D%20%3D%20%7B%0A%20%20%20%20get%20()%20%7B%0A%20%20%20%20%20%20return%20store.state%5Bmodule%5D%5Bfield%5D%0A%20%20%20%20%7D%2C%0A%20%20%20%20set%20(value)%20%7B%0A%20%20%20%20%20%20const%20n%20%3D%20%7B%7D%0A%20%20%20%20%20%20n%5Bfield%5D%20%3D%20value%0A%20%20%20%20%20%20store.commit(%60%24%7Bmodule%7D%2Fupdate%60%2C%20n)%0A%20%20%20%20%7D%0A%20%20%7D%0A%20%20return%20o%0A%7D%0A%60%60%60%0A%E5%9C%A8%20vue%E6%96%87%E4%BB%B6%E9%87%8C%3A%0A%0A%60%60%60%0Acomputed%3A%20%7B%0A%2F%2F%20...%E8%A1%A8%E7%A4%BA%E6%8A%8A%E5%90%8E%E9%9D%A2%E7%9A%84%E5%80%BC%E5%B1%95%E5%BC%80%0A%20%20%20%20...bindState('Record'%2C%20'filter')%2C%0A%7D%0A%60%60%60