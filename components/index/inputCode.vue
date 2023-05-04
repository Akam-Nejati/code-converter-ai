<script setup lang="ts">
import { Codemirror } from 'vue-codemirror'
import { javascript } from '@codemirror/lang-javascript'
import { oneDark } from '@codemirror/theme-one-dark'

const inputCode = useInputCode()
const inputLang = useInputLang()
const outputLang = useOutPutLang()
const extensions = [javascript(), oneDark]
const view = shallowRef()
const handleReady = (payload: any) => {
    view.value = payload.view
}
function changeLang() {
    console.log(inputLang.value);
}

const emit = defineEmits<{
    (event: 'convert'): void
}>()


function convert() {
    emit("convert")
}
</script>

<template>
    <div class="lg:w-1/2 w-full m-4">
        <div class="flex justify-between items-center mb-4">
            <select @change="changeLang" v-model="inputLang" class="select select-bordered w-2/4 max-w-xs shadow-2xl">
                <option selected>javascript</option>
                <option>ts</option>
                <option>python</option>
                <option>php</option>
                <option>c</option>
                <option>c++</option>
                <option>ruby</option>
                <option>rust</option>
                <option>golang</option>
                <option>java</option>
                <option>kotlin</option>
            </select>
            <button @click="convert" class="btn" :class="{'btn-disabled': inputLang === outputLang || !inputCode}">convert</button>
        </div>
        <codemirror class="shadow-xl" v-model="inputCode" placeholder="Input Code ..." :style="{ height: '400px' }"
            :autofocus="true" :indent-with-tab="true" :tab-size="2" :extensions="extensions" @ready="handleReady" />
    </div>
</template>