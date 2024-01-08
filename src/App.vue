<template>
  <div>
    <label> <input type="checkbox" v-model="includeNumbers" checked /> Включить цифры </label>
    <label>
      <input type="checkbox" v-model="includeLowercaseLetters" checked /> Включить строчные буквы
    </label>
    <label>
      <input type="checkbox" v-model="includeUppercaseLetters" checked /> Включить заглавные буквы
    </label>
    <label> <input type="checkbox" v-model="includeSymbols" checked /> Включить символы </label>
    <input type="number" v-model.number="passwordLength" min="1" placeholder="Длина пароля" />
    <button @click="generatePassword">Сгенерировать пароль</button>
    <p>Сгенерированный пароль: {{ password }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      includeNumbers: true,
      includeLowercaseLetters: true,
      includeUppercaseLetters: true,
      includeSymbols: true,
      passwordLength: 8,
      password: ''
    }
  },
  methods: {
    generatePassword() {
      const charset = []
      if (this.includeNumbers) {
        charset.push('0123456789')
      }
      if (this.includeLowercaseLetters) {
        charset.push('abcdefghijklmnopqrstuvwxyz')
      }
      if (this.includeUppercaseLetters) {
        charset.push('ABCDEFGHIJKLMNOPQRSTUVWXYZ')
      }
      if (this.includeSymbols) {
        charset.push('!@#$%^&*()')
      }

      const password = Array.from({ length: this.passwordLength }, () => {
        const randomIndex = Math.floor(Math.random() * charset.length)
        const randomCharSet = charset[randomIndex]
        const randomCharIndex = Math.floor(Math.random() * randomCharSet.length)
        return randomCharSet[randomCharIndex]
      }).join('')

      this.password = password
    }
  }
}
</script>
