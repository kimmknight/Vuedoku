<script>
export default {
    name: "tilenotesTile",

    props: ["selected", "notes"],

    data() {
        return {
            tilenotes: [false, false, false, false, false, false, false, false, false]
        }
    },

    methods: {
        toggle(number) {
            if (this.selected) {
                this.tilenotes[number - 1] = !this.tilenotes[number - 1]
                this.$emit("updated", this.tilenotes)
            }
        }
    },

    mounted() {
        this.tilenotes = this.notes
    }
}
</script>

<template>
    <div class="tile">
        <div class="tilenotes-row">
            <div :class="{note: tilenotes[0]}" @click="toggle(1)">1</div>
            <div :class="{note: tilenotes[1]}" @click="toggle(2)">2</div>
            <div :class="{note: tilenotes[2]}" @click="toggle(3)">3</div>
        </div>
        <div class="tilenotes-row">
            <div :class="{note: tilenotes[3]}" @click="toggle(4)">4</div>
            <div :class="{note: tilenotes[4]}" @click="toggle(5)">5</div>
            <div :class="{note: tilenotes[5]}" @click="toggle(6)">6</div>
        </div>
        <div class="tilenotes-row">
            <div :class="{note: tilenotes[6]}" @click="toggle(7)">7</div>
            <div :class="{note: tilenotes[7]}" @click="toggle(8)">8</div>
            <div :class="{note: tilenotes[8]}" @click="toggle(9)">9</div>
        </div>
    </div>
</template>

<style>
.tile {
    width: 100%;
    height: 100%;

    padding: 0.2em;

    font-size: 0.8em;
    color: grey;

    display: flex;
    flex-direction: column;
    justify-content: space-between;
}

.tilenotes-row {
    width: 100%;

    display: flex;
    justify-content: space-between;
}

.tilenotes-row>div {
    width: 100%;

    opacity: 0%;
}

.tilenotes-row>div:nth-child(1) {
    text-align: left;
}
.tilenotes-row>div:nth-child(2) {
    text-align: center;
}
.tilenotes-row>div:nth-child(3) {
    text-align: right;
}

.tilenotes-row>div:hover {
    opacity: 100%;
}

.note {
    opacity: 100% !important;
    color: rgb(138, 138, 138);
}

</style>