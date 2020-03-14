# vue-gallerybox

## Install

#### NPM

Install the package:

```
npm i vue-gallerybox
```

## Usage

How to use:
data it's array of images, col it's class bootstrap np: col-md-4 || another css class

```html
<gallery v-bind:images="gal" v-bind:column="'some-class'" />
```

`images` has the structure:

```javascript
import Gallery from 'vue-gallerybox'

export default {
  props: ['data'],
  components: {
    gallery: Gallery
  },
  data () {
    return {
      gal: [
        {
          thumb: "",		//thumb src
          img: ""			//image src
          description: ''	//description
        },
        {
          thumb:  "",
          img:  "",
          description: ''
        }
      ]
    }
  },
  methods: {}
}
```
