<!DOCTYPE html>
<html lang="en">
<head>
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/crypto-js/4.0.0/crypto-js.min.js"></script>
</head>
<body>
  <div id="app">    
    <h1 title='inspired by post here: https://fontawesomeicons.com/fa/vue-js-encryption-decryption-string-using-crypto-js'>Vue.js Encryption/Decryption</h1>
    <h2>Encrypt</h2>
    <h3>Plain Text</h3>
    <input v-model="encPlainText" placeholder="Enter string to encrypt" />
    <h3>Key to encrypt with</h3>
    <input v-model="encKey" placeholder="the key I will encrypt it with" />
    <button @click="encryptString">Encrypt</button>
    <div v-if="encRezStatus" style="float:right">
      <p>Encryption result status: {{ encRezStatus }}</p>
    </div>
    <input v-model="encRezult" placeholder="encryption result" />    
    <h2>Decrypt</h2>
    <h3>Encrypted Value</h3>
    <input v-model="decEncryptedText" placeholder="- - Encrypted String - -" />
    <h3>Decryption Key</h3>
    <input v-model="decKey" placeholder="- - decryption key - -" />
    <button @click="decryptString">Decrypt</button>
    <h3>Decryption Output</h3>
    <div v-if="decRezStatus" style="float:right">
      <p>Decryption result status: {{ decRezStatus }}</p>
    </div>    
    <input v-model="decRezult" placeholder="- - decryption result - -" />
  </div>
  <script type="module">
    const app = new Vue({
      el: "#app",
      data() {
        return {
          encPlainText: 'something I want to encrypt',
          encKey: 'mySecretKey',
          encRezStatus: '',
          decEncryptedText: 'U2FsdGVkX19hRJqKrEfWsKdaNjWSOCAjYXTc0p6YWcH18YQMFTO5ZWa4FdBY+FcB',
          decKey: 'mySecretKey',
          decRezStatus: '',    
        };
      },
      methods: {
        encryptString() {
          this.encRezStatus = '';
          if ( this.encPlainText == '' || this.encKey == '' ) { 
             alert('No point to encrypting with empty strings.');
          } else {
             const theRezult = CryptoJS.AES.encrypt(
             this.encPlainText,
             this.encKey
             ).toString();
             this.encRezStatus = ( theRezult != '');     
             this.encRezult = theRezult;
          }
        },
        decryptString() {
          this.decRezStatus = '';
          const decryptedBytes = CryptoJS.AES.decrypt(
            this.decEncryptedText,
            this.decKey
          );
          const theRezult = decryptedBytes.toString(CryptoJS.enc.Utf8);
          this.decRezStatus = (theRezult != ''); 
          this.decRezult = theRezult;
        },
      },
    });
  </script>
  <style scoped>
    #app {
      max-width: 500px;
      margin: 0 auto;
      padding: 20px;
      font-family: Arial, sans-serif;
    }

    h3 {
      font-size: 20px;
      margin-bottom: 10px;
    }

    input {
      padding: 10px;
      width: 100%;
      margin-bottom: 10px;
      border: 1px solid #ccc;
      border-radius: 4px;
      font-size: 14px;
    }

    button {
      padding: 10px 20px;
      background-color: #4caf50;
      color: #fff;
      border: none;
      border-radius: 4px;
      cursor: pointer;
      font-size: 14px;
    }

    button:hover {
      background-color: #45a049;
    }

    .result-container {
      margin-top: 20px;
      border: 1px solid #ccc;
      border-radius: 4px;
      padding: 10px;
      background-color: #f9f9f9;
    }

    p {
      margin: 0;
      font-size: 14px;
    }
  </style>

</body>

</html>
