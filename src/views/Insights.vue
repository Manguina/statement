<template>
  <div class="insights">
    <!-- Hero Section -->
    <section class="hero" style="margin-top: 100px;">
      <h1 style="text-align: center;color: #042236;">Insights Estratégicos</h1>
      <p>
        Nosso blog é o espaço onde compartilhamos tendências de mercado, análises de casos, boas práticas e insights estratégicos. Aqui, você encontra ideias que ajudam a tomar decisões informadas e a navegar com confiança pelas complexidades do mundo dos negócios.
      </p>
    </section>

    <!-- Filter Section -->
    <section class="filters">
      <div class="filter-buttons">
        <button>Insights e Tendências</button>
        <button>Casos de Sucesso</button>
        <button>Estratégia e Processos</button>
        <button>Economia e Mercados</button>
      </div>
    </section>

    <!-- Main Articles Section -->
    <section class="main-articles">
      <div v-if="destaque" @click="goToDetails(destaque.id)"  class="featured-article">
        <img :src="destaque.image_url" alt="Artigo em destaque">
        <div class="content">
          <span class="category"></span>
          <h2>{{ destaque.title }}</h2>
          <p>
           {{ destaque.content }}
          </p>
          <span class="date">Criado em: {{ formatDate(destaque.created_at) }}</span>
        </div>
      </div>
      <div v-else class="featured-article">Nenhuma postagem encontrada.</div>
      <aside class="recommended">
        <h3>Recomendado</h3>
        <div class="row mb-4 border-bottom pb-3"  v-for="(prinicipal, index) in prinicipal" :key="index"  @click="goToDetails(prinicipal.id)">
        <div class="col-4">
            <img :src="prinicipal.image_url" class="img-fluid" alt="Notícia 2">
        </div>
        <div class="col-8">
            <h5 class="mb-1">{{ prinicipal.title }}</h5>
            <small class="text-muted">{{ formatDate(prinicipal.created_at) }}</small>
        </div>
    </div>

      </aside>
    </section>

    <!-- Articles Grid Section -->
    <section class="articles-grid">
      <div class="article" v-for="(article, index) in articles" :key="index" @click="goToDetails(article.id)">
        <img :src="article.image_url" :alt="`Artigo ${index + 1}`">
        <h4>{{ article.title }}</h4>
        <p>{{ article.content }}</p>
        <span class="date">{{ formatDate(article.created_at) }}</span>
      </div>
    </section>

    <!-- Newsletter Section -->
    <section class="newsletter">
      <h2>Insights em Foco</h2>

      <div class="container">
      <div class="row align-items-center">
        <div class="col-md-6">
          <p class="mb-0">
            Quer saber mais sobre tópicos específicos? Escolha os boletins informativos
        abaixo e acompanhe as novas tendências.
          </p>
        </div>
        <div class="col-md-6">
          <form class="d-flex align-items-center">
            <input type="email" class="form-control me-2" placeholder="Seu Endereço de Email" aria-label="Email">
            <button type="submit" class="btn btn-subscribe">Newsletter</button>
          </form>
          <div class="form-check mt-2">
            <input class="form-check-input" type="checkbox" value="" id="privacyPolicy">
            <label class="form-check-label privacy-policy" for="privacyPolicy">
             
            </label>
          </div>
        </div>
      </div>
    </div>
    </section>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: "InsightsPage",
  data() {
    return {
      images: {
        featured: "@/assets/images/featured-article.jpg",
        placeholder: "/src/assets/images/article-placeholder.jpg",
      },
      destaque:[],
      articles: [],
      prinicipal:[],
    };
  },
  methods:{
    PostsDestaque() {
      // Fazer a requisição para a API com o filtro
      const apiUrl = `http://localhost/Blog/api`;
      axios
        .get(apiUrl)
        .then((response) => {
          this.destaque = response.data.destaque;
          this.prinicipal = response.data.reco;
          this.articles = response.data.normal;
        })
        .catch((error) => {
          console.error('Erro ao carregar as postagens:', error);
        });
    },
    formatDate(dateString) {
            const date = new Date(dateString); // Converter para objeto Date
            const day = String(date.getDate()).padStart(2, '0'); // Dia com 2 dígitos
            const month = String(date.getMonth() + 1).padStart(2, '0'); // Mês com 2 dígitos (0-indexado)
            const year = date.getFullYear(); // Ano
            return `${day}-${month}-${year}`; // Formatar como dd-mm-yyyy
        },
    goToDetails(id) {
            this.$router.push(`/details/${id}`);
        },
  },
  created() {
    // Carregar as postagens quando o componente é montado
    this.PostsDestaque();
  },
};
</script>

<style scoped>
/*****************************/
/* Layout Geral */
/*****************************/
.insights {
  font-family: Arial, sans-serif;
  color: #333;
}

/*****************************/
/* Hero Section */
/*****************************/
.hero {
  text-align: justify;
  padding: 20px;
  background-color: #f4f4f4;
}

.hero h1 {
  font-size: 2em;
  color: #b11116;
}

.hero p {
  max-width: 800px;
  margin: 0 auto;
  color: #555;
}

/*****************************/
/* Filters Section */
/*****************************/
.filters {
  text-align: center;
  margin: 20px 0;
}

.filter-buttons button {
  background-color: #fff;
  color: #333;
  border: 1px solid #ccc;
  padding: 10px 20px;
  margin: 5px;
  cursor: pointer;

  /* Adicionando transição */
  transition: background-color 0.3s ease, color 0.3s ease;
}

.filter-buttons button:hover,
.filter-buttons button:active {
  background-color: #042236;
  color: #fff;
  cursor: pointer;
}


/*****************************/
/* Main Articles Section */
/*****************************/
.main-articles {
  display: flex;
  gap: 20px;
  margin: 20px;
}

.featured-article {
  flex: 3;
  border: 1px solid #ddd;
  border-radius: 10px;
  overflow: hidden;
}

.featured-article img {
  width: 100%;
  height: auto;
}

.featured-article .content {
  padding: 10px;
}

.featured-article .category {
  font-size: 0.8em;
  color: #888;
}

.featured-article h2 {
  font-size: 1.5em;
  color: #b11116;
}

.featured-article p {
  color: #555;
}

.featured-article .date {
  font-size: 0.8em;
  color: #aaa;
}

.recommended {
  flex: 1;
  padding: 10px;  
}

.recommended h3 {
  font-size: 1.2em;
  color: #042236;
}

.recommended ul {
  list-style: none;
  padding: 0;
}

.recommended li {
  margin: 10px 0;
  font-size: 0.9em;
  color: #555;
}

/*****************************/
/* Articles Grid */
/*****************************/
.articles-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
  gap: 20px;
  margin: 20px;
}

.article {
  border: 1px solid #ddd;
  border-radius: 10px;
  overflow: hidden;
  text-align: center;
  padding: 10px;
}

.article img {
  width: 100%;
  height: 200px;
  object-fit: cover;
}

.article h4 {
  font-size: 1.2em;
  color: #042236;
}

.article p {
  font-size: 0.9em;
  color: #333;
  text-align: justify;
}

.article .date {
  font-size: 0.8em;
  color: #aaa;
}

/*****************************/
/* Newsletter Section */
/*****************************/
.newsletter {
  text-align: center;
  padding: 40px;
  background-color: #f4f4f4;
}

.newsletter h2 {
  font-size: 1.8em;
  color: #042236;
}

.newsletter p {
  color: #555;
}

.newsletter button {
  background-color: #042236;
  color: #fff;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

/*****************************/
/* Load More Section */
/*****************************/
.load-more {
  text-align: center;
  margin: 20px 0;
}

.load-more button {
  background-color: #b11116;
  color: #fff;
  padding: 10px 20px;
  border: none;
  cursor: pointer;
  border-radius: 5px;
}

.load-more button:hover {
  background-color: #900d13;
}
</style>
