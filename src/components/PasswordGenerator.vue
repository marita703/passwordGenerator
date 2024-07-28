<script setup>
import { ref } from 'vue'

const passwordLength = ref(12)

const includeUpperCase = ref(true)

const includeNumbers = ref(true)

const includeSymbols = ref(true)

const generatedPassword = ref('')

const generatePassword = () => {
  const lowercaseChars = 'abcdefghikmnlopqrstuvwxyz'
  const uppercaseChars = includeUpperCase.value ? 'ABCDEFGHIKMNLOPQRSTUVWXYZ' : ''
  const numberChars = includeNumbers.value ? '0123456789' : ''
  const symbolsChars = includeSymbols.value ? '!@#$%^&*()_+' : ''

  const allCharacters = lowercaseChars + uppercaseChars + numberChars + symbolsChars

  let password = ''

  for (let i = 0; i < passwordLength.value; i++) {
    const randomIndex = Math.floor(Math.random() * allCharacters.length)

    password += allCharacters[randomIndex]
  }

  generatedPassword.value = password
  console.log('password: ' + password)
  console.log('Genpassword: ' + generatedPassword.value)
}
</script>

<template>
  <div class="password-generator-container">
    <h2 class="password-generator-title">Password Generator</h2>
    <label for="length">Password length</label>
    <input type="number" id="lenght" v-model="passwordLength" min="4" max="32" />
    <br />
    <label for="includeUppercase">Include UpperCase</label>
    <input type="checkbox" id="includeUpperCase" v-model="includeUpperCase" />
    <br />
    <label for="includeNumbers">Include Numbers</label>
    <input type="checkbox" id="includeNumbers" v-model="includeNumbers" />
    <br />
    <label for="includeSymbols">Include Symbols</label>
    <input type="checkbox" id="includeSymbols" v-model="includeSymbols" />
    <br />

    <button @click="generatePassword" class="generated-button">Generate Password</button>

    <div v-if="generatedPassword" class="generated-password">
      <strong>Your password: </strong>{{ generatedPassword }}
    </div>
  </div>
</template>

<style scoped>
.password-generator-container {
  max-width: 400px;
  margin: 50px auto;
}

.password-generator-title {
  font-size: 24px;
  color: #333;
  margin-bottom: 20px;
}

input {
  width: 100%;
  padding: 8px;
  margin-bottom: 10px;
}

.generate-button {
  padding: 10px 15px;
  font-size: 16px;
  background-color: #3498db;
  color: #fff;
  border: none;
  border-radius: 4px;
  cursor: pointer;
}

.generate-button:hover {
  background-color: #2980b9;
}

.generated-password {
  margin-top: 20px;
  padding: 15px;
  border: 1px solid #ddd;
  border-radius: 4px;
  background-color: #f9f9f9;
  color: #333;
}
</style>
