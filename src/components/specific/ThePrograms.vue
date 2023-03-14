<template>
    <div class="d-flex flex-column">
        <div class="d-flex justify-end pb-4">
            <v-btn color="primary" x-large @click="$router.push('/applications/program-create')">Добавить программу</v-btn>
        </div>
        <div class="d-flex flex-wrap">
            <div v-for="(program, i) in programs" :key="i" class="d-flex flex-column align-center px-2 pb-2 pt-10 program"
                @mouseover="handleMouseOver(program['id'])" @mouseout="handleMouseOut()">
                <div class="program-img"></div>
                <div class="d-flex text-subtitle-1 program-name pt-2">{{ program.name }}</div>
                <div class="program-edit" v-show="isVisible(program)">
                    <v-btn icon color="indigo" @click="editProgram(program['id'])">
                        <v-icon>mdi-pencil</v-icon>
                    </v-btn>
                    <v-btn icon color="indigo" @click="deleteProgram(program)">
                        <v-icon>mdi-trash-can-outline</v-icon>
                    </v-btn>
                </div>
            </div>
        </div>
        <v-alert v-if="programDeleted"  dismissible type="success" class="alert">Программа {{lastClickedProgramName}} удалена</v-alert>
    </div>
</template>

<script>
export default {
    name: 'ThePrograms',
    components: {},
    props: {
    },
    data: function () {
        return {
            lastHoveredProgramId: 0,
            programDeleted: false,
            programs: [],
            lastClickedProgramName: '',
        }
    },
    computed: {
        requestRoute: function () {
            return process.env.VUE_APP_HOST + '/shell/programs';
        },
    },
    methods: {
        handleMouseOver(id) {
            this.lastHoveredProgramId = id;
        },
        handleMouseOut() {
            this.lastHoveredProgramId = 0;
        },
        isVisible(program) {
            return program['id'] === this.lastHoveredProgramId;
        },
        editProgram(id) {
            this.$router.push('/applications/programs/' + id)
        },
        deleteProgram(game) {
            const url = process.env.VUE_APP_HOST + '/shell/programs/' + game.id;
            this.lastClickedProgramName = game.name;
            this.axios.delete(
                url,
            ).then(response => {
                if (response.data?.success) {
                    this.updateData();
                    this.programDeleted = true;
                } else {
                    this.isUpdateError = true;
                    console.log(response?.data);
                }
            }).catch(error => {
                console.log(error);
            });
        },
        updateData() {
            this.axios.get(
                this.requestRoute,
            ).then(response => {
                if (response.data?.success) {
                    this.programs = response?.data?.items;
                } else {
                    console.log(response?.data);
                }
            }).catch(error => {
                console.log(error);
            });
        },
    },
    created() {
        this.updateData();
    },
}

</script>

<style  lang="scss">
.program {
    width: 150px;
    position: relative;
}

.program-edit {
    position: absolute;
    top: 2px;
    right: 20px;
    display: flex;
}

.program-img {
    width: 80px;
    height: 80px;
    border-radius: 12px;
    background-color: #1867c0;
    object-fit: scale-down;
    object-position: center center;
}

.program:hover {
    background-color: #dbe7f5;
    border-radius: 12px;
    cursor: default;
}

.program-name {
    width: 80px;
}
.alert {
    position: fixed;
    bottom: 0;
    right: 32px;
}
</style>
