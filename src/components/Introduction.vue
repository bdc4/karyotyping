<template>
  <v-card>
    <v-card-title>
      Karyotyping Activity
    </v-card-title>
    <v-card-subtitle>
      Introduction
    </v-card-subtitle>
    <v-card-text>
      <v-row>
        <v-col sm="12" md="6" class="px-5" >
          <p>This exercise is a simulation of human karyotyping using digital images of chromosomes from actual human
            genetic
            studies. You will be arranging chromosomes into a completed karyotype, and interpreting your findings just as
            if
            you
            were working in a genetic analysis program at a hospital or clinic. Karyotype analyses are performed over
            400,000
            times per year in the U.S. and Canada. Imagine that you were performing these analyses for real people, and
            that
            your conclusions would drastically affect their lives.</p>

          <h3>G Banding</h3>
          <p>During mitosis, the 23 pairs of human chromosomes condense and are visible with a light microscope. A
            karyotype
            analysis usually involves blocking cells in mitosis and staining the condensed chromosomes with Giemsa dye.
            The
            dye
            stains regions of chromosomes that are rich in the base pairs Adenine (A) and Thymine (T) producing a dark
            band.
            A
            common misconception is that bands represent single genes, but in fact the thinnest bands contain over a
            million
            base pairs and potentially hundreds of genes. For example, the size of one small band is about equal to the
            entire
            genetic information for one bacterium.</p>
        </v-col>
        <v-col cols="6" sm="12" md="6">
          <v-row justify="center" class="py-10">

            <v-card width="100%">
              <v-card-text class="d-flex d-flex-row">
                <v-img max-width="300" src="../assets/introduction/chromsmear.gif" style="margin: auto;"></v-img>
                <v-card max-width="200" class="mx-5">
                  <v-card-text>
                    <v-img src="../assets/introduction/chromlabel.gif" width="200"></v-img>
                  </v-card-text>
                </v-card>
              </v-card-text>
            </v-card>
          </v-row>
        </v-col>
        <v-col cols="12">
          <p>The analysis involves comparing chromosomes for their length, the placement of centromeres (areas where the
            two
            chromatids are joined), and the location and sizes of G-bands. You will electronically complete the karyotype
            for
            three individuals and look for abnormalities that could explain the phenotype.</p>

          <h3>Your assignment</h3>
          <p>This exercise is designed as an introduction to genetic studies on humans. Karyotyping is one of many
            techniques
            that allow us to look for several thousand possible genetic diseases in humans.</p>

          <p>You will evaluate 3 patients' case histories, complete their karyotypes, and diagnose any missing or extra
            chromosomes. (Keep track of your answers, as you'll be expected to submit them.)</p>
        </v-col>
      </v-row>
    </v-card-text>
  </v-card>
</template>

<script>

export default {
  name: 'Introduction'
}
</script>
