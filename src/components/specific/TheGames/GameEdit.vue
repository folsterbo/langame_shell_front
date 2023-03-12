<template>
    <div class="d-flex flex-column">
        <div class="back-navigation text-subtitle-1" @click="$router.push('/applications/games')">
            <i class="mdi mdi-chevron-left"></i>
            Назад
        </div>
        <h2 class="pt-2 mb-6">Редактирование игры</h2>
        <div class="d-flex justify-space-between">
            <div class="d-flex flex-column two-columns">
                <field-edit title="Название игры" placeholder="Введите название игры" :initial-value="gameName"
                    class="mb-6"></field-edit>

                <field-edit title="Путь к Игре" placeholder="Введите путь к игре" :initial-value="gameName"
                    class="mb-4"></field-edit>
                <field-edit placeholder="Введите путь к игре" :initial-value="gameName" class="mb-4"></field-edit>
                <field-edit placeholder="Введите путь к игре" :initial-value="gameName" class="mb-6"></field-edit>

                <field-edit title="Аргумент командной строки" placeholder="Введите аргумент командной строки" :initial-value="gameName"
                    class="mb-6"></field-edit>

                <field-edit title="Рабочая директория" placeholder="Укажите рабочую директорию" :initial-value="gameName"
                    class="mb-6"></field-edit>

                <div class="text-subtitle-1 mb-2">Группа аккаунтов</div>
                <v-select :items="accountGroupOptions" solo></v-select>

                <field-edit title="Скрипт запуска" placeholder="Введите скрипт запуска" :initial-value="gameName"
                    class="mb-6"></field-edit>

                <field-edit title="Пароль запуска" placeholder="Введите новый пароль" :initial-value="gameName"
                    class="mb-6"></field-edit>

                <div class="text-subtitle-1 mb-2">Возрастное ограничение</div>
                <field-check class="mb-6" :value.sync="gameData.is_age_restriction"
                    true-label="Ограничить возрастной контент" false-label="Ограничить возрастной контент"></field-check>

                <div v-show="gameData.is_age_restriction" class="mb-6">
                    <v-btn-toggle v-model="gameData.age_restriction">
                        <v-btn>
                            0+
                        </v-btn>
                        <v-btn>
                            6+
                        </v-btn>
                        <v-btn>
                            12+
                        </v-btn>
                        <v-btn>
                            16+
                        </v-btn>
                        <v-btn>
                            18+
                        </v-btn>
                    </v-btn-toggle>
                </div>

                <div class="text-subtitle-1 mb-2">Дополнительно</div>
                <field-check class="mb-6" :value.sync="gameData.is_admin" true-label="Запускать от имени администратора"
                    false-label="Запускать от имени администратора"></field-check>

                <div class="d-flex justify-space-between">
                    <v-btn color="two-columns">Удалить</v-btn>
                    <v-btn color="accent two-columns">Сохранить</v-btn>
                </div>
            </div>
            <div class="d-flex flex-column two-columns align-center">
                <div>
                    <div class="text-subtitle-1 mb-2">Обложка игры</div>
                    <game-avatar-input v-model="form.avatar"
                        :default-src="require('../../../assets/img/default_image.png')"></game-avatar-input>
                </div>
            </div>
        </div>

    </div>
</template>

<script>
import FieldEdit from '../../common/FieldEdit.vue'
import FieldCheck from '../../common/FieldCheck.vue'
import GameAvatarInput from '../../common/GameAvatarInput.vue'
export default {
    name: 'GameEdit',
    components: { GameAvatarInput, FieldEdit, FieldCheck },
    props: {
    },
    data: function () {
        return {
            form: {
                avatar: null,
            },
            gameData: {
                name: '',
                account_group: '',
                is_age_restriction: false,
                is_admin: false,
                age_restriction: '',
            },
            accountGroupOptions: ['account_group_1', 'account_group_2', 'account_group_3'],
        }
    },
    computed: {
        gameName: {
            get: function () {
                return this?.gameData?.game_name ?? '';
            },
            set: function (newVal) {
                this.gameData.game_name = newVal;
            },
        },
        accountGroup: {
            get: function () {
                return this?.gameData?.account_group ?? '';
            },
            set: function (newVal) {
                this.gameData.account_group = newVal;
            },
        },
    },
    methods: {

    },
}

</script>
