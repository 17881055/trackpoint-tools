[![Build Status](https://travis-ci.org/Qquanwei/trackpoint-tools.svg?branch=master)](https://travis-ci.org/Qquanwei/trackpoint-tools)

# ���������������������ǵ��߼��ˣ�������Ҫ����ʲô

## trackpoint-tools

����߼������������Եģ�������Ҫ���������ֳ�ȥ��
���˵���es6,es7 �������ṩ�˿��ܡ�



## API �б�

���е�API������curryable, ���е�trackFn ������Ӱ�������߼�ִ�С�

### before(trackFn, fn)

```
import { before } from 'trackpoint-tools'

class SomeComponent {
    onClick = before((name) => console.log('seed some ', name))((name) => {
       // normal
       console.log('normal click ', name)
    })
}
```

onClick('me')

->

```
  seed some me
  normal click me
```

### after(trackFn, fn)

```
import { after } from 'trackpoint-tools'

class SomeComponent {
  onClick = after(() => console.log('send after'))(() => {
    // normal
    console.log('normal click')
  })
}
```

onClick

->

```
    normal click
    send after

```


Using Promise

```
import { after } from 'trackpoint-tools'

class SomeComponent {
    onClick = after(() => console.log('send after'))(() => {
         return ajax.post(...).then(() => {
             console.log('normal click')
         })
    })
}
```

onClick

->

```
    normal click
    send after

```

### once(fn)

same as lodash/once
[lodash/once](https://lodash.com/docs/4.17.4#once)


### track(fn)

����es7��decorator�᰸������������һ�ַǳ����ŵķ�ʽʹ�ø߽׺����� track��������ͨ��class������װ��decorator
ʹ�������ǳ���

babel plugin: https://github.com/loganfsmyth/babel-plugin-transform-decorators-legacy

```
class SomeComponent {
  @track(before(() => console.log('before')))
  onClick () {
    console.log('click')
  }

  @track(after(() => console.log('after')))
  onClickAjax () {
    return ajax.get(...').then(() => {
        console.log('request done')
    })
  }
}
```

->

```
 before
 click
```

->

```
 request done
 after
```

## ����

��ӭfork, ���µ��뷨����ֱ����PR
