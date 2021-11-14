<template lang="pug">
  div
    h2 熱門景點
    Slider
    .tourism.row
      .tourism__search.col-md-3
        .input-group.mb-3.border.border--shadow.rounded
          input.form-control.border-0.bg-white(type="text" placeholder="關鍵字查詢" aria-label="關鍵字查詢" aria-describedby="button-addon2")
          button.btn.border-0.bg-white(type="button" id="button-addon2")
            img.search__icon(src="@/assets/img/icon/search.svg", alt="search")
        form.row.g-0.p-3.border.border--shadow.rounded
          span.h4.m-0.mb-3 篩選內容
          h2.text-primary.mb-2 地區/縣市
          .col-12.mb-2
            select(class="form-select" aria-label="tourism__areas" v-model="currentArea" @change="currentCity='All'")
              option(value="All") 全部
              option(v-for="(area,index) in areas" :key="'area'+index" :value="area.areaName") {{area.areaName}}
          .col-12
            select(class="form-select" aria-label="tourism__citys" v-model="currentCity" @change="getProducts")
              option(v-if="currentArea==='All'" value="All") 全部
              option(v-else selected disabled value="All") --請選擇--
              option(v-for="(city,index) in filterCitys" :key="'city'+index" :value="city.city") {{city.cityName}}
          .col-12.mb-3
            .border-bottom.border-2.border-info.py-2
          h2.text-primary.mb-2 類別
          .col-12.mb-3
            .form-check.mt-2
              input(class="form-check-input" type="radio" name="tourismType" id="typeAll" v-model="currentType" value="All")
              label(class="form-check-label" for="typeAll") 全部
            .form-check.mt-2(v-for="(item,index) in tourismType" :key="item.id")
              input(class="form-check-input" type="radio" name="tourismType" :id="item.id" v-model="currentType" :value="item.name")
              label(class="form-check-label" :for="item.id") {{item.name}}
          .col-12.d-flex.justify-content-center
            button(type="submit" class="btn btn-lg btn-warning text-light") SEARCH
      .tourism__content.col-md-9
        .d-flex.justify-content-end.mb-3
          button.btn.border.border--shadow.rounded.mt-4.mt-md-0(type="button" id="button-addon2")
              img.search__icon.me-2(src="@/assets/img/icon/arrangement.svg", alt="arrangement")
              span 排序：熱門度
        ul.tourism__group.ps-0.ms-md-4
          li.tourism__item.row.g-0.mb-5.border.border--shadow.rounded.overflow-hidden(v-for="tourism in filterTourismItem" :key="tourism.id")
            .tourism__img.col-md-4.img--mid.img--center(v-if="tourism.Picture.PictureUrl1" :style="{backgroundImage: `url(${tourism.Picture.PictureUrl1})`}")
            .tourism__img.col-md-4.img--mid.img--center.bg-info.d-flex.justify-content-center.align-items-center(v-else)
              p.h2 {{tourism.Name}}
            .tourism__txt.col-md-8.p-3.d-flex.flex-column.justify-content-between
              .tourism__txt__body
                h2.text-primary.d-flex.justify-content-between.align-items-center {{tourism.Name}}
                  span.badge.rounded-pill.bg-warning(v-if="tourism.Class1") {{tourism.Class1}}
                  span.badge.rounded-pill.bg-warning(v-else) 其他
                p.text-secondary.text--limit--3(:title="tourism.Description") {{tourism.Description}}
              .tourism__txt__footer.row.g-0.justify-content-between
                .icon.small.col-md-6.d-flex.align-items-center
                  img.me-2(src="@/assets/img/icon/site.svg", alt="site")
                  span.text--limit--1(:title="tourism.Address") {{tourism.Address}}
                .icon.small.col-md-6.d-flex.align-items-center.mt-2.mt-md-0
                  img.me-2(src="@/assets/img/icon/time.svg", alt="time")
                  span.text--limit--1(:title="tourism.OpenTime") {{tourism.OpenTime}}
</template>
<script>
import axios from 'axios'
import jsSHA from 'jssha'
import Slider from '@/components/Slider.vue'
export default {
  components: {
    Slider
  },
  layout: 'FrontEnd',
  data() {
    return {
      currentArea: 'All',
      currentCity: 'All',
      currentType: 'All',
      tourismItem: [],
      areas: [
        {
          areaName: '北部',
          citys: [
            {
              cityName: '臺北市',
              city: 'Taipei'
            },
            {
              cityName: '新北市',
              city: 'NewTaipei'
            },
            {
              cityName: '桃園市',
              city: 'Taoyuan'
            },
            {
              cityName: '基隆市',
              city: 'Keelung'
            },
            {
              cityName: '新竹市',
              city: 'Hsinchu'
            },
            {
              cityName: '新竹縣',
              city: 'HsinchuCounty'
            },
            {
              cityName: '宜蘭縣',
              city: 'YilanCounty'
            }
          ]
        },
        {
          areaName: '中部',
          citys: [
            {
              cityName: '臺中市',
              city: 'Taichung'
            },
            {
              cityName: '苗栗縣',
              city: 'MiaoliCounty'
            },
            {
              cityName: '彰化縣',
              city: 'ChanghuaCounty'
            },
            {
              cityName: '南投縣',
              city: 'NantouCounty'
            },
            {
              cityName: '雲林縣',
              city: 'YunlinCounty'
            }
          ]
        },
        {
          areaName: '南部',
          citys: [
            {
              cityName: '臺南市',
              city: 'Tainan'
            },
            {
              cityName: '高雄市',
              city: 'Kaohsiung'
            },
            {
              cityName: '嘉義縣',
              city: 'ChiayiCounty'
            },
            {
              cityName: '嘉義市',
              city: 'Chiayi'
            },
            {
              cityName: '屏東縣',
              city: 'PingtungCounty'
            }
          ]
        },
        {
          areaName: '東部',
          citys: [
            {
              cityName: '花蓮縣',
              city: 'HualienCounty'
            },
            {
              cityName: '臺東縣',
              city: 'TaitungCounty'
            }
          ]
        },
        {
          areaName: '離島',
          citys: [
            {
              cityName: '金門縣',
              city: 'KinmenCounty'
            },
            {
              cityName: '澎湖縣',
              city: 'PenghuCounty'
            },
            {
              cityName: '連江縣',
              city: 'LienchiangCounty'
            }
          ]
        }
      ],
      tourismType: [
        {
          name: '自然風景類',
          id: 'view'
        },
        {
          name: '文化類',
          id: 'history'
        },
        {
          name: '遊憩類',
          id: 'travel'
        },
        {
          name: '生態類',
          id: 'nature'
        },
        {
          name: '其他',
          id: 'others'
        }
      ]
    }
  },
  computed: {
    filterCitys() {
      const vm = this
      if (vm.currentArea === 'All') {
        let allCitys = []
        vm.areas.forEach((area) => {
          allCitys = allCitys.concat(area.citys)
        })
        return allCitys
      } else {
        const filterArea = vm.areas.find((area) => {
          return area.areaName === vm.currentArea
        })
        return filterArea.citys
      }
    },
    filterTourismItem() {
      const vm = this
      if (vm.currentType === 'All') {
        return vm.tourismItem
      } else if (vm.currentType === '其他') {
        return vm.tourismItem.filter((item) => {
          return !item.Class1
        })
      } else {
        return vm.tourismItem.filter((item) => {
          return item.Class1 === vm.currentType
        })
      }
    }
  },
  mounted() {
    this.getProducts()
  },
  methods: {
    getProducts(page = 1) {
      const vm = this
      let api = `${process.env.VUE_APP_APIPATH}/MOTC/v2/Tourism/ScenicSpot?$top=10&$format=JSON`
      if (vm.currentCity !== 'All') {
        api = `${process.env.VUE_APP_APIPATH}/MOTC/v2/Tourism/ScenicSpot/${vm.currentCity}?$top=10&$format=JSON`
      }

      axios
        .get(api, {
          headers: vm.getAuthorizationHeader()
        })
        .then(function(response) {
          vm.tourismItem = response.data
        })
        .catch(function(error) {
          alert(error)
        })
    },
    getAuthorizationHeader() {
      /* eslint-disable */
      const AppID = process.env.VUE_APP_ID
      const AppKey = process.env.VUE_APP_KEY
      const GMTString = new Date().toGMTString()
      const ShaObj = new jsSHA('SHA-1', 'TEXT')
      ShaObj.setHMACKey(AppKey, 'TEXT')
      ShaObj.update('x-date: ' + GMTString)
      const HMAC = ShaObj.getHMAC('B64')
      const Authorization =
        'hmac username="' +
        AppID +
        '", algorithm="hmac-sha1", headers="x-date", signature="' +
        HMAC +
        '"'
      return { Authorization, 'X-Date': GMTString }
    }
  }
}
</script>
