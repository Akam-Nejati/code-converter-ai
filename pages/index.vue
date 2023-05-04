<script setup lang="ts">
import axios from 'axios';

const inputCode = useInputCode()
const outputCode = useOutPutCode()
const inputLang = useInputLang()
const outputLang = useOutPutLang()
const loading = useLoading()
const code = useState<string>(() => "")

function convert() {
  code.value = `convert this ${inputLang.value} code ( ${inputCode.value} ) to ${outputLang.value}`
  loading.value = true
  outputCode.value = ""

  axios
    .post(`https://sugar-bead-salmonberry.glitch.me/api?query=${code.value}`)
    .then((res) => {
      console.log(res);
      outputCode.value = res.data;
      loading.value = false
    })
    .catch((error) => {
      console.log(error);
      loading.value = false
    });
}
</script>


<template>
  <div class="flex justify-center my-10 font-bold">
    <h3 class="text-4xl">Code Converter Ai</h3>
  </div>
  <div>
    <div class="flex justify-between items-center lg:flex-row flex-col px-[1rem] sm:px-[5rem] md:px-[7rem] lg:px-0">
      <IndexInputCode @convert="convert()"/>
      <IndexOutputCode />
    </div>
  </div>
</template>