# safemap

Safely get value with Type from JSON map. Will return `null` value when value was wrong.


# Feature
- [x] **安全取值**：可以从Map中连续使用`[]`操作符取值，任何错误取值都会返回`null`而不会报错。
- [x] **安全的嵌套Map**：你可以轻松取出深度嵌套Map中的数据，因为即使对Value为`null`的SafeMap使用`[]`操作符，也只会返回一个新的`SafeMap(null)`对象。
- [x] **按类型取值**：支持直接取出期望类型的数据，类型不正确就会返回`null`而不会报错。
- [x] **类似Js的空值判断**：通过调用`isEmpty()`方法，空数组，空字典，空字符串或0都会返回true，帮助你快速判断空值。

## Getting Started

```dart
test('get value from safemap', () {
    // source map
    Map map = {
      'id': 3,
      'tag': 'student',
      'info': {
        'name': 'Jerry',
      },
      'class': [
        {
          "name": 'class 1',
          'tag': '',
        },
        {},
      ],
    };
    SafeMap safeMap = SafeMap(map);

    // 取值,错误的类型会返回SafeMap(null)
    assert(safeMap['id'].value == 3);
    assert(safeMap['id'].string == null);

    // 错误的下标也会返回SafeMap(null)
    assert(safeMap['tag'].value == 'student');
    assert(safeMap['tag12345'].value == null);

    // 连续取值,可以一直安全取值,只会返回SafeMap(null).
    assert(safeMap['info']['name'].value == 'Jerry');
    assert(safeMap['a']['b']['b']['b']['b']['b'].value == null);

    // 取出数组，也可以通过数组下标继续取值
    assert(safeMap['class'].list.length == 2);
    assert(safeMap['class'][0]['name'].value == 'class 1');

    // {},[],0,'',null 都会被判断为空
    assert(safeMap['class'][0]['tag'].isEmpty());
    assert(safeMap['class'][1].isEmpty());

    // 越界也会返回SafeMap(null)，判断isEmpty为true
    assert(safeMap['class'][2].isEmpty());
  });
```
