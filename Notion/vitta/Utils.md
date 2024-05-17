_/**_

_* Created by jiachenpan on 16/11/18._

_*/_

export function parseTime(_time_, _cFormat_) {

if (arguments.length === 0) {

return null

}

const format = cFormat || '{y}-{m}-{d} {h}:{i}:{s}'

let date

if (typeof time === 'object') {

date = time

} else {

if (('' + time).length === 10) time = parseInt(time) * 1000

date = new Date(time)

}

const formatObj = {

y: date.getFullYear(),

m: date.getMonth() + 1,

d: date.getDate(),

h: date.getHours(),

i: date.getMinutes(),

s: date.getSeconds(),

a: date.getDay()

}

const time_str = format.replace(/{(y|m|d|h|i|s|a)+}/g, (_result_, _key_) => {

let value = formatObj[key]

_// Note: getDay() returns 0 on Sunday_

if (key === 'a') { return ['日', '一', '二', '三', '四', '五', '六'][value ] }

if (result.length > 0 && value < 10) {

value = '0' + value

}

return value || 0

})

return time_str

}

export function formatTime(_time_, _option_) {

time = +time * 1000

const d = new Date(time)

const now = Date.now()

const diff = (now - d) / 1000

if (diff < 30) {

return '刚刚'

} else if (diff < 3600) {

_// less 1 hour_

return Math.ceil(diff / 60) + '分钟前'

} else if (diff < 3600 * 24) {

return Math.ceil(diff / 3600) + '小时前'

} else if (diff < 3600 * 24 * 2) {

return '1天前'

}

if (option) {

return parseTime(time, option)

} else {

return (

d.getMonth() +

1 +

'月' +

d.getDate() +

'日' +

d.getHours() +

'时' +

d.getMinutes() +

'分'

)

}

}

_// 格式化时间_

export function getQueryObject(_url_) {

url = url == null ? window.location.href : url

const search = url.substring(url.lastIndexOf('?') + 1)

const obj = {}

const reg = /([^?&=]+)=([^?&=]*)/g

search.replace(reg, (_rs_, _$1_, _$2_) => {

const name = decodeURIComponent($1)

let val = decodeURIComponent($2)

val = String(val)

obj[name] = val

return rs

})

return obj

}

_/**_

_*get getByteLen_

_*_ _@param_ _{Sting}_ _val_ _input value_

_*_ _@returns_ _{number}_ _output value_

_*/_

export function getByteLen(_val_) {

let len = 0

for (let i = 0; i < val.length; i++) {

if (val[i].match(/[^\x00-\xff]/gi) != null) {

len += 1

} else {

len += 0.5

}

}

return Math.floor(len)

}

export function cleanArray(_actual_) {

const newArray = []

for (let i = 0; i < actual.length; i++) {

if (actual[i]) {

newArray.push(actual[i])

}

}

return newArray

}

export function param(_json_) {

if (!json) return ''

return cleanArray(

Object.keys(json).map(_key_ => {

if (json[key] === undefined) return ''

return encodeURIComponent(key) + '=' + encodeURIComponent(json[key])

})

).join('&')

}

export function param2Obj(_url_) {

const search = url.split('?')[1]

if (!search) {

return {}

}

return JSON.parse(

'{"' +

decodeURIComponent(search)

.replace(/"/g, '\\"')

.replace(/&/g, '","')

.replace(/=/g, '":"') +

'"}'

)

}

export function html2Text(_val_) {

const div = document.createElement('div')

div.innerHTML = val

return div.textContent || div.innerText

}

export function objectMerge(_target_, _source_) {

_/* Merges two objects,_

_giving the last one precedence */_

if (typeof target !== 'object') {

target = {}

}

if (Array.isArray(source)) {

return source.slice()

}

Object.keys(source).forEach(_property_ => {

const sourceProperty = source[property]

if (typeof sourceProperty === 'object') {

target[property] = objectMerge(target[property], sourceProperty)

} else {

target[property] = sourceProperty

}

})

return target

}

export function scrollTo(_element_, _to_, _duration_) {

if (duration <= 0) return

const difference = to - element.scrollTop

const perTick = (difference / duration) * 10

setTimeout(() => {

element.scrollTop = element.scrollTop + perTick

if (element.scrollTop === to) return

scrollTo(element, to, duration - 10)

}, 10)

}

export function toggleClass(_element_, _className_) {

if (!element || !className) {

return

}

let classString = element.className

const nameIndex = classString.indexOf(className)

if (nameIndex === -1) {

classString += '' + className

} else {

classString =

classString.substr(0, nameIndex) +

classString.substr(nameIndex + className.length)

}

element.className = classString

}

export const pickerOptions = [

{

text: '今天',

onClick(_picker_) {

const end = new Date()

const start = new Date(new Date().toDateString())

end.setTime(start.getTime())

picker.$emit('pick', [start, end])

}

},

{

text: '最近一周',

onClick(_picker_) {

const end = new Date(new Date().toDateString())

const start = new Date()

start.setTime(end.getTime() - 3600 * 1000 * 24 * 7)

picker.$emit('pick', [start, end])

}

},

{

text: '最近一个月',

onClick(_picker_) {

const end = new Date(new Date().toDateString())

const start = new Date()

start.setTime(start.getTime() - 3600 * 1000 * 24 * 30)

picker.$emit('pick', [start, end])

}

},

{

text: '最近三个月',

onClick(_picker_) {

const end = new Date(new Date().toDateString())

const start = new Date()

start.setTime(start.getTime() - 3600 * 1000 * 24 * 90)

picker.$emit('pick', [start, end])

}

}

]

export function getTime(_type_) {

if (type === 'start') {

return new Date().getTime() - 3600 * 1000 * 24 * 90

} else {

return new Date(new Date().toDateString())

}

}

export function debounce(_func_, _wait_, _immediate_) {

let timeout, args, context, timestamp, result

const later = function() {

_// 据上一次触发时间间隔_

const last = +new Date() - timestamp

_// 上次被包装函数被调用时间间隔last小于设定时间间隔wait_

if (last < wait && last > 0) {

timeout = setTimeout(later, wait - last)

} else {

timeout = null

_// 如果设定为immediate===true，因为开始边界已经调用过了此处无需调用_

if (!immediate) {

result = func.apply(context, args)

if (!timeout) context = args = null

}

}

}

return function(..._args_) {

context = _this_

timestamp = +new Date()

const callNow = immediate && !timeout

_// 如果延时不存在，重新设定延时_

if (!timeout) timeout = setTimeout(later, wait)

if (callNow) {

result = func.apply(context, args)

context = args = null

}

return result

}

}

_/**_

_* This is just a simple version of deep copy_

_* Has a lot of edge cases bug_

_* If you want to use a perfect deep copy, use lodash's _.cloneDeep_

_*/_

export function deepClone(_source_) {

if (!source && typeof source !== 'object') {

throw new Error('error arguments', 'shallowClone')

}

const targetObj = source.constructor === Array ? [] : {}

Object.keys(source).forEach(_keys_ => {

if (source[keys] && typeof source[keys] === 'object') {

targetObj[keys] = deepClone(source[keys])

} else {

targetObj[keys] = source[keys]

}

})

return targetObj

}

export function uniqueArr(_arr_) {

return Array.from(new Set(arr))

}