# safemap

Safely get value with Type from JSON map. Will return null value when value was wrong.

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
    assert(safeMap['id'].value == 3);
    assert(safeMap['id'].string == null);
    assert(safeMap['tag'].value == 'student');
    assert(safeMap['info']['name'].value == 'Jerry');
    assert(safeMap['class'].list.length == 2);
    assert(safeMap['class'][0]['name'].value == 'class 1');
    assert(safeMap['class'][0]['tag'].isEmpty());
    assert(safeMap['class'][1].isEmpty());
    assert(safeMap['class'][2].isEmpty());
  });
```
