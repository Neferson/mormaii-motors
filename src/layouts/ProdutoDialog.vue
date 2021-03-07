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

      <div
        class="col-12 col-sm-4 gt-sm"
        style=""
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

      <q-space />

    </q-card-section>

    <q-card-section class="no-padding">
      <div class="row bg-mormaii text-grey-10 q-mb-lg" style="padding: 40px 15px;">
        <div class="q-pt-lg q-pb-lg col-lg-12  col-md-12 col-sm-12 col-12 ">
          <q-img :src="`imgs/${info.id}.png`" class="" />
        </div>
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

          <q-markup-table separator="cell" bordered dense flat >
            <tbody>
              <tr
                v-for="(ficha, index) in info.fichaTecnica"
                :key="index"
              >
                <td class="text-left text-subtitle1 text-bold">
                  {{ ficha.titulo }}
                </td>
                <td class="text-left text-subtitle1 ellipsis" nowrap="true">
                  <span v-html="ficha.valor"></span>
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
