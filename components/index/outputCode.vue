<script setup lang="ts">
import { Codemirror } from 'vue-codemirror'
import { javascript } from '@codemirror/lang-javascript'
import { oneDark } from '@codemirror/theme-one-dark'

const outputCode = useOutPutCode()
const outputLang = useOutPutLang()
const loading = useLoading()

const extensions = [javascript(), oneDark]
const view = shallowRef()
const handleReady = (payload: any) => {
    view.value = payload.view
}
function changeLang() {
    console.log(outputLang.value);
}

</script>

<template>
    <div class="lg:w-1/2 w-full  m-4">
        <select @change="changeLang" v-model="outputLang"
            class="select select-bordered w-full md:w-2/4 md:max-w-xs shadow-2xl mb-4">
            <option>javascript</option>
            <option>ts</option>
            <option selected>python</option>
            <option>php</option>
            <option>c</option>
            <option>c++</option>
            <option>ruby</option>
            <option>rust</option>
            <option>golang</option>
            <option>java</option>
            <option>kotlin</option>
        </select>
        <div class="relative">
            <div v-if="!outputCode" class="absolute top-0 left-0 w-full h-full bg-[#00000052] z-20">
                <Loading v-if="loading" />
            </div>
            <codemirror class="shadow-xl" v-model="outputCode" placeholder="Output Code ..." :style="{ height: '400px' }"
                :autofocus="true" :indent-with-tab="true" :tab-size="2" :extensions="extensions" @ready="handleReady" />
        </div>
    </div>
</template>