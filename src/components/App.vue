<script>

import NotesTile from "./NotesTile.vue"

export default {
    components: [NotesTile],
    data() {
        return {
            game: {selectedTheme: "Forest"}, //selectedTheme required, otherwise backgroundImageUrl fails
            loaded: false,
            intitalGame: {
                board: [
                    [4, 2, 0, 0, 3, 0, 1, 0, 7],
                    [3, 0, 5, 6, 0, 8, 0, 0, 2],
                    [0, 0, 0, 0, 7, 2, 0, 6, 5],
                    [0, 6, 9, 8, 0, 0, 0, 0, 3],
                    [7, 1, 0, 2, 0, 0, 4, 9, 6],
                    [0, 0, 3, 9, 6, 0, 0, 2, 0],
                    [0, 0, 0, 0, 2, 4, 8, 0, 0],
                    [1, 0, 0, 7, 8, 0, 6, 0, 0],
                    [0, 5, 4, 0, 0, 0, 0, 0, 1]
                ],
                solution: [
                    [4, 2, 6, 5, 3, 9, 1, 8, 7],
                    [3, 7, 5, 6, 1, 8, 9, 4, 2],
                    [9, 8, 1, 4, 7, 2, 3, 6, 5],
                    [2, 6, 9, 8, 4, 7, 5, 1, 3],
                    [7, 1, 8, 2, 5, 3, 4, 9, 6],
                    [5, 4, 3, 9, 6, 1, 7, 2, 8],
                    [6, 3, 7, 1, 2, 4, 8, 5, 9],
                    [1, 9, 2, 7, 8, 5, 6, 3, 4],
                    [8, 5, 4, 3, 9, 6, 2, 7, 1]
                ],
                notes: [
                    [
                        [false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],
                    ],
                    [
                        [false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],
                    ],
                    [
                        [false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],
                    ],[
                        [false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],
                    ],[
                        [false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],
                    ],[
                        [false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],
                    ],[
                        [false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],
                    ],[
                        [false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],
                    ],[
                        [false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],[false, false, false, false, false, false, false, false, false],
                    ],
                ],
                difficulty: "Easy",
                notesMode: false,
                selectedTheme: "Forest"
            },
            selectedCell: { x: 0, y: 0 },
            dropdown: {theme: false},
            themes: [
                "Forest",
                "Ocean",
                "Beach",
                "Sunset",
                "Space",
                "City",
                "Reef",
                "Leaves",
                "Fabric",
                "Macro",
                "Bokeh",
                "Art",
                "Surfing",
                "Datacenter",
                "Sudoku",
                "Colors"
            ]
        };
    },

    computed: {
        countInstances() {
            let instances = [0, 0, 0, 0, 0, 0, 0, 0, 0, 0];
            for (const row in this.game.board) {
                for (const col in this.game.board[row]) {
                    instances[this.game.board[row][col]] += 1;
                    // boardString += String(this.game.board[row, col])
                }
            }
            return instances;
        },

        backgroundImageUrl() {
            return "url(https://source.unsplash.com/random/?" + this.game.selectedTheme.toLowerCase()
        }
    },

    methods: {
        deepCopy(arr) {
            return JSON.parse(JSON.stringify(arr));
        },
        fetchGetNewPuzzle() {
            this.loaded = false;
            fetch("https://sudoku-api.vercel.app/api/dosuku")
                .then((httpResponse) => httpResponse.json())
                .then((responseData) => {
                this.intitalGame.board = responseData.newboard.grids[0].value;
                this.intitalGame.solution = responseData.newboard.grids[0].solution;
                this.intitalGame.difficulty = responseData.newboard.grids[0].difficulty;
                this.game = this.deepCopy(this.intitalGame);
                this.loaded = true;
            });
        },
        resetPuzzle() {
            this.game.board = this.deepCopy(this.intitalGame.board);
        },
        numberAlreadyInRow(x) {
            return x == this.selectedCell.x;
        },
        numberAlreadyInCol(y) {
            return y == this.selectedCell.y;
        },
        numberAlreadyInCurrentSquare(x, y) {
            const firstNumberAlreadyInCurrentSquareX = Math.ceil((this.selectedCell.x + 1) / 3);
            const firstNumberAlreadyInCurrentSquareY = Math.ceil((this.selectedCell.y + 1) / 3);
            const firstInCandidateSquareX = Math.ceil((x + 1) / 3);
            const firstInCandidateSquareY = Math.ceil((y + 1) / 3);
            return firstNumberAlreadyInCurrentSquareX == firstInCandidateSquareX && firstNumberAlreadyInCurrentSquareY == firstInCandidateSquareY;
        },
        cellContentSameAsSelected(x, y) {
            return this.game.board[y][x] > 0 && this.game.board[y][x] == this.game.board[this.selectedCell.y][this.selectedCell.x];
        },
        cellContentAlreadyInLine(x, y) {
        },
        cellEditable(x, y) {
            return this.intitalGame.board[y][x] == 0;
        },
        callValid(x, y) {
            const numberToCheck = this.game.board[y][x];
            if (numberToCheck == 0)
                return true;
            for (const col in this.game.board[y]) {
                const value = this.game.board[y][col];
                if (col != x && value == numberToCheck) {
                    return false;
                }
            }
            for (const row in this.game.board) {
                const value = this.game.board[row][x];
                if (row != y && value == numberToCheck) {
                    return false;
                }
            }
            const sqStartx = Math.floor(x / 3) * 3;
            const sqStarty = Math.floor(y / 3) * 3;
            for (let row = sqStarty; row <= sqStarty + 2; row++) {
                for (let col = sqStartx; col <= sqStartx + 2; col++) {
                    const value = this.game.board[row][col];
                    if ((row != y && col != x) && value == numberToCheck) {
                        return false;
                    }
                }
            }
            return true;
        },

        cellSelected(x, y) {
            return this.selectedCell.x == x && this.selectedCell.y == y
        },

        enterInSelectedCell(value) {
            if (this.cellEditable(this.selectedCell.x, this.selectedCell.y)) {
                this.game.board[this.selectedCell.y][this.selectedCell.x] = value;
            }
        },

        toggleNoteInSelectedCell(value) {
            this.game.notes[this.selectedCell.y][this.selectedCell.x][value - 1] = !this.game.notes[this.selectedCell.y][this.selectedCell.x][value - 1]
        },

        clearNotesInSelectedCell() {
            for (const number in this.game.notes[this.selectedCell.y][this.selectedCell.x]) {
                this.game.notes[this.selectedCell.y][this.selectedCell.x][number] = false
            }
        },

        clearAllNotes() {
            for (const row in this.game.notes) {
                for (const col in this.game.notes[row]) {
                    for (const number in this.game.notes[row][col]) {
                        this.game.notes[row][col][number] = false
                    }
                }
            }
        },

        localStorageLoad(alternativeFunction) {
            const storedDataJSON = localStorage.getItem("vuedoku-state");
            if (storedDataJSON) {
                const storedData = JSON.parse(storedDataJSON);
                this.game = storedData.game;
                this.intitalGame = storedData.intitalGame;
                this.loaded = true;
            }
            else {
                console.log("Puzzle not present in local storage. Fetching new puzzle.");
                alternativeFunction();
            }
        },
        localStorageSave() {
            localStorage.setItem("vuedoku-state", JSON.stringify({ game: this.game, intitalGame: this.intitalGame }));
        },

        selectTheme(theme) {
            this.game.selectedTheme = theme
            this.dropdown.theme = false
        }
    },
    
    watch: {
        game: {
            handler(newValue, oldValue) {
                this.localStorageSave();
            }, deep: true
        }
    },
    mounted() {
        this.localStorageLoad(() => { this.fetchGetNewPuzzle(); });
    },
    components: { NotesTile }
}
</script>

<template>
    <header :style="{'background-image': backgroundImageUrl}">
        <span class="header-text">Vuedoku</span>
        
        <div id="menubar" :class="{invisible: !loaded}">
            <div id="controls">
                <div class="controls-button" @click="fetchGetNewPuzzle()">
                    New puzzle
                </div>
                <div class="difficulty">{{ game.difficulty }}</div>
                <div class="controls-button" @click="resetPuzzle()">
                    Reset puzzle
                </div>
                <div class="controls-button theme-button" @click="dropdown.theme = !dropdown.theme">
                    >
                </div>
                <div class="dropdown-content" v-if="dropdown.theme">
                    <div v-for="theme in themes" class="dropdown-item"><div @click="selectTheme(theme)">{{ theme }}</div></div>
                </div>
            </div>
        </div>
    </header>

    <div id="loading" v-if="!loaded">
        <div class="loader"></div>
    </div>


    <main v-if="loaded" :class="{'win-background': countInstances[0] == 0}">
        <div class="board-container">
    
            <div id="grid-container" class="d-flex flex-column">
                <div class="board-row" v-for="(row, y) in game.board">
                    <div
                        class="board-cell d-flex justify-content-center align-items-center"
                        :class="{
                            'selected': (cellSelected(x, y)),
                            'relevant-line': (numberAlreadyInRow(x) || numberAlreadyInCol(y)),
                            'relevant-square': (numberAlreadyInCurrentSquare(x, y)),
                            'samesies': (cellContentSameAsSelected(x, y)),
                            'warning': (!callValid(x, y)),
                            'user-entered': (cellEditable(x, y))
                        }"
                        v-for="(cell, x) in row"
                        @click="selectedCell = {x: x, y: y}"
                    >
                        <span v-if="!game.board[y][x] == 0">{{ game.board[y][x] }}</span>
                        <NotesTile v-else :selected="cellSelected(x, y)" :notes="game.notes[y][x]" @updated="(notes) => {game.notes[y][x] = notes}" />
                    </div>
                </div>
            </div>
    
            <div id="remaining-numbers"><b>Remaining: {{ countInstances[0] }}</b></div>
        </div>
        <div id="input-area">
            

            <div class="notes-checkbox-container">
                <input id="notes-checkbox" type="checkbox" v-model="game.notesMode" /><label for="notes-checkbox">Notes</label>
            </div>

            <div class="input-container" v-if="!game.notesMode">
    
                <div v-for="index in 9">
                    <div class="input-button" @click="enterInSelectedCell(index)" :class="{'input-button-disabled': countInstances[index] >= 9}">
                        {{ index }}
                        <span class="input-button-count">{{ 9 - countInstances[index] }}</span>
                    </div>
                </div>
                <div class="input-button clear-button" @click="enterInSelectedCell(0)" :class="{'input-button-disabled': !cellEditable(selectedCell.x, selectedCell.y) || game.board[selectedCell.y][selectedCell.x] == 0}" >
                    Clear
                </div>
            </div>
            
            <div class="input-container" v-else>
    
                <div v-for="index in 9">
                    <div class="input-button input-button-notes" @click="toggleNoteInSelectedCell(index)" :class="{'input-button-disabled': countInstances[index] >= 9}">
                        {{ index }}
                    </div>
                </div>
                <div class="input-button input-button-notes clear-button" @click="clearNotesInSelectedCell()" v-if="cellEditable(selectedCell.x, selectedCell.y)">
                    Clear
                </div>
                <div class="input-button input-button-notes clear-button" @click="clearAllNotes()">
                    Clear all notes
                </div>
            </div>
        </div>
    </main>
</template>

<style scoped>

header {
    padding-top: 2em;
    padding-bottom: 1em;
    text-align: center;
    background-color: white;
    background-position: center;
    background-size: cover;
    width: 100vw;
    border-bottom: 1px solid #5c5c5c;
    position: relative;
}
.header-text {
    font-size: calc(1.625rem + 3vw);
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
    align-items: center;
    padding-left: 1em;
    padding-right: 1em;
}

.win-background {
    background-color: green;
}
.board-container {
    display: flex;
    justify-content: center;
    align-items: center;
    flex-direction: column;
    margin-top: 5vh;
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
    background-color: white;
    justify-content: center;
    align-items: center;
    width: 10vw;
    height: 10vw;
    max-width: 2.5em;
    max-height: 2.5em;
    border: 1px solid grey;
    user-select: none;
    font-weight: 600;
    cursor: pointer;
}

.board-cell:hover {
    /* background-color: lightgreen; */
    box-shadow: inset 0px 0px 0px 1px blue;
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

.user-entered {
    font-weight: 400;
    color: rgb(0, 0, 220);
}

.relevant-square {
    background-color: rgb(230, 230, 230);
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

#input-area {
    text-align: center;
}

#remaining-numbers {
    margin-top: 1em;
}

.input-container {
    margin-left: 2vw;
    margin-right: 2vw;
    margin-top: 1.5vh;
    margin-bottom: 1.5vh;
    display: flex;
    flex-wrap: wrap;
    width: 12em;
    height: fit-content;
    justify-content: center;
    align-items: center;
    border: 1px solid lightgrey;
    padding: 1em;
    border-radius: 2%;
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
    position: relative;
    background-color: white;
}

.input-button:hover {
    background-color: rgb(218, 218, 218);
}

.input-button-disabled {
    visibility: hidden;
}

.input-button-count {
    font-size: 0.7em;
    color: rgb(180, 180, 180);
    position: absolute;
    bottom: 0.3em;
    right: 0.3em;
}

.input-button-notes {
    color: grey;
}

.clear-button {
    width: 10.2em;
}

#menubar {
 display: flex;
 justify-content: center;
 margin-top: 1.2em;
}

#controls {
    display: flex;
    justify-content: space-between;
    width: 95vw;
}

.difficulty {
    font-weight: 600;
    font-size: 2em;
    text-align: center;
    margin: 0.25em;
    color: white;
    text-shadow: 0px 0px 5px rgba(0,0,0,1);
}

#loading {
    display: flex;
    justify-content: center;
    align-items: center;
    margin-top: 6em;
}

.controls-button {
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 0.5em;
    /* border: 0.1em solid grey; */
    margin: 0.2em;
    border-radius: 0.25em;
    cursor: pointer;
    text-align: center;
    
    color: white;
    text-shadow: 0px 0px 5px rgba(0,0,0,1);
}

.controls-button:hover {
    background-color: rgb(218, 218, 218);
}

.invisible {
    visibility: hidden;
}

#notes-checkbox {
    width: 1.2em;
    height: 1.2em;
}

.notes-checkbox-container {
    margin-top: 1em;
    display: flex;
    align-items: center;
    justify-content: center;
}

.loader {
  border: 16px solid #f3f3f3; /* Light grey */
  border-top: 16px solid #3498db; /* Blue */
  border-radius: 50%;
  width: 120px;
  height: 120px;
  animation: spin 2s linear infinite;
}

.dropdown-button {
    position: absolute;
    top: 0.5em;
    right: 0.5em;
}

.dropdown-content {
    background-color: white;
    position: absolute;
    top: 1em;
    right: 1em;
    padding: 2em;
    border: 1px solid grey;
    border-radius: 3%;
    max-height: 15em;
    overflow-y: scroll;
}

.theme-button {
    position: absolute;
    top: 1em;
    right: 1em;
} 

.dropdown-item {
    padding: 1em;
    cursor: pointer;
    border-radius: 10%;
} 

.dropdown-item:hover {
    background-color: lightgrey;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

</style>
