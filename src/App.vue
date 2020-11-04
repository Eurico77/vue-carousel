<template>
  <div id="app">
    <carousel :dotsVisible="true">
      <carousel-slide
        v-for="(slider, index) in slides"
        :key="index"
        :imageUrl="slides[index].src"
        :title="slides[index].title"
        :sub-title="slides[index].subtitle"
      >
      </carousel-slide>
    </carousel>
  </div>
</template>

<script>
import Carousel from "./components/Carousel";
import CarouselSlide from "./components/CarouselSlide";

export default {
  name: "App",
  components: {
    Carousel,
    CarouselSlide,
  },
  data() {
    return {
      slides: [
        {
          src: "https://picsum.photos/201/300",
          title: "O que é Lorem Ipsum?",
          subtitle: "Lorem Ipsum é simplesmente uma simulação de texto da indústria tipográfica e de impressos, e vem sendo utilizado desde o século XVI, quando um impressor desconhecido pegou uma bandeja de tipos e os embaralhou para fazer um livro de modelos de tipos.",
        },
        {
          src: "https://picsum.photos/202/300",
          title: "De onde ele vem?",
          subtitle: "Ao contrário do que se acredita, Lorem Ipsum não é simplesmente um texto randômico. Com mais de 2000 anos, suas raízes podem ser encontradas em uma obra de literatura latina clássica datada de 45 AC. ",
        },
        {
          src: "https://picsum.photos/203/300",
          title: "Onde posso conseguí-lo?",
          subtitle: "O trecho padrão original de Lorem Ipsum, usado desde o século XVI, está reproduzido abaixo para os interessados. Seções 1.10.32 e 1.10.33 de de Finibus Bonorum et Malorum de Cicero também foram reproduzidas abaixo em sua forma exata original, acompanhada das versões para o inglês da tradução feita por H. Rackham em 1914.",
        },
        {
          src: "https://picsum.photos/201/300",
          title: "Porque nós o usamos?",
          subtitle: "É um fato conhecido de todos que um leitor se distrairá com o conteúdo de texto legível de uma página quando estiver examinando sua diagramação. A vantagem de usar Lorem Ipsum é que ele tem uma distribuição normal de letras, ao contrário de Conteúdo aqui, conteúdo aqui, fazendo com que ele tenha uma aparência similar a de um texto legível.",
        },
      ],
    };
  },
};
</script>

<style scoped>
#app {
display: flex;
justify-content: center;
}
</style>
