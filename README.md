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
 <gallery v-bind:data="clearData(data)" v-bind:column="'col-md-4'"/>
```

`images` has the structure:
```javascript
  import Gallery from 'vue-gallerybox';    

    export default {
	props: ['data'],
	components: {
	    'gallery': Gallery
	},
	methods: {    
	    clearData(data) {
			var $data = [];
			if (data.images) {
						var items = data.images;
				for (var i in items) {
					var obj = {
						thumb: items[i].thumb,                 		//thumb src
						img: items[i].img,                          //image src
						description: '', 							//description
					}
					$data.push(obj);
				}
			}
			return {images: $data};
	    }
	}
    }
```
