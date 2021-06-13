<template>
  <div class="validate-input-container pd-3">
    <input type="text" class="form-control" :class="{'is-invalid': inputRef.error}" id="exampleInputEmail1" v-model="inputRef.val" @blur="validateInput">
    <span v-if="inputRef.error" class="invalid-feedback">{{inputRef.message}}</span>
  </div>
</template>

<script lang="ts">
import { defineComponent, reactive, PropType } from 'vue'
const emailReg = /^\w{3,}(\.\w+)*@[A-z0-9]+(\.[A-z]{2,5}){1,2}$/
interface RuleProp {
  type: 'required' | 'email';
  message: string;
}
export type RulesProp = RuleProp[]
export default defineComponent({
  name: "ValidateInput",
  props: {
    rules: Array as PropType<RulesProp>
  },
  setup (props) {
    const inputRef = reactive({
      val: '',
      error: false,
      message: ''
    })
    const validateInput = () => {
      if (props.rules) {
        // every 可以逐个判断，只有有一个是false就返回false，全true才会返回true
        const allPassed = props.rules.every(rule => {
          let passed = true
          inputRef.message = rule.message
          switch (rule.type) {
            case 'required':
              passed = (inputRef.val.trim() !== '')
              break
            case 'email':
              passed = emailReg.test(inputRef.val)
              break
            default:
              break
          }
          return passed
        })
        inputRef.error  = !allPassed
      }
    }

    return {
      inputRef,
      validateInput
    }
  }
})
</script>

<style scoped>

</style>
