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

> Please noted that if you want to set width, just set css style to the component's parent. This component is a `block` hence it will extend itself to fullfill it's parent width.

#### Config height

Set an exact height by `height-limit`, the unit is `px`. Default height limit is none, height is auto. 

```vue
<snapshot-compare
  :bottom-image="bottomImage"
  :cover-image="coverImage"
  :height-limit="300"></snapshot-compare>
```

#### Config seperator style

Set seperator style by `seperator`. Valid values are `slash` and `vertical`, default value is `slash`. 

```vue
<snapshot-compare
  :bottom-image="bottomImage"
  :cover-image="coverImage"
  :seperator="'vertical'"></snapshot-compare>
```

#### Config seperator color

Set seperator color by `seperator-color`. Valid value accept all valid css values(e.g. `red`, `#fff`, `transparent`). Default value is `#fff`. 

```vue
<snapshot-compare
  :bottom-image="bottomImage"
  :cover-image="coverImage"
  :seperator-color="'red'"></snapshot-compare>
```

#### Config seperator initial position

Set initial seperator position by `position`. Valid values are numbers between `0~1`( `0` stands for left edge while `1` stands for right edge). Default value is `0.5` which means middle. 

```vue
<snapshot-compare
  :bottom-image="bottomImage"
  :cover-image="coverImage"
  :position="0.75"></snapshot-compare>
```

