

列表过滤器

## Simple Usage

```js
import { Filter } from 'saltui';

<Filter
  size={4}
  activeIndex={-1}
  defaultValue={{
    sort: [
      {
        text: '默认',
        value: ''
      },
    ]
  }}
  options={[
    {
      name: 'sort',     // 必选，过滤器唯一标志
      title: '默认排序', // 必选，过滤器名称
      type: 'order',  // 必选，过滤器类型(order|select|switch)
      items: [        // 可选，过滤器选项
        {
          text: '默认',
          value: ''
        },
        {
          text: '距离',
          value: 'distance'
        },
        {
          text: '评分',
          value: 'grade'
        }
      ]
    },
  ]}
  onChange={(data, filter) => {
    console.log(data)
  }}
  onConfirm={(data, filter) => {
    console.log(data)
  }}
  onReset={(data, filter) => {
    console.log(data)
  }}
>
```

## Props

#### className

描述：自定义的扩展样式名称

类型：String

默认：''

必填：否


#### size

描述：显示过滤器个数

类型：Number

默认：4

必填：否


#### defaultValue

描述：默认选择项

类型：Object

默认：{}

必填：否


#### options

描述：过滤器设置参数，数组中每个对象表示一个过滤器，顶部显示过滤器个数由size参数决定。

当过滤器个数超出size时，将会被自动归入到"高级筛选"过滤器。

类型：Array

默认：[]

必填：是


#### activeIndex

描述：默认激活的过滤器索引，-1 ~ (size - 1)

类型：number

默认：-1

必填：否


#### onChange

描述：当过滤项改变状态时即触发，不管是单选还是多选，适用于需要即时响应的场景

类型：Function

默认：(data, filter) => {// data中包含当前发生change的项以及change之后的所有选中项}

必填：否

#### onConfirm

描述：跟onChange的区别主要在于对多选过滤项的处理，如单选即时触发，如多选则会等待点击『确定』按钮后触发。
一般场景下推荐在本方法内处理过滤项的提交，除非需要实时更新（如处于高级筛选界面下点击筛选项时仍然需要更新列表）时才使用onChange

类型：Function

默认: (data, filter) => {// data中包含所有选中的筛选项}

必填：否

#### onReset

描述：当点击重置按钮时触发

类型：Function

默认：(data, filter) => {// data中包含所有被重置的过滤项名称以及重置后的所有选择项}

必填：否

## APIS

#### getValue([name])

描述：获取当前所有选中过滤项

参数：name 过滤器名称，可选。若为空，返回所有选中项；若为指定过滤器，则返回对应选中项

返回值：Object|Array，格式示例如下：

```javascript
// 若name不存在

result = {
   sort: [
     { text: '距离', value: '1000' }
   ],
   quickSort: [
     { text: '升序', value: 'asc' }
   ]
}


// 若name存在

result = [
  { text: '升序', value: 'asc' }
]
```

#### setValue(name, values)

描述：设置当前选中过滤项

参数：name 过滤器名称

参数：values 过滤器选中项

示例：
```javascript
filter.setValue('sort', [{text:'升序', value: 'asc'}])
```


#### clearValue([name])

描述：重置当前所有选中项

参数：name 过滤器名称，可选。存在时仅重置对应过滤器选中，省略时清空所有选中。

