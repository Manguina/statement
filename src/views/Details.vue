<template>
    <div class="container" style="margin-top: 120px;">
      <div v-if="detalhe">
        <div class="row align-items-center hero-section">
            <!-- Texto principal -->
            <div class="col-lg-6 col-md-12 mb-4 mb-lg-0">
                <p class="text-danger fw-bold">The Visionary CEO’s Guide to Sustainability</p>
                <h1 class="title-text">{{ detalhe.title }}</h1>
                <p class="subtitle-text">
                  {{ detalhe.subtitulo }}
                </p>
                <p class="author-text">
                    Autor:<br>
                    <span>8 min</span>
                </p>
                <!-- Ícones de ação -->
                <div class="action-icons">
                    <i class="bi bi-share"></i>
                    <i class="bi bi-file-earmark-pdf"></i>
                    <i class="bi bi-bookmark"></i>
                </div>
                
            </div>
            <!-- Imagem -->
            <div class="col-lg-6 col-md-12 image-section">
                <img :src="detalhe.image_url" alt="Pessoa com tablet">
            </div>
        </div>

        <div class="row mt-4">
            <!-- Coluna 1: Autores -->
            <div class="col-md-3 sidebar-section">
                <h6>Noticias Relacionadas</h6>
                <div v-for="lis in lista" :key="lis.id" class="mb-4">
                    <img :src="lis.image_url" alt="Autor 1" class="author-img">
                    <p class="mb-0"><strong>{{ lis.title }}</strong></p>
                </div>
            </div>

            <!-- Coluna 2: Conteúdo Principal -->
            <div class="col-md-6">
                <!-- Escuta do Artigo -->
                <div class="d-flex align-items-center mb-4">
                    
                </div>
                <!-- Seção "At a Glance" -->
                <h4 class="section-title">{{ detalhe.title }}</h4>
                <div class="list-item">
                    <i class="bi bi-caret-right-fill"></i>
                    <p>{{ detalhe.subtitulo }}</p>
                </div>
                <div class="list-item">
                    <p>{{ detalhe.content }}</p>
                </div>
            </div>

            <!-- Coluna 3: Links Relacionados -->
            <div class="col-md-3 sidebar-section">
                <h6>Outros Conteudo</h6>
                <a href="#">Insights e Tendências</a>
                <a href="#">Casos de Sucesso</a>
                <a href="#">Estratégia e Processos</a>
                <a href="#">Economia e Mercados</a>
            </div>
        </div>
      </div>
      <p v-else>Carregando detalhes...</p>
    </div>
  </template>
  
  <script>
  import axios from "axios";
  
  export default {
    name: "DetailsPage",
    props: ["id"],
    data() {
      return {
        detalhe: null, // Armazena os detalhes da postagem
        lista:null,
      };
    },
    methods: {
      // Função para buscar detalhes da postagem
      fetchPostDetails() {
        const apiUrl = `http://localhost/Blog/api/single/${this.id}`;
        axios
          .get(apiUrl)
          .then((response) => {
            this.detalhe = response.data.post; // Atualiza os detalhes
            this.lista = response.data.lista; // Atualiza os detalhes
            console.log( response.data.lista);
          })
          .catch((error) => {
            console.error("Erro ao carregar os detalhes:", error);
          });
      },
    },
    mounted() {
      // Chama a função ao montar o componente
      this.fetchPostDetails();
    },
    watch: {
      // Atualiza os dados se a propriedade `id` mudar
      id() {
        this.fetchPostDetails();
      },
    },
  };
  </script>
  
  <style scoped>
   body {
            font-family: Arial, sans-serif;
            margin: 0;
            padding: 0;
            color: #333;
        }
        .hero-section {
            padding: 3rem 1.5rem;
            background-color: #f9f9f9;
        }
        .title-text {
            color: black;
            font-size: 2.5rem;
            font-weight: bold;
            line-height: 1.2;
        }
        .subtitle-text {
            color: #666;
            font-size: 1rem;
            margin-top: 1rem;
        }
        .author-text {
            font-size: 0.9rem;
            color: #777;
            margin-top: 1rem;
        }
        .image-section img {
            max-width: 100%;
            border-radius: 8px;
        }
        .action-icons {
            margin-top: 2rem;
        }
        .action-icons i {
            font-size: 1.5rem;
            color: #555;
            margin-right: 1rem;
            cursor: pointer;
        }
        .section-title {
            border-bottom: 2px solid red;
            padding-bottom: 5px;
            font-weight: bold;
        }
        .list-item {
            display: flex;
            align-items: flex-start;
            margin-bottom: 1rem;
        }
        .list-item i {
            color: red;
            font-size: 1.2rem;
            margin-right: 10px;
        }
        .author-img {
            width: 60px;
            height: 60px;
            border-radius: 50%;
            object-fit: cover;
            margin-bottom: 10px;
        }
        .sidebar-section h6 {
            font-weight: bold;
            margin-top: 1.5rem;
        }
        .sidebar-section a {
            text-decoration: none;
            color: #d93025;
            display: block;
            margin-bottom: 0.5rem;
        }
  </style>
  