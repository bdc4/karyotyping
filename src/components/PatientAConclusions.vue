<template>
  <div>
    <h2>Patient A's Karyotype</h2>
    <p>
      Congratulations! You successfully completed Patient A's Karyotype. Next, interpret the karyotype and make a
      diagnosis. Patient A's completed karyotype is at the bottom of the page for reference.
    </p>
    <p>
      On a separate piece of paper, answer the following 2 questions.
    </p>
    <h3>Interpreting the karyotype</h3>
    <p>
      Lab technicians compile karyotypes and then use a specific notation to characterize the karyotype. This notation
      includes the total number of chromosomes, the sex chromosomes, and any extra or missing autosomal chromosomes.
      For example, <strong>47, XY, +18</strong> indicates that the patient has 47 chromosomes, is a male, and has an extra
      autosomal chromosome 18. <strong>46, XX</strong> is a female with a normal number of chromosomes. <strong>47,
        XXY</strong> is a patient with an extra sex chromosome.
    </p>
    <p>
      <strong>A 1.</strong> What notation would you use to characterize Patient A's karyotype?
    </p>
    <h3>Making a diagnosis</h3>
    <p>
      The next step is to either diagnose or rule out a chromosomal abnormality. In a patient with a normal number of
      chromosomes, each pair will have only two chromosomes. Having an extra or missing chromosome usually renders a fetus
      inviable. In cases where the fetus makes it to term, there are unique clinical features depending on which
      chromosome is affected. Listed below are some syndromes caused by an abnormal number of chromosomes.
    </p>
    <p>
      <strong>A 2.</strong> What diagnosis would you give patient A?
    </p>
    <v-table>
      <thead>
        <tr>
          <th><strong>Diagnosis</strong></th>
          <th><strong>Chromosomal Abnormality</strong></th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Normal # of chromosomes</td>
          <td>patient's problems are due to something other than an abnormal number of chromosomes.</td>
        </tr>
        <tr>
          <td>Klinefelter's Syndrome</td>
          <td>one or more extra sex chromosomes (i.e., XXY)</td>
        </tr>
        <tr>
          <td>Down's Syndrome</td>
          <td>Trisomy 21, extra chromosome 21</td>
        </tr>
        <tr>
          <td>Trisomy 13 Syndrome</td>
          <td>extra chromosome 13
          </td>
        </tr>
      </tbody>
    </v-table>
  </div>
</template>

<script>
export default {
  name: "PatientAConclusions",
  data () {
    return {
      foo: 'bar'
    }
  }
}
</script>

