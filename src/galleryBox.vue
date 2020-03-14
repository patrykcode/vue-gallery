<template>
    <div class="gallery-box" v-if="images">
        <div v-bind:class="classAdd()" v-for="image,index in images" v-bind:key="index" class="">
            <a v-bind:href="image.img" v-on:click="popup(index,$event)">
                <img v-bind:src="image.thumb" alt="" class="img-fluid">
                <div v-if="image.description" class="my-3" v-html="image.description"></div>
            </a>
        </div>
        <div class="popup" v-if="showPopup" v-on:click.self="closePop($event)">
            <div class="popup-img" v-if="imagePopup.img">
                <button class="navPop prev" v-on:click="prev">
                    <svg fill="white" x="0px" y="0px" width="100%" height="100%" viewBox="0 0 512 512">
                        <path d="M213.7,256L213.7,256L213.7,256L380.9,81.9c4.2-4.3,4.1-11.4-0.2-15.8l-29.9-30.6c-4.3-4.4-11.3-4.5-15.5-0.2L131.1,247.9 c-2.2,2.2-3.2,5.2-3,8.1c-0.1,3,0.9,5.9,3,8.1l204.2,212.7c4.2,4.3,11.2,4.2,15.5-0.2l29.9-30.6c4.3-4.4,4.4-11.5,0.2-15.8 L213.7,256z"></path>
                    </svg>
                </button>
                <button class="navPop next" v-on:click="next">
                    <svg fill="white" x="0px" y="0px" width="100%" height="100%" viewBox="0 0 512 512" xml:space="preserve">
                        <path d="M298.3,256L298.3,256L298.3,256L131.1,81.9c-4.2-4.3-4.1-11.4,0.2-15.8l29.9-30.6c4.3-4.4,11.3-4.5,15.5-0.2l204.2,212.7 c2.2,2.2,3.2,5.2,3,8.1c0.1,3-0.9,5.9-3,8.1L176.7,476.8c-4.2,4.3-11.2,4.2-15.5-0.2L131.3,446c-4.3-4.4-4.4-11.5-0.2-15.8 L298.3,256z"></path>
                    </svg>
                </button>
                <div class="popup-content">
                    <div>
                        <button class="btn-close-pop" v-on:click="closePop($event)">
                            <svg fill="white" x="0px" y="0px" width="100%" height="100%" viewBox="0 0 512 512">
                                <path d="M443.6,387.1L312.4,255.4l131.5-130c5.4-5.4,5.4-14.2,0-19.6l-37.4-37.6c-2.6-2.6-6.1-4-9.8-4c-3.7,0-7.2,1.5-9.8,4 L256,197.8L124.9,68.3c-2.6-2.6-6.1-4-9.8-4c-3.7,0-7.2,1.5-9.8,4L68,105.9c-5.4,5.4-5.4,14.2,0,19.6l131.5,130L68.4,387.1 c-2.6,2.6-4.1,6.1-4.1,9.8c0,3.7,1.4,7.2,4.1,9.8l37.4,37.6c2.7,2.7,6.2,4.1,9.8,4.1c3.5,0,7.1-1.3,9.8-4.1L256,313.1l130.7,131.1 c2.7,2.7,6.2,4.1,9.8,4.1c3.5,0,7.1-1.3,9.8-4.1l37.4-37.6c2.6-2.6,4.1-6.1,4.1-9.8C447.7,393.2,446.2,389.7,443.6,387.1z"></path>
                            </svg>
                        </button>
                    </div>
                    <div class=""><img v-bind:src="imagePopup.img" alt=""></div>
                    <div class="desc-box" v-if="imagePopup.description" v-html="imagePopup.description"></div>
                    <div class="index-nr"><span class="">{{imagePopup.index + 1 + ' / ' + counter}}</span></div>
                </div>
            </div>
            <div class="popup-thumbs">
                <button class="navPop prev small-pop" v-on:click="prev">
                    <svg fill="white" x="0px" y="0px" width="100%" height="100%" viewBox="0 0 512 512">
                        <path d="M213.7,256L213.7,256L213.7,256L380.9,81.9c4.2-4.3,4.1-11.4-0.2-15.8l-29.9-30.6c-4.3-4.4-11.3-4.5-15.5-0.2L131.1,247.9 c-2.2,2.2-3.2,5.2-3,8.1c-0.1,3,0.9,5.9,3,8.1l204.2,212.7c4.2,4.3,11.2,4.2,15.5-0.2l29.9-30.6c4.3-4.4,4.4-11.5,0.2-15.8 L213.7,256z"></path>
                    </svg>
                </button>
                <button class="navPop next small-pop" v-on:click="next">
                    <svg fill="white" x="0px" y="0px" width="100%" height="100%" viewBox="0 0 512 512" xml:space="preserve">
                        <path d="M298.3,256L298.3,256L298.3,256L131.1,81.9c-4.2-4.3-4.1-11.4,0.2-15.8l29.9-30.6c4.3-4.4,11.3-4.5,15.5-0.2l204.2,212.7 c2.2,2.2,3.2,5.2,3,8.1c0.1,3-0.9,5.9-3,8.1L176.7,476.8c-4.2,4.3-11.2,4.2-15.5-0.2L131.3,446c-4.3-4.4-4.4-11.5-0.2-15.8 L298.3,256z"></path>
                    </svg>
                </button>
                <div class="popupThumbs" v-for="image,index in images" v-bind:style="{'background-image': 'url('+image.thumb+')'}" v-on:click="popup(index,$event)" v-bind:class="{'active':index==imagePopup.index}" v-if="thumb(index)">

                </div>
            </div>
        </div>
    </div>
</template>

<script>
    export default {
        name: 'gallery',
        props: ['images', 'column', 'autopopup'],
        data() {
            return {
                showPopup: false,
                imagePopup: {
                    index: null,
                    thumb: null,
                    img: null,
                    description: null,
                    link: null,
                },
                counter: this.images && this.images.length !== undefined ? this.images.length : 0,
            }
        },
        created() {
            if (this.autopopup) {
                console.log('auto')
                this.popup(0)
            }
        },
        methods: {
            classAdd() {
                return this.column;
            },
            popup(id = 0, e = null) {
                if (e) {
                    e.preventDefault();
                }
                this.showPopup = true;
                var thumb = this.images[id].thumb ? this.images[id].thumb : null;
                var img = this.images[id].img ? this.images[id].img : null;
                var description = this.images[id].description ? this.images[id].description : null;
                var link = this.images[id].link ? this.images[id].link : null;

                this.imagePopup = {
                    index: id,
                    thumb: thumb,
                    img: img,
                    description: description,
                    link: link,
                };
            },
            prev() {
                var curentIndex = this.imagePopup.index - 1;
                var index = curentIndex < 0 ? this.images.length - 1 : curentIndex;
                if (this.images[index] !== undefined) {
                    this.popup(index)
                }
            },
            next() {
                var curentIndex = this.imagePopup.index + 1;
                var index = curentIndex > this.images.length - 1 ? 0 : curentIndex;
                if (this.images[index] !== undefined) {
                    this.popup(index)
                }
            },
            thumb(index) {
                return index >= this.imagePopup.index - 3 &&
                    index <= this.imagePopup.index + 3
            },
            closePop(e) {
                e.stopPropagation();
                this.showPopup = false;
            }
        }
    }
</script>
<style scrope>
    .popup * {
        -webkit-transition: all .5s;
        -o-transition: all .5s;
        transition: all .5s;
    }

    .popup {
        position: fixed;
        width: 100%;
        height: 100%;
        top: 0;
        left: 0;
        z-index: 99999;
        text-align: center;
    }

    .popup:before {
        content: "";
        position: absolute;
        width: 100%;
        height: 100%;
        background: rgba(0, 0, 0, 0.8);
        top: 0;
        left: 0;
        z-index: -1;
    }

    .btn-close-pop {
        width: 20px;
        height: 20px;
        background: transparent;
        padding: 0;
        border: 0;
        float: right;
        margin: 10px 0;
    }

    .popupThumbs {
        width: 100px;
        height: 100px;
        float: left;
        margin: 10px;
        background-position: center;
        border-radius: 4px;
        background-size: auto 100px;
    }

    .popupThumbs.active {
        border: 2px solid #fff;
    }

    .popup-thumbs {
        max-width: 900px;
        margin: auto;
        height: 120px;
        bottom: 0;
        position: absolute;
        left: 0;
        right: 0;
        z-index: 9999;
        width: 100%;
        padding: 0px 90px;
    }

    .popup-content,
    .popup-img {
        position: relative;
        display: inline-block;
        vertical-align: middle;
        margin: 0 auto;
        text-align: left;
    }

    .popup-img {
        top: 50%;
        transform: translateY(-50%);
    }

    .popup-img img {
        max-width: 90vw;
        max-height: calc(100vh - 260px);
    }

    .navPop {
        position: fixed;
        top: 50%;
        transform: translateY(-50%);
        width: 55px;
        height: 55px;
        background: transparent;
        border: 0;
        z-index: 9999;
    }

    .navPop,
    .btn-close-pop {
        cursor: pointer;
    }

    .navPop:focus {
        outline: 0;
        outline: 0;
    }

    .navPop.prev {
        left: -66px;
    }

    .navPop.next {
        right: -66px;
    }

    .desc-box {
        position: absolute;
        right: 0;
        left: 0;
        bottom: 22px;
        background: #000000b0;
        color: #efefef;
        padding: 5px;
    }

    .desc-box p {
        margin: 0 !important;
        padding: 10px;
    }

    .index-nr {
        text-align: right;
        color: #bdbdbd;
    }

    .small-pop {
        position: absolute !important;
        width: 40px !important;
        height: 40px !important;
    }

    .popup-img h4 {
        padding: 10px;
        background: rgba(0, 0, 0, 0.8);
        bottom: -8px;
        color: #fff;
    }

    @media(max-width:992px) {
        .navPop.prev {
            left: 0;
        }

        .navPop.prev {
            left: 0;
        }

        .popup-thumbs {
            max-width: 100%;
            height: 70px;
            padding: 0px 40px;
        }

        .popupThumbs {
            width: 50px;
            height: 50px;
            margin: 5px;
            background-size: auto 50px;
        }
    }
</style>