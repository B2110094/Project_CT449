<script>
import ProductService from '../services/Product.service';
import StoreService from '../services/Store.service';
import SliderIProduct from '../components/SliderProduct.vue'

export default {
    components: {
        SliderIProduct
    },
    data() {
        return {
            ProductData: [],
            ProductDataSort: [],
            SellquantityProduct: []
        }
    },
    methods: {
        async getDataProduct() {
            try {
                this.ProductData = await ProductService.getProductLimit();
            } catch (error) {
                console.log(error)
            }
        },
        async getProductDataSort() {
            try {
                this.ProductDataSort = await StoreService.getStoreSort();
                console.log(this.ProductDataSort)
            } catch (err) {
                console.log(err);
            }
        },
    },
    mounted() {
        this.getDataProduct();
        this.getProductDataSort();
    },

}
</script>

<template>
    <div class="container" id="main_page">
        <!-- Slider Image -->
        <SliderIProduct></SliderIProduct>

        <!-- Main_Content_Product-->
        <div class="row mt-5 item_product">
            <h4> <i class="fa-solid fa-fire"></i> SẢN PHẨM BÁN CHẠY</h4>
            <div class="col-lg-3" v-for="item in ProductDataSort">

                <div data-aos="zoom-out-left" class="card" style="width: 18rem;">
                    <img :src="item.sanphamdata.img_url[0]" class="card-img-top" alt="..." width="190" height="190" style="object-fit: contain;">
                    <div class="card-body">
                        <span class="card-title" style="height:48px">{{ item.sanphamdata.title }}</span>

                        <p style="font-weight:bold">Đã bán:
                            <button class="button-88" role="button">{{ item.soluongSP }} sản phẩm</button>  
                        </p>

                        <p class="card-text"><span class="fw-bold"> Giá bán:</span> <span class="text-danger fw-bold"> {{ item.sanphamdata.price.toLocaleString() }} đ</span></p>
                        <router-link :to="{
                            name: 'Details',
                            params: { id: item.sanphamdata._id },
                        }">
                            <button type="button" class="btn" id="btn_detail">Xem chi tiết</button>
                        </router-link>
                    </div>
                </div>
                <p>{{ item.id_product }}</p>
            </div>
        </div>


        <!-- Img_Banner_Adv   -->
        <div class="row container mt-5">
            <div class="col" data-aos="fade-up" data-aos-anchor-placement="top-bottom">
                <img src="https://htmldemo.net/pustok/pustok/image/bg-images/promo-banner-with-text.jpg" class="img-fluid" alt="..." width="100%">
            </div>
            <div class="col" data-aos="fade-up" data-aos-anchor-placement="top-bottom">
                <img src="https://htmldemo.net/pustok/pustok/image/bg-images/promo-banner-with-text-2.jpg" class="img-fluid" alt="..." width="100%">
            </div>
        </div>

        <div class="row">
            <div class="col">
                <div class="row mt-5 item_product" style="margin-right:10px;">
                    <h4><i class=""></i> Sách Ngoại Ngữ</h4>
                    <div class="col-lg-6 mt-3" v-for="item in ProductData" v-show="item.categories === 'Sách Ngoại Ngữ'">
                        <div class="card" style="width: 18rem;" data-aos="zoom-in-down">
                            <img :src="item.img_url[0]" class="card-img-top" alt="..." width="190" height="190" style="object-fit: contain;">
                            <div class="card-body">
                                <span class="card-title" style="height:48px">{{ item.title }}</span>
                                <p class="card-text"><span class="fw-bold"> Giá bán:</span> <span class="text-danger fw-bold"> {{ item.price.toLocaleString() }} đ</span></p>
                                <router-link :to="{
                                    name: 'Details',
                                    params: { id: item._id },
                                }">
                                    <button type="button" class="btn" id="btn_detail">Xem chi tiết</button>
                                </router-link>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
            <div class="col">
                <div class="row mt-5 item_product">
                    <h4><i class=""></i> Sách Thiếu Nhi</h4>
                    <div class="col-lg-6 mt-3" v-for="item in ProductData" v-show="item.categories === 'Sách Thiếu Nhi'">
                        <div class="card" style="width: 18rem;" data-aos="zoom-in-down">
                            <img :src="item.img_url[0]" class="card-img-top" alt="..." width="190" height="190" style="object-fit: contain;">
                            <div class="card-body">
                                <span class="card-title" style="height:48px">{{ item.title }}</span>
                                <p class="card-text"><span class="fw-bold"> Giá bán:</span> <span class="text-danger fw-bold"> {{ item.price.toLocaleString() }} đ</span></p>
                                <router-link :to="{
                                    name: 'Details',
                                    params: { id: item._id },
                                }">
                                    <button type="button" class="btn" id="btn_detail">Xem chi tiết</button>
                                </router-link>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<style>
#main_page {
    height: 100%;
}

.item_product h4 {
    background-color: red;
    border-radius: 5px;
    text-align: center;
    color: white;
    padding: 5px;
    margin-bottom: 19px;
}

.item_product {
    border: 1.5px solid red;
    border-radius: 5px;
    padding: 5px;
}

.card-title {
    overflow: hidden;
    text-overflow: ellipsis;
    display: -webkit-box;
    -webkit-line-clamp: 2;
    line-clamp: 2;
    -webkit-box-orient: vertical;
}

#btn_detail {
    background-color: red;
    width: 100%;
    font-weight: bold;
    color: white;
}

/* CSS */
.button-88 {
    display: flex;
    align-items: center;
    font-family: inherit;
    font-weight: 500;
    font-size: 16px;
    padding: 0.7em 1.4em 0.7em 1.1em;
    color: white;
    background: #ad5389;
    background: linear-gradient(0deg, rgb(81, 20, 167) 0%, rgb(102, 162, 247) 100%);
    border: none;
    box-shadow: 0 0.7em 1.5em -0.5em #14a73e98;
    letter-spacing: 0.05em;
    border-radius: 20em;
    cursor: pointer;
    user-select: none;
    -webkit-user-select: none;
    touch-action: manipulation;
}

.button-88:hover {
    box-shadow: 0 0.5em 1.5em -0.5em #14a73e98;
}

.button-88:active {
    box-shadow: 0 0.3em 1em -0.5em #14a73e98;
}
</style>