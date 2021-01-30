<template>
  <q-layout view="lHh Lpr lFf">

    <div class="row menu-container q-pa-lg" >
      <div class="col-7 col-sm-4">
          <q-img
          src="imgs/logo-mormaii-motors-email.png"
          style="max-width: 301px;"
          />
      </div>
      <div class="col col-sm-8 text-right">
         <q-btn
          outline
          color="teal-6"
          :size="($q.screen.lt.lg) ? 'sm' : 'md'"
          label="Modelos"
        >
          <!-- <q-menu max-width="800px">
            <div class="row no-wrap q-pa-xs" style="min-width: 500px">
              <div class="column">
                <div class="text-h6 q-mb-md">Bikes</div>
                <q-list separator>
                  <q-item clickable v-ripple>
                    <q-item-section>Single line item</q-item-section>
                  </q-item>
                  <q-item clickable v-ripple>
                    <q-item-section>
                      <q-item-label>Item with caption</q-item-label>
                      <q-item-label caption>Caption</q-item-label>
                    </q-item-section>
                  </q-item>
                  <q-item clickable v-ripple>
                    <q-item-section>
                      <q-item-label overline>OVERLINE</q-item-label>
                      <q-item-label>Item with caption</q-item-label>
                    </q-item-section>
                  </q-item>
                </q-list>

              </div>

              <q-separator vertical inset class="q-mx-lg" />

              <div class="column">
                <div class="text-h6 q-mb-md">Motos</div>
                <q-list separator>
                <q-item clickable v-ripple>
                <q-item-section>Single line item</q-item-section>
                </q-item>
                <q-item clickable v-ripple>
                <q-item-section>
                <q-item-label>Item with caption</q-item-label>
                <q-item-label caption>Caption</q-item-label>
                </q-item-section>
                </q-item>
                <q-item clickable v-ripple>
                <q-item-section>
                <q-item-label overline>OVERLINE</q-item-label>
                <q-item-label>Item with caption</q-item-label>
                </q-item-section>
                </q-item>
                </q-list>
              </div>
            </div>
          </q-menu> -->
        </q-btn>
      </div>
    </div>

    <div class="q-pa-lg container-slide">

      <div class="q-pa-xs">

        <VueSlickCarousel v-bind="settingsSlider" class="q-pa-xs">

          <div
            class="text-center"
            v-for="slider in produtos.banner"
            :key="slider.produtoId">
            <p class="text-h4 text-white text-bold q-pa-lg">
              {{ slider.titulo }}
            </p>

            <q-img :src="slider.image" />

            <div class="row">
              <div
                class="col-4 q-pa-lg text-center"
                v-for="(info, index) in slider.info"
                :key="index"
              >
                <p class="text-white">
                  <span class="text-h4">{{ info.valor }}</span>
                  <small>{{ info.titulo }}</small>
                </p>
              </div>
              <div class="col-12 q-pa-md">
                <q-btn
                  outline
                  :size="($q.screen.lt.lg) ? 'md' : 'lg'"
                  color="white"
                  label="Ver mais informações"
                  @click="abrirModal()"
                />
              </div>
            </div>
          </div>

        </VueSlickCarousel>

      </div>
    </div>

    <div class="container-menu row q-mt-lg q-pa-md">
      <div
        class="col-12 col-sm-6 col-md-3 q-pl-md q-pr-md q-mb-lg"
        v-for="slider in produtos.banner"
        :key="slider.produtoId"
      >
        <q-card class="my-card" flat bordered>
          <q-card-section class="bg-grey-2 text-white q-pt-xl q-pb-md">
            <q-img :src="slider.image" />
          </q-card-section>

          <q-card-section>
             <q-btn
              class="q-mt-xs"
              color="white"
              outline text-color="black"
              :label="slider.titulo"
             />

          </q-card-section>
        </q-card>
      </div>
    </div>

    <!-- <q-carousel
      animated
      v-model="slide"
      navigation
      infinite
      :autoplay="true"
      arrows
      transition-prev="slide-right"
      transition-next="slide-left"
      @mouseenter="autoplay = false"
      @mouseleave="autoplay = true"
      class="bg-blue"
    >

      <q-carousel-slide
        v-for="(slider, index) in produtos.banner"
        :name="slider.produtoId"
        :img-src="slider.image"
        :key="index"
      />
    </q-carousel> -->

    <q-dialog
      v-model="modalInfo"
      full-height
      full-width
      maximized
      transition-show="slide-up"
      transition-hide="slide-down"
    >
      <q-card>
        <q-card-section class="row items-center q-pb-none bg-grey-2 q-pa-lg">
          <q-btn
            icon="close"
            color="red"
            dense
            v-close-popup
            class="absolute-top-right q-mt-sm q-mr-sm"
          />
          <div class="text-h3 text-bold col-12 to">
            {{ produtos.info.nome }}
          </div>
          <div class="row q-mt-md">
            <div
              class="col-12 col-sm-4 q-pl-lg q-pr-lg"
              style="border-right: 1px solid #ddd;"
            >
              <div class="text-h5 text-bold">
                200kg
              </div>
              <div class="text-subtitle1">
                Suporta até
              </div>
            </div>

            <div class="col-12 col-sm-6 q-pl-lg q-pr-lg" style="border-right: 1px solid #ddd;">
              <div class="text-h5 text-bold">
                4 há 8 horas
              </div>
              <div class="text-subtitle1">
                Autonomia
              </div>
            </div>

            <div class="col-12 col-sm-2 q-pl-lg q-pr-lg">
              <div class="text-h5 text-bold">
                55km
              </div>
              <div class="text-subtitle1">
                Velocidade
              </div>
            </div>
          </div>

          <q-space />

        </q-card-section>
        <q-card-section class="no-padding">
          <div class="row bg-teal-2 text-grey-10 q-mb-lg" style="padding: 40px 15px;">
            <div class="q-pt-lg q-pb-lg col-lg-12  col-md-12 col-sm-12 col-12 ">
              <q-img :src="'imgs/1.png'" class="" />
            </div>
            <!-- <div class="col-lg-12 col-md-12 col-sm-12 col-12 q-pt-lg">
              <div class="text-h3 q-pt-xs">
                {{ produtos.info.nome }}
              </div>
              <br>
              <div class="text-h6 text-normal">
              {{ produtos.info.descricao }}
              </div>
            </div> -->
          </div>
          <div class="row">

            <div
              class="col-lg-7 col-md-12 col-sm-12 col-12 q-pl-md q-pr-md q-mb-md"
            >

              <div class="text-h4 q-mb-md">Visualização 360°</div>
              <VueProductSpinner
                :images="images"
                :slider="false"
                :mouseDrag="true"
                :mouseWheel="false"
                auto
                class=""
                style="cursor: w-resize;"
              >
              </VueProductSpinner>

              <q-separator class="q-mt-lg q-mb-lg" />

              <div
                class="col-lg-7 col-md-6 col-sm-12 col-12 q-pr-md q-mb-md order-last"
              >
                <div class="text-h5">Cores</div>
                <!-- <div class="text-subtitle1">Disponível nas cores</div> -->
                <div class="container-cor">
                  <q-avatar
                    v-for="(cor, index) in produtos.info.cores"
                    :color="cor"
                    rounded
                    text-color="white"
                    icon=""
                    :key="index"
                    class="q-mr-md"
                    style="border: solid 1px #ccc;"
                  />
                </div>
              </div>
            </div>
            <div class="col-lg-5 col-sm-12 col-12 q-pl-md q-pr-md q-mb-md">
              <div class="text-h4 q-mb-md">Ficha Técnica</div>

              <q-markup-table separator="cell" bordered dense flat>
                <tbody>
                  <tr
                    v-for="(ficha, index) in produtos.info.fichaTecnica"
                    :key="index"
                  >
                    <td class="text-left text-subtitle1 text-bold">
                      {{ ficha.titulo }}
                    </td>
                    <td class="text-right text-subtitle1">
                      {{ ficha.valor }}
                    </td>
                  </tr>
                </tbody>
              </q-markup-table>
            </div>
          </div>
        </q-card-section>
        <q-card-actions align="right">
        </q-card-actions>
      </q-card>
    </q-dialog>

  </q-layout>
</template>

<script>

import VueSlickCarousel from 'vue-slick-carousel';
import 'vue-slick-carousel/dist/vue-slick-carousel.css';
import 'vue-slick-carousel/dist/vue-slick-carousel-theme.css';

import VueProductSpinner from 'vue-product-spinner';

export default {
  name: 'MainLayout',
  components: {
    VueSlickCarousel,
    VueProductSpinner,
  },
  data() {
    return {
      slide: 1,
      modalInfo: false,
      settingsSlider: {
        autoplay: true,
        dots: true,
        arrows: true,
        infinite: true,
        speed: 500,
        slidesToShow: 1,
        slidesToScroll: 1,
        initialSlide: 0,
        centerMode: false,
        adaptiveHeight: false,
        autoplaySpeed: 6000,
        touchMove: false,
        responsive: [
          {
            breakpoint: 1024,
            settings: {
              slidesToShow: 1,
              slidesToScroll: 1,
              infinite: true,
              dots: false,
            },
          },
          {
            breakpoint: 600,
            settings: {
              slidesToShow: 1,
              slidesToScroll: 1,
              initialSlide: 2,
              dots: false,
            },
          },
          {
            breakpoint: 480,
            settings: {
              slidesToShow: 1,
              slidesToScroll: 1,
              dots: false,
            },
          },
        ],
      },

      listaProdutos: [
        {
          id: 1,
          titulo: 'LINCE R2',
        },
      ],

      produtos: {
        banner: [
          {
            produtoId: 1,
            titulo: 'NAJA',
            image: 'imgs/1.png',
            info: [
              {
                titulo: 'Autonomia',
                valor: '34 km',
              },
              {
                titulo: 'Capacidade máxima',
                valor: '175 Kg',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '50 km/h',
              },
            ],
          },
          {
            produtoId: 2,
            titulo: 'LINCE',
            image: 'imgs/2.png',
            info: [
              {
                titulo: 'Autonomia',
                valor: '58 km',
              },
              {
                titulo: 'Capacidade máxima',
                valor: '207 Kg',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '50 km/h',
              },
            ],
          },
          {
            produtoId: 3,
            titulo: 'RAIA R2',
            image: 'imgs/3.png',
            info: [
              {
                titulo: 'Autonomia',
                valor: '6-8 horas',
              },
              {
                titulo: 'Capacidade máxima',
                valor: '200 Kg',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '61 km/h',
              },
            ],
          },
          {
            produtoId: 4,
            titulo: 'MOUNTAIN E-BIKE',
            image: 'imgs/6.png',
            info: [
              {
                titulo: 'Autonomia',
                valor: '20-45 km',
              },
              {
                titulo: 'Capacidade máxima',
                valor: '100 Kg',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '35 km/h',
              },
            ],
          },
        ],
        info: {
          nome: 'Naja R2',
          descricao: `Com autonomia de até 8 horas, nossas motos vão
          te levar a um novo momento em sua vida. O design único
          aliado ao conforto e autonomia da NAJA, facilitam o uso
          diário em qualquer lugar. Além disso, você tem a segurança
          de andar por aí em um produto totalmente legalizado.`,
          cores: [
            'red',
            'black',
            'white',
          ],
          images: [],
          fichaTecnica: [
            {
              titulo: 'Motor',
              valor: '2000W',
            },
            {
              titulo: 'Inclinação Máxima',
              valor: '40graus',
            },
            {
              titulo: 'Velocidade Máxima',
              valor: '61km/h',
            },
            {
              titulo: 'Bateria Litium',
              valor: '60V 20A',
            },
            {
              titulo: 'Alcance / Range / Gama',
              valor: '35-55km',
            },
            {
              titulo: 'Farol / Head Light',
              valor: 'Sim',
            },
            {
              titulo: 'Horn / Guidão',
              valor: 'Sim',
            },
            {
              titulo: 'Velocímetro / Speedometer',
              valor: 'Sim',
            },
            {
              titulo: 'Retrovisor',
              valor: 'Sim',
            },
            {
              titulo: 'Suspensão Dianteira',
              valor: 'Sim',
            },
            {
              titulo: 'Suspensão Traseira',
              valor: 'Sim',
            },
            {
              titulo: 'Luz de Freio',
              valor: 'Sim',
            },
            {
              titulo: 'Alarme',
              valor: 'Sim',
            },
            {
              titulo: 'Assento Simples',
              valor: 'Sim',
            },
            {
              titulo: 'Assento Duplo',
              valor: 'Não*',
            },
            {
              titulo: 'Carregador',
              valor: 'Sim',
            },
            {
              titulo: 'Tempo de Carga',
              valor: '6-8h',
            },
            {
              titulo: 'Peso Máximo Suportado',
              valor: '200kg',
            },
            {
              titulo: 'Roda',
              valor: '13 Polegadas',
            },
            {
              titulo: 'Medidas da Caixa',
              valor: '186*38*80',
            },
            {
              titulo: 'Peso Líquido / Bruto',
              valor: '72 /75 kg',
            },
          ],
        },
      },
    };
  },

  computed: {
    images() {
      const imagesArray = [];

      for (let i = 1; i < 100; i += 1) {
        imagesArray.push(`imgs/Moto1/image_${i}.jpg`);
      }

      return imagesArray;
    },
  },

  methods: {
    abrirModal() {
      this.modalInfo = true;
    },
  },
};
</script>
