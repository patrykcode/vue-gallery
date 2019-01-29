# vue-gallerybox

## Install

#### NPM 

Install the package:

```
npm i vue-gallerybox
```
## Usage

How to use:
```html
 <gallery v-bind:data="clearData(data)" v-bind:col="4"/>
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
			    img: items[i].img,//image src
			    description: items[i].desc_one.description, // description
			    link: items[i].desc_one.link,//link
			}
			$data.push(obj);
		    }
		}
		return {images: $data};
	    }
	}
    }
```
