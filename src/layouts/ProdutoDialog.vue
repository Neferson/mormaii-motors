<template>
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
        {{ info.nome }}
      </div>
      <div class="row q-mt-md">
        <div
          class="col-12 col-sm-4 q-pl-lg q-pr-lg"
          style="border-right: 1px solid #ddd;"
          v-for="(prodInfo, index) in info.subInfo"
          :key="index"
        >
          <div class="text-h5 text-bold">
            {{ prodInfo.valor }}
          </div>
          <div class="text-subtitle1">
             {{ prodInfo.titulo }}
          </div>
        </div>

        <!-- <div class="col-12 col-sm-6 q-pl-lg q-pr-lg" style="border-right: 1px solid #ddd;">
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
        </div> -->
      </div>

      <q-space />

    </q-card-section>
    <q-card-section class="no-padding">
      <div class="row bg-teal-2 text-grey-10 q-mb-lg" style="padding: 40px 15px;">
        <div class="q-pt-lg q-pb-lg col-lg-12  col-md-12 col-sm-12 col-12 ">
          <q-img :src="`imgs/${info.id}.png`" class="" />
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
            :images="info.images"
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
                v-for="(cor, index) in info.cores"
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
                v-for="(ficha, index) in info.fichaTecnica"
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
</template>

<script>
import VueProductSpinner from 'vue-product-spinner';

export default {
  props: {
    info: Object
  },
  components: {
    VueProductSpinner,
  },
  data () {
    return {};
  },
}
</script>
