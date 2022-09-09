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
      <v-list v-for="item in items" :key="item.id" cols="12">
        <v-list-item-group>
          <v-list-item>
            <v-list-item-content>
              <v-list-item-title>{{ item.id }}</v-list-item-title>
            </v-list-item-content>
            <v-list-item-content>
              <v-list-item-title>{{ item.task }}</v-list-item-title>
            </v-list-item-content>
          </v-list-item>
        </v-list-item-group>
      </v-list>
    </v-card>
  </v-container>
</template>

<script lang="ts">
import { defineComponent } from "vue";

interface Item {
  id: number;
  task: string;
  assignee: string;
  control: boolean;
}

interface Header {
  text: string;
  sortable: boolean;
  value: string;
  width?: string;
}

export default defineComponent({
  name: "TodoList",
  data: (): {
    headers: Header[];
    items: Item[];
    assignees: ("担当者A" | "担当者B" | "担当者C" | "担当者D" | "担当者E")[];
    task: string;
    assignee: string;
  } => ({
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
        id: Date.now(),
        task: this.task,
        assignee: this.assignee,
        control: false,
      });
      // 入力値クリア
      this.task = "";
      this.assignee = "";
      console.log(this.items);
    },
    deleteTask: function (id: number) {
      this.items.filter((item) => item.id !== id);
    },
  },
});
</script>
