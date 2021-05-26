<template>
  <div class="yellow lighten-3 pa-3">
    <h3>회원 정보를 수정할 수 있습니다.</h3>
    <p>수정사항</p>
    <v-text-field
      label="이름"
      v-model="user.name"
    ></v-text-field>
    <v-text-field
        label="주소"
        v-model="user.address"
    ></v-text-field>
    <v-text-field
        label="전화번호"
        v-model="user.phone"
    ></v-text-field>
    <v-radio-group v-model="user.hasDog">
      <v-radio
        label="반려견 있음"
        :value="true"
      ></v-radio>
      <v-radio
          label="반려견 없음"
          :value="false"
      ></v-radio>
    </v-radio-group>
    <v-btn @click="changUser">수정 완료</v-btn>
  </div>
</template>

<script>
import { eventBus} from "../main";

export default {
    props: ["name", "address", "phone", "hasDog"],
    data() {
      return {
        user: {} // user 오브젝트 생성
      }
    },
    created() { // user 오브젝트에 값 저장
      this.user.name=this.name
      this.user.address=this.address
      this.user.phone=this.phone
      this.user.hasDog=this.hasDog
    },
    methods: {
      changUser() {
        this.$emit("child", this.user) // User.vue에 @child
        eventBus.$emit("userWasEdited", new Date()) // eventBus(부모)에 신호르 보내면 UserDetail.vue에 있는 eventBus.$on이 받는다.
        // $emit는 자식이 부모에게 신호를 보내는 것
      }
    }
  }
</script>
