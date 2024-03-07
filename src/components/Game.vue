<template>
    <v-text-field type="number" v-model="sizeX" label="Size X"></v-text-field>

    <v-text-field type="number" v-model="sizeY" label="Size Y"></v-text-field>

    <v-sheet :height="2048" :width="2048" color="black">
        <div class="d-flex">
            <div v-for="box in boxes.listX" v-on:mouseover="() => changeColorX(box.index)" class="square"
                :style="box.toggled ? 'background-color: white' : 'background-color: blue'">
            </div>
        </div>

        <div class="d-flex flex-column">
            <div v-for="box in boxes.listY" v-on:mouseover="() => changeColorY(box.index)" class="square"
                :style="box.toggled ? 'background-color: white' : 'background-color: blue'">
            </div>
        </div>

    </v-sheet>
</template>

<script setup lang="ts">
import { ref, reactive, computed } from "vue";

const sizeX = ref(0)
const sizeY = ref(0)


const boxes = computed(() => {
    if (sizeX.value === 0 || sizeX.value === '') {
        sizeX.value = 1
    }
    if (sizeY.value === 0 || sizeY.value === '') {
        sizeY.value = 1
    }
    const listX = reactive([])
    for (let i of Array.from(Array(parseInt(sizeX.value.toString())).keys())) {
        listX.push(
            {
                index: i,
                toggled: false
            }
        )
    }
    const listY = reactive([])
    for (let i of Array.from(Array(parseInt(sizeY.value.toString())).keys())) {
        listY.push(
            {
                index: i,
                toggled: false
            }
        )
    }
    return {
        listX,
        listY
    };
});

function changeColorX(index: number) {
    boxes.value.listX[index].toggled = !boxes.value.listX[index].toggled
}
function changeColorY(index: number) {
    boxes.value.listY[index].toggled = !boxes.value.listY[index].toggled
}

</script>

<style>
.square {
    margin: 1px 1px 1px 1px;
    width: 32px;
    height: 32px;
}
</style>