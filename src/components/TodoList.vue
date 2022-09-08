<template>
  <v-container text-center wrap md12>
    <v-card class="mx-auto" outlined max-width="1200">
      <v-card-title>
        <v-text-field
          placeholder="追加する作業を入力してください"
          v-model="task"
        ></v-text-field>
        <v-select
          :items="assignees"
          label="担当者を選択してください"
          solo
          class="mt-2"
          v-model="assignee"
        ></v-select>
        <v-btn color="primary" dark class="mb-2" @click="addTask()">追加</v-btn>
      </v-card-title>
      <v-data-table
        :headers="headers"
        :items="items"
        :items-per-page="5"
        class="elevation-1"
      >
        <template v-slot:item.control="{ item }">
          <v-btn
            class="mx-2"
            fab
            dark
            x-small
            color="error"
            @click="deleteTask(item)"
          >
            <v-icon dark>mdi-minus</v-icon>
          </v-btn>
        </template>
      </v-data-table>
    </v-card>
  </v-container>
</template>

<script lang="ts">
import { defineComponent } from "vue";

export default defineComponent({
  name: "TodoList",
  data: () => ({
    headers: [
      {
        text: "作業名",
        sortable: true,
        value: "task",
        width: "70%",
      },
      {
        text: "担当者",
        sortable: true,
        value: "assignee",
      },
      {
        text: "操作",
        sortable: false,
        value: "control",
      },
    ],
    items: [],
    assignees: ["担当者A", "担当者B", "担当者C", "担当者D", "担当者E"],
    task: "",
    assignee: "",
  }),
  methods: {
    addTask: function () {
      // 未入力エラー
      if (!this.task || !this.assignee) {
        alert("タスク名と作業者を入力してください。");
        return;
      }
      // タスク追加
      this.items.push({
        task: this.task,
        assignee: this.assignee,
      });
      // 入力値クリア
      this.task = "";
      this.assignee = "";
    },
    deleteTask: function (item) {
      this.items.splice(this.items.indexOf(item), 1);
    },
  },
});
</script>
