<template>
   <section style="margin-top: 150px;">
    <div class="container">
    <!-- Seção de informações -->
    <div class="info-box">
      <h1>Luanda</h1>
      <p>Rua 28 de Maio,<br>
        Edifício Kende,<br>
        7º andar<br>
        Maianga<br>
        Luanda, Angola</p>
      <p><strong>Tel:</strong> +224 938-613-955<br>
         <strong>Whatshapp:</strong> +224 938-613-955</p>
    </div>
    <!-- Seção do mapa -->
    <div class="map-box">
     <iframe
          width="100%"
          height="100%"
          style="border:0"
          loading="lazy"
          :src="mapSrc"
          allowfullscreen
        ></iframe>
    </div>
  </div>
   </section>
</template>

<script>
export default {
  name: "ContactPage",
  data() {
      return {
        form: {
          name: '',
          email: '',
          message: ''
        },
        // Substitua pelo seu endereço do Google Maps
        mapSrc: 'https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d3153.1234567890!2d-122.4194157481234!3d37.7749295481234!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x8085818e12345678%3A0x1234567890abcdef!2sExemplo!5e0!3m2!1spt-BR!2sbr!4v1612345678901!5m2!1spt-BR!2sbr' // Exemplo de link do Google Maps
      };
    },
    methods: {
      submitForm() {
        // Lógica para enviar o formulário
        console.log('Formulário enviado:', this.form);
        // Aqui você pode adicionar código para enviar os dados para o servidor
        // E limpar o formulário após o envio
        this.form.name = '';
        this.form.email = '';
        this.form.message = '';
      }
    }
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: row;
  height: 450px;
  margin-top: 15px;
  margin-bottom: 35px;
}

/* Caixa de informações */
.info-box {
  width: 40%;
  padding: 40px;
  background-color: #002433; /* Cor de fundo escura */
}

.info-box h1 {
  font-size: 2em;
  margin-bottom: 20px;
  color: #ffffff;
}

.info-box p {
  font-size: 1em;
  line-height: 1.6;
  margin-bottom: 20px;
  color: #ffffff;
}

.info-box strong {
  color: #cccccc;
}

.map-link {
  color: #ffffff;
  text-decoration: none;
  font-weight: bold;
  display: inline-block;
  margin-top: 20px;
}

.map-link:hover {
  text-decoration: underline;
  color: #999999;
}

/* Caixa do mapa */
.map-box {
  width: 60%;
  background-color: #e0e0e0;
}

.map-box iframe {
  display: block;
  width: 100%;
  height: 100%;
  border: none;
}

</style>
