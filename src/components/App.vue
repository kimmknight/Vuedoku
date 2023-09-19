<script>

export default {

    data() {
        return {
            backgroundImageUrl: "https://source.unsplash.com/random/?ocean",
            gameBoard: [],
            startBoard: [
                [ 4, 2, 0, 0, 3, 0, 1, 0, 7 ],
                [ 3, 0, 5, 6, 0, 8, 0, 0, 2 ],
                [ 0, 0, 0, 0, 7, 2, 0, 6, 5 ],
                [ 0, 6, 9, 8, 0, 0, 0, 0, 3 ],
                [ 7, 1, 0, 2, 0, 0, 4, 9, 6 ],
                [ 0, 0, 3, 9, 6, 0, 0, 2, 0 ],
                [ 0, 0, 0, 0, 2, 4, 8, 0, 0 ],
                [ 1, 0, 0, 7, 8, 0, 6, 0, 0 ],
                [ 0, 5, 4, 0, 0, 0, 0, 0, 1 ]
            ],
            selectedCell: {x: 0, y: 0}
        }
    },

    methods: {
        deepCopy(arr) {
            return JSON.parse(JSON.stringify(arr))
        },

        // countInstances(number) {
        //     let boardString = ""
        //     for (const row in this.gameBoard) {
        //         for (const col in this.gameBoard[row]) {
        //             boardString += String(this.gameBoard[row, col])
        //         }
        //     }

        //     return boardString.match(`/${number}/g`)
        // },

        cellInSelectedRow(x) {
            return x == this.selectedCell.x
        },


        cellInSelectedCol(y) {
            return y == this.selectedCell.y
        },

        cellInSelectedSquare(x, y) {
            const firstcellInSelectedSquareX = Math.ceil((this.selectedCell.x + 1) / 3)
            const firstcellInSelectedSquareY = Math.ceil((this.selectedCell.y + 1) / 3)
            
            const firstInCandidateSquareX = Math.ceil((x + 1) / 3)
            const firstInCandidateSquareY = Math.ceil((y + 1) / 3)

            return firstcellInSelectedSquareX == firstInCandidateSquareX && firstcellInSelectedSquareY == firstInCandidateSquareY
        },

        cellContentSameAsSelected(x, y) {
            return this.gameBoard[y][x] > 0 && this.gameBoard[y][x] == this.gameBoard[this.selectedCell.y][this.selectedCell.x]
        },

        cellContentAlreadyInLine(x, y) {

        },

        cellEditable(x, y) {
            return this.startBoard[y][x] == 0
        },

        isCellValid(x, y) {
            const numberToCheck = this.gameBoard[y][x]

            if (numberToCheck == 0) return true

            for (const col in this.gameBoard[y]) {
                const value = this.gameBoard[y][col]
                if ( col != x && value == numberToCheck ) {
                    return false
                }
            }

            for (const row in this.gameBoard) {
                const value = this.gameBoard[row][x]
                if (row != y && value == numberToCheck) {
                    return false
                }
            }

            const sqStartx = Math.floor(x / 3) * 3
            const sqStarty = Math.floor(y / 3) * 3

            for (let row = sqStarty; row <= sqStarty + 2; row++) {
                for (let col = sqStartx; col <= sqStartx + 2; col++) {
                    const value = this.gameBoard[row][col]
                    if ( (row != y && col != x) && value == numberToCheck) {
                        return false
                    }
                }
            }
            
            return true
        },

        enterInSelectedCell(value) {
            if (this.cellEditable(this.selectedCell.x, this.selectedCell.y)) {
                this.gameBoard[this.selectedCell.y][this.selectedCell.x] = value
            }
        }
    },

    computed: {
        backgroundImageUrlEnclosed() {
            return "url(\"" + this.backgroundImageUrl + "\")"
        },

        countInstances() {
            let instances = [0,0,0,0,0,0,0,0,0,0]
            for (const row in this.gameBoard) {
                for (const col in this.gameBoard[row]) {
                    instances[this.gameBoard[row][col]] += 1
                    // boardString += String(this.gameBoard[row, col])
                }
            }
            return instances
        }
    },

    mounted() {
        this.gameBoard = this.deepCopy(this.startBoard);
    }
}
</script>

<template>
    <header :style="{'background-image': backgroundImageUrlEnclosed}">
        <span class="header-text">Vuedoku</span>
    </header>

    <main>
        <div class="board-container">
    
            <div id="grid-container" class="d-flex flex-column">
                <div class="board-row" v-for="(row, y) in gameBoard">
                    <div
                        class="board-cell d-flex justify-content-center align-items-center"
                        :class="{
                            'selected': (selectedCell.x == x && selectedCell.y == y),
                            'relevant-line': (cellInSelectedRow(x) || cellInSelectedCol(y)),
                            'relevant-square': (cellInSelectedSquare(x, y)),
                            'samesies': (cellContentSameAsSelected(x, y)),
                            'warning': (!isCellValid(x, y))
                        }"
                        v-for="(cell, x) in row"
                        @click="selectedCell = {x: x, y: y}"
                    >
                        <span v-show="!gameBoard[y][x] == 0">{{ gameBoard[y][x] }}</span>
                    </div>
                </div>
            </div>
    
        </div>
        <div id="input-container">  <!-- v-show="cellEditable(selectedCell.x, selectedCell.y)" -->
            <div v-for="index in 9">
                <div class="input-button" @click="enterInSelectedCell(index)" :class="{'input-button-disabled': countInstances[index] >= 9}">
                    {{ index }}
                </div>
            </div>
            <div class="input-button clear-button" @click="enterInSelectedCell(0)">
                Clear
            </div>
        </div>
    </main>
</template>

<style scoped>

header {
    padding-top: 2em;
    padding-bottom: 2em;
    margin-bottom: 2em;
    text-align: center;
    background-color: white;
    background-position: center;
    background-size: cover;
    width: 100vw;
}
.header-text {
    font-size: calc(1.625rem + 4.5vw);
    font-weight: 300;
    letter-spacing: 0px;
    line-height: 1.2;
    color: white;
    text-shadow: 0px 0px 5px rgba(0,0,0,1);
}

main {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}
.board-container {
    display: flex;
    justify-content: center;
}
.board-row {
    display: flex;
    width: fit-content;
}
.board-row:first-child {
    border-top: 3px solid black;
}

.board-row:nth-child(3n) {
    border-bottom: 3px solid black;
}

.board-cell {
    display: flex;
    color: rgb(85, 85, 85);
    justify-content: center;
    align-items: center;
    width: 10vw;
    height: 10vw;
    max-width: 3em;
    max-height: 3em;
    border: 1px solid grey;
    font-weight: 600;
    cursor: pointer;
}

.board-cell:hover {
    background-color: lightyellow;
}

.board-cell:nth-child(9n+1) {
    border-left: 3px solid black;
}

.board-cell:nth-child(3n) {
    border-right: 3px solid black;
}

.samesies {
    background-color: rgb(203, 237, 203);
}

.relevant-square {
    background-color: rgb(240, 240, 240);
}

.relevant-line {
    background-color: rgb(215, 215, 215);
}

.warning {
    background-color: red;
    color: white;
}

.selected {
    background-color: lightgreen;
}

#input-container {
    margin: 2vw;
    display: flex;
    flex-wrap: wrap;
    width: 12em;
    height: fit-content;
}

.input-button {
    display: flex;
    justify-content: center;
    align-items: center;
    border: 0.1em solid grey;
    height: 3em;
    width: 3em;
    margin: 0.2em;
    border-radius: 0.25em;
    cursor: pointer;
}

.input-button:hover {
    background-color: rgb(218, 218, 218);
}

.input-button-disabled {
    visibility: hidden;
}

.clear-button {
    width: 10.2em;
}

</style>
