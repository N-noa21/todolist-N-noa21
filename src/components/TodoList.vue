<script setup lang="ts">
import { computed, ref } from "vue"

interface Task { //interfaceは型を確かめるためのもの
    name: string
    isFinished: boolean 
}

const tasks = ref<Task[]>([])
//完了済みのタスクを、computedにより自動で反映、filterにより、isFinished==Trueのみを取り出している
//アロー関数の左辺の()が空より、入力なし
//tasksの値のみ返している
const FinishedTasks = computed(() => tasks.value.filter((task) => task.isFinished))

const NotFinishedTasks = computed(() => tasks.value.filter((task) => !task.isFinished))

const NewTaskName = ref("")
// タスクを追加
const addTask = () => {
    if (NewTaskName.value == "") { // 入力が空
        alert("タスク名が空です")
        return 
    }

    if (tasks.value.some((task) => task.name === NewTaskName.value)) {
        alert("既に登録されています")
        return
    }

    tasks.value.push({
        name: NewTaskName.value,
        isFinished:false
    })
    NewTaskName.value = ""
}
//タスクを終了
const finishTask = (taskName: string) => {
    tasks.value = tasks.value.map((task) => {
        if (task.name === taskName) {
            return {
                ...task,
                isFinished: true
            }
        }
    return task
    })
}
</script>

<template>
    <div>
        <div>TodoList</div>
        <div>完了済みタスク</div>

        <ul>
            <li v-for="task in FinishedTasks" :key="task.name">
                <div>{{ task.name }}</div>
            </li>

        </ul>

        <div>未完タスク</div>

        <ul>
            <li v-for="task in NotFinishedTasks" :key="task.name">
                <div>{{ task.name }}</div>
                <div>
                    <button @click="finishTask(task.name)">完了する</button>
                </div>
            </li>

        </ul>

        <div>
            <label>
                名前
                <input v-model="NewTaskName" type="text" />
            </label>
            <button @click="addTask">追加</button>
        </div>

    </div>
</template>

<style></style>