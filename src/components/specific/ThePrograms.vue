<template>
    <div class="d-flex flex-column">
        <div class="d-flex justify-end pb-4">
            <v-btn color="accent" @click="$router.push('/applications/program-create')">Добавить программу</v-btn>
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
                    <v-btn icon color="indigo" @click="deleteProgram(program['id'])">
                        <v-icon>mdi-trash-can-outline</v-icon>
                    </v-btn>
                </div>
            </div>
        </div>
        <v-alert v-if="programDeleted"  dismissible type="success" class="alert">Программа удалена</v-alert>
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
            programs: [
                {
                    id: 1,
                    name: 'Template 1',
                },
                {
                    id: 2,
                    name: 'Template 2',
                },
                {
                    id: 3,
                    name: 'Template 3',
                },
                {
                    id: 4,
                    name: 'Template 4',
                },
                {
                    id: 5,
                    name: 'Template 5',
                },
                {
                    id: 6,
                    name: 'Template 6',
                },
                {
                    id: 7,
                    name: 'Template 7',
                },
                {
                    id: 8,
                    name: 'Template 8',
                },
            ],
            lastHoveredProgramId: 0,
            programDeleted: false,
        }
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
        deleteProgram(id) {
            console.log('удалить' + id);
            this.programDeleted = true;
        },
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
    background-color: rgb(211, 176, 254);
    object-fit: scale-down;
    object-position: center center;
}

.program:hover {
    background-color: rgb(32, 178, 170, .1);
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
