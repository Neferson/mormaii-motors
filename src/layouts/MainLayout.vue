<template>
  <q-layout view="lHh Lpr lFf">

    <div class="row menu-container q-pt-sm  q-pb-sm  q-pl-md q-pr-md bg-black" >
      <div class="col-7 col-sm-4">
          <q-img
            src="imgs/logo-mormaii.png"
            style="max-width: 54px;"
          />
      </div>
      <div class="col col-sm-8 text-right">
         <q-btn
          outline
          color="white"
          :size="($q.screen.lt.lg) ? 'sm' : 'md'"
          label="Modelos"
          class="q-mt-sm"
        >
          <q-menu max-width="800px">
            <div class="row no-wrap q-pa-xs" style="min-width: 350px">

              <div class="col">
                <q-list separator>
                  <q-item
                    clickable
                    v-ripple
                    v-for="prod in produtos.banner"
                    :key="prod.id"
                    @click="abrirModal(prod.produtoId)"
                    v-close-popup
                  >
                    <q-item-section>
                      <span class="text-subtitle1">
                        {{ prod.titulo }}
                      </span>
                    </q-item-section>
                    <q-item-section>
                      <q-img :src="prod.image" />
                    </q-item-section>
                  </q-item>
                </q-list>
              </div>
            </div>
          </q-menu>
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
                  @click="abrirModal(slider.produtoId)"
                />
              </div>
            </div>
          </div>

        </VueSlickCarousel>

      </div>
    </div>

    <div id="container-menu-home" class="container-menu row q-mt-lg q-pa-md">
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
              @click="abrirModal(slider.produtoId)"
             />

          </q-card-section>
        </q-card>
      </div>
    </div>

    <q-dialog
      v-model="modalInfo"
      full-height
      full-width
      maximized
      transition-show="slide-up"
      transition-hide="slide-down"
    >
      <ProdutoDialog :info="produto"></ProdutoDialog>
    </q-dialog>

  </q-layout>
</template>

<script>

import VueSlickCarousel from 'vue-slick-carousel';
import 'vue-slick-carousel/dist/vue-slick-carousel.css';
import 'vue-slick-carousel/dist/vue-slick-carousel-theme.css';

import ProdutoDialog from './ProdutoDialog'

export default {
  name: 'MainLayout',
  components: {
    VueSlickCarousel,
    ProdutoDialog,
  },
  data() {
    return {
      slide: 1,
      modalInfo: false,
      produto: {},
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
            image: 'imgs/4.png',
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
          {
            produtoId: 5,
            titulo: 'MINI E-BIKE',
            image: 'imgs/5.png',
            info: [
              {
                titulo: 'Autonomia',
                valor: '20-60 km',
              },
              {
                titulo: 'Capacidade máxima',
                valor: '120 Kg',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '25 km/h',
              },
            ],
          },
          {
            produtoId: 6,
            titulo: 'E-MOUTAIN BIKE S',
            image: 'imgs/6.png',
            info: [
              {
                titulo: 'Autonomia',
                valor: '35-80 km',
              },
              {
                titulo: 'Capacidade máxima',
                valor: '150 Kg',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '35 km/h',
              },
            ],
          },
          {
            produtoId: 7,
            titulo: 'MINI E-BIKE ARTICULÁVEL',
            image: 'imgs/7.png',
            info: [
              {
                titulo: 'Autonomia',
                valor: '30-40 km',
              },
              {
                titulo: 'Capacidade máxima',
                valor: '110 Kg',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '25 km/h',
              }
            ],
          },
          {
            produtoId: 8,
            titulo: 'BIKE DOBRÁVEL S ',
            image: 'imgs/8.png',
            info: [
              {
                titulo: 'Autonomia',
                valor: '25-65 km',
              },
              {
                titulo: 'Capacidade máxima',
                valor: '120 Kg',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '25 km/h',
              }
            ],
          },
        ],
        lista: [
          {
            id: 1,
            nome: 'NAJA',
            descricao: `Com autonomia de até 8 horas, nossas motos vão
            te levar a um novo momento em sua vida. O design único
            aliado ao conforto e autonomia da NAJA, facilitam o uso
            diário em qualquer lugar. Além disso, você tem a segurança
            de andar por aí em um produto totalmente legalizado.`,
            subInfo: [
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
          {
            id: 2,
            nome: 'LINCE',
            descricao: `Com autonomia de até 8 horas, nossas motos vão
            te levar a um novo momento em sua vida. O design único
            aliado ao conforto e autonomia da NAJA, facilitam o uso
            diário em qualquer lugar. Além disso, você tem a segurança
            de andar por aí em um produto totalmente legalizado.`,
            subInfo: [
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
            cores: [
              'red',
              'blue-5',
              'black',
            ],
            images: [],
            fichaTecnica: [
              {
                titulo: 'Dimensões (C * L * A)',
                valor: '1980 mm * 860 mm * 1100 mm',
              },
              {
                titulo: 'Apoio para cada pé do condutor (C * L)',
                valor: '160 mm * 100 mm',
              },
              {
                titulo: 'Distância entre eixos',
                valor: '1410 mm',
              },
              {
                titulo: 'Peso (kg)',
                valor: '74 kg',
              },
              {
                titulo: 'Material',
                valor: 'Metal',
              },
              {
                titulo: 'Capacidade máxima',
                valor: '207 kg',
              },
              {
                titulo: 'Pneu dianteiro (TAM)',
                valor: '165/45-12',
              },
              {
                titulo: 'Pneu traseiro (TAM)',
                valor: '215/40-12',
              },
              {
                titulo: 'Freio dianteiro',
                valor: 'Disco 180 mm (hidráulico)',
              },
              {
                titulo: 'Freio traseiro',
                valor: 'Disco 180 mm (hidráulico)',
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
                titulo: 'Motor',
                valor: '2000W',
              },
              {
                titulo: 'Proteção de corrente de sobrecarga',
                valor: 'Sim',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '50 km/h ≤',
              },
              {
                titulo: 'Torque máximo',
                valor: '63 Nm',
              },
              {
                titulo: 'Consumo de energia',
                valor: '25 Wh/km',
              },
              {
                titulo: 'Autonomia',
                valor: '58 km',
              },
              {
                titulo: 'Bateria',
                valor: 'Lítio, 126 cells / 60 V / 20 Ah',
              },
              {
                titulo: 'Bateria (kg)',
                valor: '8 Kg',
              },
              {
                titulo: 'Ângulo máximo de manobra, roda dianteira',
                valor: '49° ambos os lados',
              },
              {
                titulo: 'Modo de aceleração',
                valor: '1° - Modo padrão <br>2° - Modo econômico <br>3° - Modo esporte',
              },
              {
                titulo: 'Inclinação máxima',
                valor: '28º',
              },
              {
                titulo: 'Farol',
                valor: 'Tipo: SG01-NZ – 1 / BRANCO',
              },
              {
                titulo: 'Farol de rodagem diurna',
                valor: 'Tipo: SG01-NZ – 1 / BRANCO',
              },
              {
                titulo: 'Luzes indicadoras de direção frontal',
                valor: 'Tipo: SJ-LED-Z10 – 2 / ÂMBAR',
              },
              {
                titulo: 'Refletor Lateral',
                valor: 'Tipo: KM206 – 2 / ÂMBAR',
              },
              {
                titulo: 'Refletor traseiro',
                valor: 'Tipo: KM206 – 1 / VERMELHO',
              },
              {
                titulo: 'Lâmpada da placa de registro',
                valor: 'Tipo: CH-2044 – 1 / BRANCO',
              },
              {
                titulo: 'Luzes indicadoras de direção traseira',
                valor: 'Tipo: SJ-LED-Z10 2 / ÂMBAR',
              },
              {
                titulo: 'Luz de freio',
                valor: 'Tipo: CH-2041 – 1 / VERMELHO',
              },
              {
                titulo: 'Espelhos retrovisores',
                valor: 'Sim',
              },
              {
                titulo: 'Buzina',
                valor: 'Sim',
              },
              {
                titulo: 'Dispositivo antifurto',
                valor: 'Sim',
              },
            ],
          },
          {
            id: 3,
            nome: 'RAIA R2',
            descricao: `Com autonomia de até 8 horas, nossas motos vão
            te levar a um novo momento em sua vida. O design único
            aliado ao conforto e autonomia da NAJA, facilitam o uso
            diário em qualquer lugar. Além disso, você tem a segurança
            de andar por aí em um produto totalmente legalizado.`,
            subInfo: [
              {
                titulo: 'Autonomia',
                valor: '35-55 km',
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
          {
            id: 4,
            nome: 'MOUNTAIN E-BIKE',
            descricao: `Com autonomia de até 8 horas, nossas motos vão
            te levar a um novo momento em sua vida. O design único
            aliado ao conforto e autonomia da NAJA, facilitam o uso
            diário em qualquer lugar. Além disso, você tem a segurança
            de andar por aí em um produto totalmente legalizado.`,
            subInfo: [
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
            cores: [
              'red',
              'black',
              'white',
            ],
            images: [],
            fichaTecnica: [
              {
                titulo: 'Dimensões (C * L * A)',
                valor: '187 cm * 67 cm * 115 cm',
              },
              {
                titulo: 'Distância entre eixos',
                valor: '112 cm',
              },
              {
                titulo: 'Peso Líquido (kg)',
                valor: '22,5 kg',
              },
              {
                titulo: 'Peso Bruto (kg)',
                valor: '25 kg',
              },
              {
                titulo: 'Quadro',
                valor: 'Alumínio',
              },
              {
                titulo: 'Capacidade máxima',
                valor: '100 kg',
              },
              {
                titulo: 'Garfo',
                valor: 'Suspensão MTB com trava de bloqueio',
              },
              {
                titulo: 'Câmbio',
                valor: '7 marchas cabide montagem direta',
              },
              {
                titulo: 'Passador de marcha',
                valor: 'MicroShift 51-8*',
              },
              {
                titulo: 'Câmbio traseiro',
                valor: 'MicroShift TZ-50*',
              },
              {
                titulo: 'Pneu',
                valor: 'fat 26 x 4.0',
              },
              {
                titulo: 'Freios',
                valor: 'Disco',
              },
              {
                titulo: 'Motor',
                valor: '250 W',
              },
              {
                titulo: 'Manopla de velocidade',
                valor: 'Sim',
              },
              {
                titulo: 'Pedal assistido',
                valor: 'Sim',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '35 km',
              },
              {
                titulo: 'Autonomia (CNTP)',
                valor: '30 – 45 km, peso 75 kg > mantendo 20 - 25 km/h',
              },
              {
                titulo: 'Bateria',
                valor: 'Lítio - 36 V / 10.4 A',
              },
              {
                titulo: 'Carregador',
                valor: 'Bivolt',
              },
              {
                titulo: 'Tempo de recarga',
                valor: '6 – 8 h',
              },
              {
                titulo: 'Bateria (kg)',
                valor: '8 Kg',
              },
              {
                titulo: 'Consumo de energia',
                valor: '≤ 1.2kw/h',
              },
              {
                titulo: 'Luz dianteira',
                valor: 'Sim',
              },
            ],
          },
          {
            id: 5,
            nome: 'MINI E-BIKE',
            descricao: `Com autonomia de até 8 horas, nossas motos vão
            te levar a um novo momento em sua vida. O design único
            aliado ao conforto e autonomia da NAJA, facilitam o uso
            diário em qualquer lugar. Além disso, você tem a segurança
            de andar por aí em um produto totalmente legalizado.`,
            subInfo: [
              {
                titulo: 'Autonomia',
                valor: '20-60 km',
              },
              {
                titulo: 'Capacidade máxima',
                valor: '120 Kg',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '25 km/h',
              },
            ],
            cores: [
              'red',
              'black',
              'white',
            ],
            images: [],
            fichaTecnica: [
              {
                titulo: 'Dimensões (C * L * A)',
                valor: '107 cm * 45 cm * 100 cm',
              },
              {
                titulo: 'Dimensões dobravél (C * L * A)',
                valor: '107 cm * 27 cm * 73 cm',
              },
              {
                titulo: 'Peso Líquido (kg)',
                valor: '17 kg',
              },
              {
                titulo: 'Quadro',
                valor: 'Alumínio',
              },
              {
                titulo: 'Guidão',
                valor: 'Dobrável',
              },
              {
                titulo: 'Pedal',
                valor: 'Dobrável',
              },
              {
                titulo: 'Capacidade máxima',
                valor: '120 kg',
              },
              {
                titulo: 'Suspensão',
                valor: 'Mola',
              },
              {
                titulo: 'Pneu',
                valor: '12',
              },
              {
                titulo: 'Freios',
                valor: 'Disco',
              },
              {
                titulo: 'Motor',
                valor: '350 W',
              },
              {
                titulo: 'Manopla de velocidade',
                valor: 'Sim',
              },
              {
                titulo: 'Pedal assistido',
                valor: 'Sim',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '35 km',
              },
              {
                titulo: 'Modo de assistência',
                valor: '3 níveis de velocidade',
              },
              {
                titulo: 'Autonomia (CNTP)',
                valor: 'Modo elétrico: 20 – 25 km / Modo assistido: 40 – 60 km',
              },
              {
                titulo: 'Bateria',
                valor: ' Lítio - 36 V / 7.5 A',
              },
              {
                titulo: 'Proteção de carga',
                valor: 'Proteção contra: curto circuito, sobrecarga, descarga excessiva, <br>sobrecorrente, sobretensão e temperatura.',
              },
              {
                titulo: 'Carregador',
                valor: 'Bivolt',
              },
              {
                titulo: 'Tempo de recarga',
                valor: '3 – 4 h',
              },
              {
                titulo: 'Capacidade de rampa',
                valor: '15°',
              },
              {
                titulo: 'Índice de proteção',
                valor: 'IP54',
              },
              {
                titulo: 'Luz dianteira',
                valor: 'Sim',
              },
              {
                titulo: 'Luz traseira',
                valor: 'Sim',
              },
            ],
          },
          {
            id: 6,
            nome: 'E-MOUNTAIN BIKE S',
            descricao: `Com autonomia de até 8 horas, nossas motos vão
            te levar a um novo momento em sua vida. O design único
            aliado ao conforto e autonomia da NAJA, facilitam o uso
            diário em qualquer lugar. Além disso, você tem a segurança
            de andar por aí em um produto totalmente legalizado.`,
            subInfo: [
              {
                titulo: 'Autonomia',
                valor: '35-80 km',
              },
              {
                titulo: 'Capacidade máxima',
                valor: '150 Kg',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '35 km/h',
              }
            ],
            cores: [
              'lime-6',
              'red',
              'black',
              'white',
            ],
            images: [],
            fichaTecnica: [
              {
                titulo: 'Dimensões (C * L * A)',
                valor: '191 cm * 76 cm * 116 cm',
              },
              {
                titulo: 'Marchas',
                valor: '21',
              },
              {
                titulo: 'Peso Líquido (kg)',
                valor: '26 kg',
              },
              {
                titulo: 'Quadro',
                valor: 'Liga de alumínio',
              },
              {
                titulo: 'Guidão',
                valor: 'Liga de alumínio',
              },
              {
                titulo: 'Canote de selim',
                valor: 'Alumínio',
              },
              {
                titulo: 'Canote de selim',
                valor: 'Alumínio',
              },
              {
                titulo: 'Garfo',
                valor: 'Liga de alumínio com suspensão com <br>trava de bloqueio',
              },
              {
                titulo: 'Alavanca de câmbio',
                valor: 'SHIMANO TX50-7',
              },
              {
                titulo: 'Câmbio dianteiro',
                valor: 'SHIMANO TZ30',
              },
              {
                titulo: 'Câmbio traseiro',
                valor: 'SHIMANO TZ50',
              },
              {
                titulo: 'Pedivela',
                valor: 'Liga de alumínio',
              },
              {
                titulo: 'Cassete',
                valor: 'SHIMANO TZ21-714-28T',
              },
              {
                titulo: 'Freios',
                valor: 'ZSTAR Disco 160 mm',
              },
              {
                titulo: 'Cubo dianteiro',
                valor: ' Liga de alumínio com QR',
              },
              {
                titulo: 'Aro',
                valor: 'Liga de alumínio',
              },
              {
                titulo: 'Pneu',
                valor: '26 x 4.0',
              },
              {
                titulo: 'Pedais',
                valor: 'Alumínio MTB',
              },
              {
                titulo: 'Motor',
                valor: '350 W',
              },
              {
                titulo: 'Manopla de velocidade',
                valor: 'Sim',
              },
              {
                titulo: 'Pedal assistido',
                valor: 'Sim',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '35 km',
              },
              {
                titulo: 'Autonomia (CNTP)',
                valor: 'Elétrico: 35 km <br>Pedal assistido: 60 - 80 km',
              },
              {
                titulo: 'Modo de assistência',
                valor: 'Elétrico puro (5 turnos) <br>Assistência elétrica (5 turnos)<br> Equitação Humano puro',
              },
              {
                titulo: 'Bateria',
                valor: 'Lítio 48v 10ah',
              },
              {
                titulo: 'Tempo de recarga',
                valor: '4 – 6 h',
              },
              {
                titulo: 'Proteção de sobrecarga',
                valor: 'Sobretensão, sobrecorrente, curto circuito',
              },
              {
                titulo: 'PAS',
                valor: '12 sensor magnético, assistido de potência de pulso',
              },
              {
                titulo: 'Farol',
                valor: 'Sim',
              },
            ],
          },
          {
            id: 7,
            nome: 'MINI E-BIKE ARTICULÁVEL',
            descricao: `Com autonomia de até 8 horas, nossas motos vão
            te levar a um novo momento em sua vida. O design único
            aliado ao conforto e autonomia da NAJA, facilitam o uso
            diário em qualquer lugar. Além disso, você tem a segurança
            de andar por aí em um produto totalmente legalizado.`,
            subInfo: [
              {
                titulo: 'Autonomia',
                valor: '30-40 km',
              },
              {
                titulo: 'Capacidade máxima',
                valor: '110 Kg',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '25 km/h',
              }
            ],
            cores: [
              'amber-6',
              'black',
              'white',
            ],
            images: [],
            fichaTecnica: [
              {
                titulo: 'Dimensões (C * L * A)',
                valor: '125 cm * 59cm * 105 cm',
              },
              {
                titulo: 'Distância entre eixos',
                valor: '96 cm',
              },
              {
                titulo: 'Dimensões articulado: (C * L * A)',
                valor: '70 cm * 29 cm * 95 cm',
              },
              {
                titulo: 'Peso Líquido (kg)',
                valor: '17,8 kg',
              },
              {
                titulo: 'Peso (kg) Bruto',
                valor: '20,2 kg',
              },
              {
                titulo: 'Capacidade máxima suportada (kg)',
                valor: '110 kg',
              },
              {
                titulo: 'Quadro',
                valor: 'Alumínio',
              },
              {
                titulo: 'Freios',
                valor: 'Tambor',
              },
              {
                titulo: 'Pneu',
                valor: '12',
              },
              {
                titulo: 'Motor',
                valor: '250 W',
              },
              {
                titulo: 'Manopla de velocidade',
                valor: 'SIM',
              },
              {
                titulo: 'Pedal assistido',
                valor: 'SIM',
              },
              {
                titulo: 'Níveis de assistência',
                valor: '3 níveis de velocidade',
              },
              {
                titulo: 'Velocidade máxima (CNTP)',
                valor: '25 km/h',
              },
              {
                titulo: 'Autonomia (CNTP)',
                valor: 'Acionamento elétrico: 30 - 40 km <br>Auxílio por pedalada: 50 – 60 km',
              },
              {
                titulo: 'Modo cruzeiro',
                valor: 'Acionando a manopla de velocidade durante 8 segundos',
              },
              {
                titulo: 'Bateria',
                valor: 'Lítio – 36v / 10ah',
              },
              {
                titulo: 'Carregador',
                valor: 'Bivolt',
              },
              {
                titulo: 'Tempo de recarga',
                valor: '3 – 5 h',
              },
              {
                titulo: 'Farol',
                valor: 'SIM',
              },
              {
                titulo: 'Buzina',
                valor: 'SIM',
              },
            ],
          },
          {
            id: 8,
            nome: 'BIKE DOBRÁVEL S',
            descricao: `Com autonomia de até 8 horas, nossas motos vão
            te levar a um novo momento em sua vida. O design único
            aliado ao conforto e autonomia da NAJA, facilitam o uso
            diário em qualquer lugar. Além disso, você tem a segurança
            de andar por aí em um produto totalmente legalizado.`,
            subInfo: [
              {
                titulo: 'Autonomia',
                valor: '25-65 km',
              },
              {
                titulo: 'Capacidade máxima',
                valor: '120 Kg',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '25 km/h',
              }
            ],
            cores: [
              'red',
              'black',
              'white',
            ],
            images: [],
            fichaTecnica: [
              {
                titulo: 'Dimensões (C * L * A)',
                valor: '(122 cm * 49 cm * 108 cm)',
              },
              {
                titulo: 'Distância entre eixos',
                valor: '85 cm',
              },
              {
                titulo: 'Dimensões articulado: (C * L * A)',
                valor: '(71 cm * 34 cm * 64 cm)',
              },
              {
                titulo: 'Peso Líquido (kg)',
                valor: '20 kg',
              },
              {
                titulo: 'Peso (kg) Bruto',
                valor: '23,5 kg',
              },
              {
                titulo: 'Capacidade máxima suportada (kg)',
                valor: '120 kg',
              },
              {
                titulo: 'Quadro',
                valor: 'Liga de alumínio',
              },
              {
                titulo: 'Amortecedor dianteiro',
                valor: 'Sim',
              },
              {
                titulo: 'Amortecedor traseiro',
                valor: 'SIM',
              },
              {
                titulo: 'Freios',
                valor: 'Disco',
              },
              {
                titulo: 'Pneu',
                valor: '14',
              },
              {
                titulo: 'Pedal assistido',
                valor: 'SIM',
              },
              {
                titulo: 'Motor',
                valor: '400 W',
              },
              {
                titulo: 'Velocidade máxima',
                valor: '25 km/h',
              },
              {
                titulo: 'Autonomia',
                valor: '25-30 km / Pedal assistido: 55-65 km',
              },
              {
                titulo: 'Modo de assistência',
                valor: '3 níveis de velocidade ',
              },
              {
                titulo: 'Bateria',
                valor: '48v - 10 ah / 15ah',
              },
              {
                titulo: 'Carregador',
                valor: 'Bivolt',
              },
              {
                titulo: 'Tempo de recarga',
                valor: '5 - 6 h',
              },
              {
                titulo: 'Capacidade de escalada',
                valor: '25°',
              },
              {
                titulo: 'Índice de proteção',
                valor: 'IP 54',
              },
              {
                titulo: 'Luz dianteira',
                valor: 'LED',
              },
              {
                titulo: 'Luz de freio',
                valor: 'SIM',
              },
              {
                titulo: 'Buzina',
                valor: 'SIM',
              },
            ],
          },
        ],
      },
    };
  },

   meta: {
    // sets document title
    title: 'Mormaii E-Motors',
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
    abrirModal(produtoId) {
      this.modalInfo = true;

      this.produtos.lista.map((prod) => {
        prod.images = this.arrayImages(produtoId)

        if (prod.id === produtoId) {
          this.produto = prod
        }
        return ''
      })
    },

    arrayImages(produtoId) {
      const imagesArray = [];

      for (let i = 1; i < 100; i += 1) {
        imagesArray.push(`imgs/Moto${produtoId}/image_${i}.jpg`);
      }

      return imagesArray;
    },
  },
};
</script>
