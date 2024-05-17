- 具体文件
- inedx 文件

# 具体文件

```Plain
import _ from 'lodash'
import { request } from '../../common'
import eventBus from '../../eventBus'

const attrs = {
  'bus_id': 220,
  'no': 170,
  'register_at': 110,
  'category': null,
  'km_status': 110,
  'order_no': 170,
  'status': 170
}

const names = {
  'bus_id': 'Vehicle ID',
  'no': 'Event ID',
  'register_at': 'Date registered',
  'category': 'Category',
  'km_status': 'Km. stand',
  'order_no': 'Order number',
  'status': 'Status'
}

const defaults = [
  'bus_id', 'no', 'register_at',
  'category', 'km_status',
  'order_no', 'status'
]

const columns = {}
for (let key in attrs) {
  columns[key] = _.includes(defaults, key)
}

const rightAligns = ['km_status']

const fields = {}
for (let key in attrs) {
  fields[key] = {
    text: names[key],
    value: key,
    align: rightAligns.indexOf(key) >= 0 ? 'right' : 'left',
    sortable: false,
    width: attrs[key]
  }
}

const filterStatus = [
  {
    children: [
      {
        label: 'Open',
        value: 'open'
      },
      {
        label: 'Planned',
        value: 'planned'
      },
      {
        label: 'Rectified',
        value: 'rectified'
      },
      {
        label: 'Cancelled',
        value: 'cancelled'
      }
    ]
  }
]

const state = {
  other: false,
  inactive: false,
  filter: false,
  columns,
  fields,
  filterStatus
}

const mutations = {
  async update (state, o) {
    _.assignIn(state, o)
    if ('columns' in o) {
      let resp = await request('/n/update_user_meta', 'post', {
        componentColumns: o.columns
      })
      if (resp) {
        state.columns = o.columns
        eventBus.$emit('update-meta-component')
      }
    }
  }
}

const getters = {
}

const actions = {
}

export default {
  namespaced: true,
  state,
  mutations,
  getters,
  actions
}
```

# inedx 文件

> 用到了 vuex-persistedstate

```Plain
import Vue from 'vue'
import Vuex from 'vuex'
import createPersistedState from 'vuex-persistedstate'

import modules from './modules'

Vue.use(Vuex)

export default new Vuex.Store({
  modules,
  strict: process.env.NODE_ENV !== 'production',
  plugins: [
    createPersistedState({
      paths: [
        'BusMaster.other',
        'BusMaster.showInactive',
        'CompanyStructure.showInactive',
        'Config.locale',
        'Config.sidebar',
        'Config.fullscreen',
        'FleetRegister.inactive',
        'FleetRegister.other',
        'FleetRegister.filter',
        'FleetRegister.columns',
        'OrderHistory.inactive',
        'OrderHistory.other',
        'OrderHistory.filter',
        'OrderHistory.columns',
        'ComponentHistory.inactive',
        'ComponentHistory.other',
        'ComponentHistory.filter',
        'ComponentHistory.columns'
      ]
    })
  ]
})
```

%0A%0A%5Btoc%5D%0A%23%20%E5%85%B7%E4%BD%93%E6%96%87%E4%BB%B6%0A%60%60%60%0Aimport%20_%20from%20'lodash'%0Aimport%20%7B%20request%20%7D%20from%20'..%2F..%2Fcommon'%0Aimport%20eventBus%20from%20'..%2F..%2FeventBus'%0A%0Aconst%20attrs%20%3D%20%7B%0A%20%20'bus_id'%3A%20220%2C%0A%20%20'no'%3A%20170%2C%0A%20%20'register_at'%3A%20110%2C%0A%20%20'category'%3A%20null%2C%0A%20%20'km_status'%3A%20110%2C%0A%20%20'order_no'%3A%20170%2C%0A%20%20'status'%3A%20170%0A%7D%0A%0Aconst%20names%20%3D%20%7B%0A%20%20'bus_id'%3A%20'Vehicle%20ID'%2C%0A%20%20'no'%3A%20'Event%20ID'%2C%0A%20%20'register_at'%3A%20'Date%20registered'%2C%0A%20%20'category'%3A%20'Category'%2C%0A%20%20'km_status'%3A%20'Km.%20stand'%2C%0A%20%20'order_no'%3A%20'Order%20number'%2C%0A%20%20'status'%3A%20'Status'%0A%7D%0A%0Aconst%20defaults%20%3D%20%5B%0A%20%20'bus_id'%2C%20'no'%2C%20'register_at'%2C%0A%20%20'category'%2C%20'km_status'%2C%0A%20%20'order_no'%2C%20'status'%0A%5D%0A%0Aconst%20columns%20%3D%20%7B%7D%0Afor%20(let%20key%20in%20attrs)%20%7B%0A%20%20columns%5Bkey%5D%20%3D%20_.includes(defaults%2C%20key)%0A%7D%0A%0Aconst%20rightAligns%20%3D%20%5B'km_status'%5D%0A%0Aconst%20fields%20%3D%20%7B%7D%0Afor%20(let%20key%20in%20attrs)%20%7B%0A%20%20fields%5Bkey%5D%20%3D%20%7B%0A%20%20%20%20text%3A%20names%5Bkey%5D%2C%0A%20%20%20%20value%3A%20key%2C%0A%20%20%20%20align%3A%20rightAligns.indexOf(key)%20%3E%3D%200%20%3F%20'right'%20%3A%20'left'%2C%0A%20%20%20%20sortable%3A%20false%2C%0A%20%20%20%20width%3A%20attrs%5Bkey%5D%0A%20%20%7D%0A%7D%0A%0Aconst%20filterStatus%20%3D%20%5B%0A%20%20%7B%0A%20%20%20%20children%3A%20%5B%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20label%3A%20'Open'%2C%0A%20%20%20%20%20%20%20%20value%3A%20'open'%0A%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20label%3A%20'Planned'%2C%0A%20%20%20%20%20%20%20%20value%3A%20'planned'%0A%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20label%3A%20'Rectified'%2C%0A%20%20%20%20%20%20%20%20value%3A%20'rectified'%0A%20%20%20%20%20%20%7D%2C%0A%20%20%20%20%20%20%7B%0A%20%20%20%20%20%20%20%20label%3A%20'Cancelled'%2C%0A%20%20%20%20%20%20%20%20value%3A%20'cancelled'%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%5D%0A%20%20%7D%0A%5D%0A%0Aconst%20state%20%3D%20%7B%0A%20%20other%3A%20false%2C%0A%20%20inactive%3A%20false%2C%0A%20%20filter%3A%20false%2C%0A%20%20columns%2C%0A%20%20fields%2C%0A%20%20filterStatus%0A%7D%0A%0Aconst%20mutations%20%3D%20%7B%0A%20%20async%20update%20(state%2C%20o)%20%7B%0A%20%20%20%20_.assignIn(state%2C%20o)%0A%20%20%20%20if%20('columns'%20in%20o)%20%7B%0A%20%20%20%20%20%20let%20resp%20%3D%20await%20request('%2Fn%2Fupdate_user_meta'%2C%20'post'%2C%20%7B%0A%20%20%20%20%20%20%20%20componentColumns%3A%20o.columns%0A%20%20%20%20%20%20%7D)%0A%20%20%20%20%20%20if%20(resp)%20%7B%0A%20%20%20%20%20%20%20%20state.columns%20%3D%20o.columns%0A%20%20%20%20%20%20%20%20eventBus.%24emit('update-meta-component')%0A%20%20%20%20%20%20%7D%0A%20%20%20%20%7D%0A%20%20%7D%0A%7D%0A%0Aconst%20getters%20%3D%20%7B%0A%7D%0A%0Aconst%20actions%20%3D%20%7B%0A%7D%0A%0Aexport%20default%20%7B%0A%20%20namespaced%3A%20true%2C%0A%20%20state%2C%0A%20%20mutations%2C%0A%20%20getters%2C%0A%20%20actions%0A%7D%0A%0A%60%60%60%0A%0A%23%20inedx%20%E6%96%87%E4%BB%B6%0A%0A%3E%20%E7%94%A8%E5%88%B0%E4%BA%86%20%60vuex-persistedstate%60%0A%60%60%60%0Aimport%20Vue%20from%20'vue'%0Aimport%20Vuex%20from%20'vuex'%0Aimport%20createPersistedState%20from%20'vuex-persistedstate'%0A%0Aimport%20modules%20from%20'.%2Fmodules'%0A%0AVue.use(Vuex)%0A%0Aexport%20default%20new%20Vuex.Store(%7B%0A%20%20modules%2C%0A%20%20strict%3A%20process.env.NODE_ENV%20!%3D%3D%20'production'%2C%0A%20%20plugins%3A%20%5B%0A%20%20%20%20createPersistedState(%7B%0A%20%20%20%20%20%20paths%3A%20%5B%0A%20%20%20%20%20%20%20%20'BusMaster.other'%2C%0A%20%20%20%20%20%20%20%20'BusMaster.showInactive'%2C%0A%20%20%20%20%20%20%20%20'CompanyStructure.showInactive'%2C%0A%20%20%20%20%20%20%20%20'Config.locale'%2C%0A%20%20%20%20%20%20%20%20'Config.sidebar'%2C%0A%20%20%20%20%20%20%20%20'Config.fullscreen'%2C%0A%20%20%20%20%20%20%20%20'FleetRegister.inactive'%2C%0A%20%20%20%20%20%20%20%20'FleetRegister.other'%2C%0A%20%20%20%20%20%20%20%20'FleetRegister.filter'%2C%0A%20%20%20%20%20%20%20%20'FleetRegister.columns'%2C%0A%20%20%20%20%20%20%20%20'OrderHistory.inactive'%2C%0A%20%20%20%20%20%20%20%20'OrderHistory.other'%2C%0A%20%20%20%20%20%20%20%20'OrderHistory.filter'%2C%0A%20%20%20%20%20%20%20%20'OrderHistory.columns'%2C%0A%20%20%20%20%20%20%20%20'ComponentHistory.inactive'%2C%0A%20%20%20%20%20%20%20%20'ComponentHistory.other'%2C%0A%20%20%20%20%20%20%20%20'ComponentHistory.filter'%2C%0A%20%20%20%20%20%20%20%20'ComponentHistory.columns'%0A%20%20%20%20%20%20%5D%0A%20%20%20%20%7D)%0A%20%20%5D%0A%7D)%0A%0A%60%60%60%0A