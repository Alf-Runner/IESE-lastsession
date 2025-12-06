<template>
  <div>
    <h2>AES (ECB) - Cifrar y Descifrar</h2>
<!-- Cifrar -->
 <!-- Cifrar -->
  <!-- Cifrar -->
    <!-- Cifrar -->
    <h3>Cifrar</h3>
    <form @submit.prevent="encryptAES">
      <label>Texto a cifrar:</label>
      <input v-model="textToEncrypt" type="text" />
      <button type="submit">Cifrar</button>
    </form>

    <div v-if="encrypted">
      <h4>Resultado cifrado (Base64):</h4>
      <p>{{ encrypted }}</p>
    </div>

    <!-- Descifrar -->
    <h3>Descifrar</h3>
    <form @submit.prevent="decryptAES">
      <label>Texto Base64 a descifrar:</label>
      <input v-model="textToDecrypt" type="text" />
      <button type="submit">Descifrar</button>
    </form>

    <div v-if="decrypted">
      <h4>Resultado descifrado:</h4>
      <p>{{ decrypted }}</p>
    </div>
  </div>
</template>

<script setup>
import CryptoJS from "crypto-js";
import { ref } from "vue";

// KEY EXACTA DE 16 BYTES (AES-128)
const KEY = CryptoJS.enc.Utf8.parse("miClaveSegura202"); 

// Inputs
const textToEncrypt = ref("");
const textToDecrypt = ref("");

// Outputs
const encrypted = ref("");
const decrypted = ref("");

// Cifrar
const encryptAES = () => {
  const result = CryptoJS.AES.encrypt(
    CryptoJS.enc.Utf8.parse(textToEncrypt.value),
    KEY,
    {
      mode: CryptoJS.mode.ECB,
      padding: CryptoJS.pad.Pkcs7,
    }
  );
  encrypted.value = result.toString(); // Base64
};

// Descifrar
const decryptAES = () => {
  const bytes = CryptoJS.AES.decrypt(
    textToDecrypt.value,
    KEY,
    {
      mode: CryptoJS.mode.ECB,
      padding: CryptoJS.pad.Pkcs7,
    }
  );
  decrypted.value = bytes.toString(CryptoJS.enc.Utf8);
};
</script>
