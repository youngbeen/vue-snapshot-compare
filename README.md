[toc]

## [@youngbeen/vue-snapshot-compare](https://www.npmjs.com/package/@youngbeen/vue-snapshot-compare)

A vue component of comparing snapshots. See [demo](https://youngbeen.github.io/index/index.html#/workitcompare)

### Features

* Supports local and remote images
* All configs are optional, easy to use
* Customize width and height
* Customize seperator line style and color
* Customize default seperator line position

### Install

```shell
npm install @youngbeen/vue-snapshot-compare
```

### Usage

in script
```javascript
import SnapshotCompare from '@youngbeen/vue-snapshot-compare'
import coverImage from '@/your/local/image'
...

components: {
  SnapshotCompare
},
  
data () {
  return {
    coverImage: coverImage,
    bottomImage: 'https://example.com/some_remote_image.png'
  }
}
```

in template

```vue
<snapshot-compare
  :bottom-image="bottomImage"
  :cover-image="coverImage"></snapshot-compare>
```

That's all!



### API config

You can customize some config via `props`

> Please noted that if you want to set width, just set css style to the component's parent. This component is a `block` hence it will extend to fullfill it's parent width.

#### Config height

You can set an exact height by `heightLimit`, the unit is `px`. Default height limit is none, height is auto. 

```vue
<snapshot-compare
  :bottom-image="bottomImage"
  :cover-image="coverImage"
  :heightLimit="300"></snapshot-compare>
```

#### Config seperator style

You can set seperator style by `seperator`. Valid values are `slash` and `vertical`, default value is `slash`. 

```vue
<snapshot-compare
  :bottom-image="bottomImage"
  :cover-image="coverImage"
  :seperator="'vertical'"></snapshot-compare>
```

#### Config seperator color

You can set seperator color by `seperatorColor`. Valid value accept all valid css values(e.g. `red`, `#fff`, `transparent`). Default value is `#fff`. 

```vue
<snapshot-compare
  :bottom-image="bottomImage"
  :cover-image="coverImage"
  :seperatorColor="'red'"></snapshot-compare>
```

#### Config seperator initial position

You can set initial seperator position by `position`. Valid values are numbers between `0~1`( `0` stands for left edge while `1` stands for right edge). Default value is `0.5` which means middle. 

```vue
<snapshot-compare
  :bottom-image="bottomImage"
  :cover-image="coverImage"
  :position="0.75"></snapshot-compare>
```

