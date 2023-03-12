<template>
    <div class="d-flex flex-column">
        <div class="back-navigation text-subtitle-1" @click="$router.push('/applications/programs')">
            <i class="mdi mdi-chevron-left"></i>
            Назад
        </div>
        <h2 class="pt-2 mb-6">Редактирование программы</h2>
        <div class="d-flex justify-space-between">
            <div class="d-flex flex-column two-columns">
                <field-edit title="Название программы" placeholder="Введите название программы" :initial-value="programName"
                    class="mb-6"></field-edit>

                <field-edit title="Путь к программе" placeholder="Введите путь к программе" :initial-value="programName"
                    class="mb-4"></field-edit>
                <field-edit placeholder="Введите путь к программе" :initial-value="programName" class="mb-4"></field-edit>
                <field-edit placeholder="Введите путь к программе" :initial-value="programName" class="mb-6"></field-edit>

                <field-edit title="Путь к иконке" placeholder="Введите путь к иконке" :initial-value="programName"
                    class="mb-6"></field-edit>

                <field-edit title="Аргумент командной строки" placeholder="Введите аргумент командной строки" :initial-value="programName"
                    class="mb-6"></field-edit>

                <field-edit title="Рабочая директория" placeholder="Укажите рабочую директорию" :initial-value="programName"
                    class="mb-6"></field-edit>

                <div class="text-subtitle-1 mb-2">Группа аккаунтов</div>
                <v-select :items="accountGroupOptions" solo></v-select>

                <field-edit title="Скрипт запуска" placeholder="Введите скрипт запуска" :initial-value="programName"
                    class="mb-6"></field-edit>

                <field-edit title="Пароль запуска" placeholder="Введите новый пароль" :initial-value="programName"
                    class="mb-6"></field-edit>

                <div class="text-subtitle-1 mb-2">Дополнительно</div>
                <field-check class="mb-6" :value.sync="programData.is_admin" true-label="Запускать от имени администратора"
                    false-label="Запускать от имени администратора"></field-check>

                <div class="d-flex justify-space-between">
                    <v-btn color="two-columns">Удалить</v-btn>
                    <v-btn color="accent two-columns">Сохранить</v-btn>
                </div>
            </div>
            <div class="d-flex flex-column two-columns align-center">
            </div>
        </div>

    </div>
</template>

<script>
import FieldEdit from '../../common/FieldEdit.vue'
import FieldCheck from '../../common/FieldCheck.vue'

export default {
    name: 'ProgramEdit',
    components: { FieldEdit, FieldCheck },
    props: {
    },
    data: function () {
        return {
            form: {
                avatar: null,
            },
            programData: {
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
        programName: {
            get: function () {
                return this?.programData?.program_name ?? '';
            },
            set: function (newVal) {
                this.programData.program_name = newVal;
            },
        },
        accountGroup: {
            get: function () {
                return this?.programData?.account_group ?? '';
            },
            set: function (newVal) {
                this.programData.account_group = newVal;
            },
        },
    },
    methods: {

    },
}

</script>
