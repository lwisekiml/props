<template>
  <div class="blue lighten-3 pa-3">
    <h1>User 컴포넌트</h1>
    <p>이름: 뷰제이에스</p>
    <p>{{ getDateAndTime(createAt) }}</p>
    {{helloToMixin}}
    <hr>
    <v-layout row wrap>
      <v-flex xs12 sm6>
        <UserDetail
          :name="name"
          :address="address"
          :phone="phone"
          :hasDog="hasDog"
        >
        </UserDetail>
      </v-flex>
      <v-flex xs12 sm6>
        <UserEdit
          :name="name"
          :address="address"
          :phone="phone"
          :hasDog="hasDog"
          @child="parents"
        ></UserEdit>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
import UserDetail from "./UserDetail.vue"
import UserEdit from "./UserEdit.vue"
import { dateFormat } from "../mixins/dateFormat";

export default {
  components: {
    UserDetail,
    UserEdit
  },
  data () {
    return {
      name: 'Hoza',
      address: 'Seoul',
      phone: '1234-5678',
      hasDog: true,
      createAt: null,
    }
  },
  computed: {
    helloToMixin() {
      return this.mixinData + " 안녕하세요" // 믹스인을 통해 컴포넌트에 들어간 함수, 값 등은 this를 통행 불러올 수 있다.
    }
  },
  created() {
    this.createAt = new Date()
  },
  methods : {
    parents(user) {
      // user = {name, address, phone, hasDog}
      this.name = user.name
      this.address = user.address
      this.phone = user.phone
      this.hasDog = user.hasDog
      console.log("부모가 받았어!")
    },
    getDateAndTime(date) { // editedDate가 null이므로 에러
      if(date !== null) {
        let hour = date.getHours()
        let minutes = date.getMinutes()
        let fullDate = `${date.getFullYear()}/${date.getMonth() + 1}/${date.getDate()}`
        return `${hour}:${minutes} ${fullDate}`
        // dateFormat.js 실행뒤 User.vue가 실행되어 이것이 출력된다.
      } else {
        return null
      }
    }
  },
  mixins: [dateFormat]
}
</script>