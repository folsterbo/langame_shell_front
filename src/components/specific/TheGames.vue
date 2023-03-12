<template>
    <div class="d-flex flex-column">
        <div class="d-flex justify-end pb-4">
            <v-btn color="accent" @click="$router.push('/applications/game-create')">Добавить игру</v-btn>
        </div>
        <div class="d-flex flex-wrap">
            <div v-for="(game, i) in games" :key="i" class="d-flex flex-column align-center px-2 pb-2 pt-10 game"
                @mouseover="handleMouseOver(game['id'])" @mouseout="handleMouseOut()">
                <img :src="game.image" alt="img" class="game-img">
                <div class="d-flex text-subtitle-1 game-name pt-2">{{ game.name }}</div>
                <div class="game-edit" v-show="isVisible(game)">
                    <v-btn icon color="indigo" @click="editGame(game['id'])">
                        <v-icon>mdi-pencil</v-icon>
                    </v-btn>
                    <v-btn icon color="indigo" @click="deleteGame(game['id'])">
                        <v-icon>mdi-trash-can-outline</v-icon>
                    </v-btn>
                </div>
            </div>
        </div>
        <v-alert v-if="gameDeleted"  dismissible type="success" class="alert">Игра удалена</v-alert>
    </div>
</template>

<script>
export default {
    name: 'TheGames',
    components: {},
    props: {
    },
    data: function () {
        return {
            games: [
                {
                    id: 1,
                    name: 'World of Warcraft',
                    image: require('../../assets/img/2023-03-03-the-cabin-on-the-lake-1-58020.jpeg')
                },
                {
                    id: 2,
                    name: 'Apex Legends',
                    image: require('../../assets/img/2023-03-06-the-top-of-the-mountain-1-58073.jpeg')
                },
                {
                    id: 3,
                    name: 'The Elder Scrolls 5: Skyrim',
                    image: require('../../assets/img/2023-03-07-kitty-1-58107.jpeg')
                },
                {
                    id: 4,
                    name: 'Batman: Arkham City',
                    image: require('../../assets/img/2023-03-08-northern-cardinal-1-58144.jpeg')
                },
                {
                    id: 5,
                    name: 'Starfield',
                    image: require('../../assets/img/starfield-mobile.jpg')
                },
                {
                    id: 6,
                    name: 'Diablo IV',
                    image: require('../../assets/img/11ad4aa209-1_1390x600.jpg')
                },
                {
                    id: 7,
                    name: 'Star Wars Jedi: Survivor',
                    image: require('../../assets/img/hhgwp96sk6gvzpdudurfog.jpeg')
                },
                {
                    id: 8,
                    name: 'Redfall',
                    image: require('../../assets/img/redfall.jpeg')
                },
            ],
            lastHoveredGameId: 0,
            gameDeleted: false,
        }
    },
    methods: {
        handleMouseOver(id) {
            this.lastHoveredGameId = id;
        },
        handleMouseOut() {
            this.lastHoveredGameId = 0;
        },
        isVisible(game) {
            return game['id'] === this.lastHoveredGameId;
        },
        editGame(id) {
            this.$router.push('/applications/games/' + id)
        },
        deleteGame(id) {
            console.log('удалить' + id);
            this.gameDeleted = true;
        },
    },
}

</script>

<style  lang="scss">
.game {
    width: 190px;
    position: relative;
}

.game-edit {
    position: absolute;
    top: 2px;
    right: 20px;
    display: flex;
}

.game-img {
    width: 150px;
    height: 240px;
    border-radius: 12px;
    object-fit: cover;
    object-position: center center;
}

.game:hover {
    background-color: rgb(32, 178, 170, .1);
    border-radius: 12px;
    cursor: default;
}

.game-name {
    width: 150px;
}
.alert {
    position: fixed;
    bottom: 0;
    right: 32px;
}
</style>
